## 1. Escenario y Contexto de CTI

Como parte del flujo operativo de **Detection Engineering**, el equipo de **Cyber Threat Intelligence (CTI)** entrega un reporte accionable sobre un patrón de persistencia asociado al actor:

- **APT41** → [https://attack.mitre.org/groups/G0096/](https://attack.mitre.org/groups/G0096/)
    

### **TTP identificado**

- **Táctica:** Persistencia (**TA0003**) → [https://attack.mitre.org/tactics/TA0003/](https://attack.mitre.org/tactics/TA0003/)
    
- **Técnica asociada:** Creación de servicio + abuso de `svchost`
    

### **Características del comportamiento**

- Uso de:
    
    - `sc.exe`
        
    - `reg.exe`
        
- Creación manual de servicio fuera de instaladores estándar
    
- Registro del servicio en:
    
    - `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Svchost`
        

**Interpretación técnica:**  
No es el uso individual de herramientas lo que define el ataque, sino la **secuencia coordinada de acciones**.

---

## 2. Validación en Laboratorio (Gap Analysis)

### Resultado

- **Sin alertas del SIEM/EDR**
    
- Eventos visibles pero no correlacionados
    

### Evidencia observada

- `cmd.exe /c .\depl.bat`
    
- Ejecución secuencial de:
    
    - `reg.exe`
        
    - `sc.exe`
        

### Problema identificado

- Detección basada en eventos individuales
    
- Falta de correlación multi-evento
    

**Conclusión técnica:**  
Existe un **gap de detección por ausencia de lógica comportamental**.

---

## 3. Estrategia de Detección (Enfoque Correcto)

### Modelo de detección

No basado en:

- IoCs
    
- Binarios
    

Basado en:

- **Correlación temporal + semántica**
    

### Eventos a correlacionar

#### Evento A (Registro)

- Modificación de:
    
    - `Svchost`
        
- Herramienta:
    
    - `reg.exe`
        

#### Evento B (Servicio)

- Creación de servicio:
    
    - `sc.exe`
        
- Uso de:
    
    - `svchost.exe -k <service>`
        

### Condiciones de correlación

- Mismo:
    
    - `DeviceId`
        
    - `ServiceName`
        
- Ventana temporal:
    
    - ≤ 20 segundos
        
- Opcional:
    
    - Mismo proceso padre
        

---

## 4. Query de Caza (KQL)

```kql
let RegServiceCreation = DeviceProcessEvents
| where Timestamp > ago(1d)
| where tolower(FileName) == "reg.exe" 
| where ProcessCommandLine contains "add" 
  and ProcessCommandLine contains "currentversion" 
  and ProcessCommandLine contains "svchost"
| extend Reg_ServiceName = tolower(extract(@'\/v\s+[\"]?(\w+)', 1, tolower(ProcessCommandLine))),
         Reg_ParentProcessId = InitiatingProcessId,
         Reg_Timestamp = Timestamp;

let ScServiceCreation = DeviceProcessEvents
| where Timestamp > ago(1d)
| where tolower(FileName) == "sc.exe" 
| where ProcessCommandLine contains "create" 
  and ProcessCommandLine contains "svchost.exe"
| extend Sc_ServiceName = tolower(extract(@'svchost\.exe\s+-k\s+[\"]?(\w+)', 1, tolower(ProcessCommandLine))),
         Sc_ParentProcessId = InitiatingProcessId,
         Sc_Timestamp = Timestamp;

RegServiceCreation
| join kind=inner (ScServiceCreation) on DeviceId
| where Reg_ServiceName == Sc_ServiceName
| where (Reg_ParentProcessId == Sc_ParentProcessId 
        or abs(datetime_diff('second', Reg_Timestamp, Sc_Timestamp)) < 20)
| project Timestamp, DeviceName, Reg_ServiceName, ProcessCommandLine
```

---

## 5. Resultado Operativo

### Evaluación

- **Falsos positivos:** Muy bajos o nulos
    
- **Cobertura:** Alta para este TTP específico
    

### Acción

- Conversión a:
    
    - **Regla de detección en SIEM**
        
    - Posible alerta en EDR
        

### Mejora lograda

- CTI → Detección real
    
- Indicador → Capacidad defensiva
    

---

## 6. Lección Clave (Detection Engineering)

La integración efectiva con CTI implica:

- Traducir:
    
    - **Reporte → comportamiento observable**
        
- Diseñar:
    
    - **Correlaciones, no firmas**
        
- Validar:
    
    - En laboratorio antes de producción
        

**Principio técnico:**

> Un TTP no se detecta por herramientas individuales, sino por la relación entre acciones en el tiempo.

---

## Referencias Externas

- [https://attack.mitre.org/groups/G0096/](https://attack.mitre.org/groups/G0096/)
    
- [https://attack.mitre.org/tactics/TA0003/](https://attack.mitre.org/tactics/TA0003/)
    
- [https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-overview](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-overview)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[09 - Uso de IoCs de fuentes abiertas]]  
[[10 - Convertir inteligencia en hipótesis de hunting]]