## 1. ¿Qué se busca?

La cacería de **persistencia y ejecución** se enfoca en detectar:

- **Persistencia:** cómo el atacante mantiene acceso
    
- **Ejecución:** cómo lanza código malicioso
    

Ambas son fases críticas en endpoints.

---

## 2. Técnicas comunes y huellas

|Técnica|Ejemplo|Detección|
|---|---|---|
|Run Keys|`HKCU\...\Run\Updater.exe`|Sysmon 12, 13, 14|
|Scheduled Tasks|`schtasks /create ...`|Event 4698, 4702|
|PowerShell codificado|`powershell.exe -enc ...`|Event 4104|
|Process Injection|DLL en `explorer.exe`|Sysmon 8, 10|
|WMI Persistence|`__EventFilter`|WMI anómalo|

---

## 3. Enfoque de hunting

### 3.1 Baseline

- Identificar actividad normal
    
- Filtrar tareas legítimas
    
- Detectar desviaciones
    

---

### 3.2 Uso de LOLBins

- PowerShell, WMIC, Schtasks son legítimos
    
- El problema está en:
    
    - argumentos
        
    - comportamiento
        

Ejemplos sospechosos:

- `-enc`
    
- ejecución oculta
    
- descargas remotas
    

---

### 3.3 Análisis en memoria

Necesario para:

- Inyección de procesos
    
- Técnicas fileless
    
- Persistencia sin archivos
    

Requiere:

- EDR (ej. Velociraptor)
    
- Telemetría avanzada
    

---

## 4. Objetivo del hunting

- Detectar persistencia temprana
    
- Identificar ejecución maliciosa
    
- Evitar reentrada del atacante
    

---

## Referencias Externas

- [https://attack.mitre.org/tactics/TA0003/](https://attack.mitre.org/tactics/TA0003/)
    
- [https://attack.mitre.org/tactics/TA0002/](https://attack.mitre.org/tactics/TA0002/)
    
- [https://learn.microsoft.com/en-us/defender-for-endpoint/investigate-powershell-command](https://learn.microsoft.com/en-us/defender-for-endpoint/investigate-powershell-command)
    

---

## Documentación Relacionada

[[02 - Procesos sospechosos, inyección de código, LOLBAS]]  
[[03 - Técnicas de descubrimiento y movimiento lateral]]  
[[04 - Identificación de intentos de RDP, SMB y PASS-THE-HASH]]  
[[05 - Cazando anomalías en privilegios]]  
[[06 - Queries y hunting en EDR]]  
[[07 - Cómo formular búsquedas efectivas]]  
[[08 - Casos de ransomware, Cobalt Strike y keyloggers]]  
[[01 - Filosofía y estrategia del Threat Hunting]]