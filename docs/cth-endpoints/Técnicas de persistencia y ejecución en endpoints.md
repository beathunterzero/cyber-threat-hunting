## 1. Definición y Enfoque

La cacería de **persistencia y ejecución** es la búsqueda proactiva de actividades maliciosas en computadoras, servidores y dispositivos de usuario (endpoints). Está enfocada específicamente en detectar dos fases críticas del ciclo de vida del atacante:

- **Persistencia:** Cómo los atacantes se mantienen activos en el sistema y sobreviven a reinicios o cierres de sesión.
    
- **Ejecución:** Cómo lanzan su código dañino (payloads) interactuando con los recursos del sistema operativo.
    

## 2. Matriz de Técnicas, Ejemplos y Huellas (Footprints)

Basado en los vectores de ataque más comunes, a continuación se detallan las técnicas clave que todo Hunter debe monitorear, junto con sus ejemplos prácticos y los artefactos que dejan en la telemetría:

|**Técnica de Ataque**|**Ejemplo Práctico de Ejecución**|**Huellas (Footprints) para Detección**|
|---|---|---|
|**Claves de Registro (Windows Registry Run Keys)**|`HKCU\Software\Microsoft\Windows\CurrentVersion\Run\Updater.exe`|Creación o edición de valores persistentes en las rutas de auto-arranque del registro. _(Sysmon Event ID 12, 13, 14)._|
|**Tareas Programadas (Scheduled Tasks)**|`schtasks /create /sc minute /tn "OfficeUpdate" /tr "malware.exe"`|Eventos **ID 4698** (Tarea Creada) y **4702** (Tarea Actualizada) en los logs de seguridad nativos de Windows.|
|**PowerShell con Código Codificado**|`powershell.exe -enc JABhAGwAdABlAHIA...` (Base64)|Eventos **ID 4104 (ScriptBlockLogging)** que revelan el código desofuscado antes de su ejecución en memoria.|
|**Inyección de Procesos (Process Injection)**|Malware que inyecta una DLL maliciosa dentro de un proceso legítimo como `explorer.exe` o `svchost.exe`.|Relaciones anómalas de procesos padre/hijo, o accesos sospechosos a la memoria de otros procesos _(Sysmon Event ID 8, 10)._|
|**Persistencia Fileless con WMI**|`wmic /namespace:\\root\subscription PATH __EventFilter`|Suscripciones WMI anómalas (_EventFilters_, _EventConsumers_) almacenadas directamente en el repositorio CIM.|

## 3. Estrategia de Caza en el Laboratorio

Para detectar estas técnicas en tu entorno de **Elastic Security** y **Velociraptor**, el enfoque debe ser el siguiente:

1. **Afinar el Baseline:** Los administradores de sistemas crean tareas programadas y modifican el registro constantemente. El Hunter debe filtrar el "ruido blanco" (acciones legítimas) para destacar las anomalías.
    
2. **Monitoreo de LOLBins:** Las herramientas listadas (PowerShell, WMIC, Schtasks) son binarios legítimos del sistema (_Living off the Land_). La alerta no debe saltar porque se use PowerShell, sino por los **argumentos** pasados al ejecutable (como el flag `-enc` o `-WindowStyle Hidden`).
    
3. **Inspección en Memoria:** Para técnicas como la inyección de procesos o la persistencia WMI (Fileless), el escaneo tradicional de antivirus en disco es ineficaz. Se requiere telemetría profunda de EDR (Velociraptor) para analizar los hilos de ejecución y la memoria asignada.
    

---

### Referencias Externas

- [MITRE ATT&CK: Persistence (TA0003)](https://attack.mitre.org/tactics/TA0003/)
    
- [MITRE ATT&CK: Execution (TA0002)](https://attack.mitre.org/tactics/TA0002/)
    
- [Microsoft: Investigating PowerShell Attacks](https://www.google.com/search?q=https://learn.microsoft.com/en-us/defender-for-endpoint/investigate-powershell-command)
    

### Documentación Relacionada

[[Threat Hunting basado en IoCs (IoC-Driven)]]
[[Filosofía y estrategia del Threat Hunting]]