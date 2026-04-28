## 1. Definición del Concepto

Convertir inteligencia en hipótesis implica transformar datos de **Cyber Threat Intelligence (CTI)** —como TTPs, IoCs o patrones de ataque— en **suposiciones verificables dentro del entorno propio**.

No es una inferencia vaga, sino una **traducción técnica del comportamiento adversario a telemetría observable**.

**Objetivo operativo:**

> Pasar de “lo que hace el atacante” → a “cómo se ve en mis logs”

---

## 2. El Proceso de 5 Pasos

|**Paso**|**Fase**|**Descripción Operativa**|
|---|---|---|
|**1**|**Filtrado de Inteligencia**|Recolectar CTI (reportes, campañas, TTPs) y filtrar según relevancia real: tecnología, superficie expuesta y sector.|
|**2**|**Abstracción del Comportamiento (TTP)**|Eliminar nombres de herramientas o malware. Enfocarse en el comportamiento: ejecución, persistencia, movimiento lateral, C2.|
|**3**|**Mapeo a Telemetría**|Traducir la TTP a eventos concretos: procesos, red, autenticación, memoria, DNS. Definir qué logs permiten observar ese comportamiento.|
|**4**|**Formulación de la Hipótesis**|Redactar una hipótesis clara, verificable y medible basada en la telemetría identificada.|
|**5**|**Diseño, Ejecución y Validación**|Construir queries, ejecutar hunting, validar resultados, eliminar falsos positivos y convertir en detección si aplica.|

---

## 3. Corrección Clave (Error Común)

### ❌ Enfoque incorrecto

CTI → Query directa

- Dependencia de IoCs
    
- Alta tasa de falsos positivos
    
- Baja durabilidad de detección
    

---

### ✅ Enfoque correcto

CTI → TTP → Telemetría → Hipótesis → Query

---

### Interpretación técnica

- **CTI** aporta contexto
    
- **TTP** define comportamiento
    
- **Telemetría** define visibilidad
    
- **Hipótesis** estructura la búsqueda
    
- **Query** ejecuta la detección
    

---

### Principio operativo

> No se cazan indicadores, se cazan comportamientos observables en datos.

---

## 4. De la Inteligencia a la Hipótesis (Ejemplo Práctico)

### Inteligencia recibida

- Grupo:  
    [https://attack.mitre.org/groups/G0032/](https://attack.mitre.org/groups/G0032/)
    
- Técnica:  
    Uso de `.ISO` + `.LNK` + `regsvr32.exe`
    

---

### Abstracción de TTP

- Ejecución indirecta mediante contenedor (ISO)
    
- Uso de LOLBin (`regsvr32`)
    
- Carga de DLL desde rutas no estándar
    

---

### Hipótesis de Hunting

> “Si un adversario utiliza ejecución indirecta mediante contenedores montados, observaremos procesos `regsvr32.exe` ejecutando DLLs desde rutas no estándar y lanzados por procesos de usuario como `explorer.exe`.”

---

### Telemetría requerida

- Process Creation (Sysmon / EDR)
    
- CommandLine
    
- Parent Process
    
- File Path
    

---

### Query de ejemplo (KQL)

```kql
DeviceProcessEvents
| where FileName == "regsvr32.exe"
| where ProcessCommandLine contains ".dll"
| where not(ProcessCommandLine contains "system32")
| where InitiatingProcessFileName == "explorer.exe"
| project Timestamp, DeviceName, ProcessCommandLine, InitiatingProcessFileName
```

---

## 5. Template Operativo para Hipótesis

Para estandarizar en tu laboratorio:

1. **Técnica MITRE:**  
    [https://attack.mitre.org/](https://attack.mitre.org/)
    
2. **Contexto CTI:**  
    Actor / campaña / vector
    
3. **Hipótesis:**  
    Declaración verificable
    
4. **Telemetría requerida:**  
    Logs necesarios
    
5. **Condición de detección:**  
    Patrón esperado
    
6. **Query:**  
    Implementación técnica
    

---

## 6. Integración con el Proceso de Hunting

Relación con documentos:

- [[08 - Integración con CTI]] → Fuente
    
- [[09 - Uso de IoCs de fuentes abiertas]] → Input táctico
    
- [[10 - Convertir inteligencia en hipótesis de hunting]] → Transformación
    
- [[05 - Threat Hunting en SIEM]] / [[06 - Queries y hunting en EDR]] → Ejecución
    

---

## 7. Valor Operativo

Este proceso permite:

- Reducir dependencia de IoCs
    
- Aumentar detección basada en comportamiento
    
- Crear reglas duraderas
    
- Elevar la madurez del SOC
    

---

## 8. Conclusión Técnica

El Threat Hunting efectivo no consume inteligencia, la transforma en lógica operativa.

**Principio clave:**

> La inteligencia solo es útil cuando puede ejecutarse como una hipótesis verificable en la telemetría.

---

## Referencias Externas

- [https://attack.mitre.org/resources/working-with-attack/](https://attack.mitre.org/resources/working-with-attack/)
    
- [https://www.crowdstrike.com/cybersecurity-101/threat-hunting/](https://www.crowdstrike.com/cybersecurity-101/threat-hunting/)
    
- [https://attack.mitre.org/groups/G0032/](https://attack.mitre.org/groups/G0032/)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[08 - Integración con CTI]]  
[[09 - Uso de IoCs de fuentes abiertas]]