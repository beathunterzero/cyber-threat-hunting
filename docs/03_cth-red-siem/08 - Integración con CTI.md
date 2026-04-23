## 1. Escenario y Contexto de CTI

Como parte del equipo de ingeniería de detección, se recibe un reporte del equipo de **Cyber Threat Intelligence (CTI)**. Han identificado un patrón de persistencia utilizado en múltiples campañas por el actor de amenazas **APT41**.

### **TTP: TA0003 - Persistencia (Creación de Servicio Manual)**

El atacante utiliza un script de procesamiento por lotes (`.bat`) para instalar un servicio malicioso de forma manual, evadiendo las rutas de instalación estándar. El script utiliza `sc.exe` y `reg.exe`.

**Plantilla del Script de Persistencia:**

Fragmento de código

```code
@echo off
set "WORK_DIR=C:\Windows\System32"
set "DLL_NAME=<nombre_dll>"
set "SERVICE_NAME=<nombre_servicio>"

:: Detener y eliminar versiones previas
sc stop %SERVICE_NAME%
sc delete %SERVICE_NAME%

:: Copiar la DLL maliciosa al directorio del sistema
copy "%~dp0%DLL_NAME%" "%WORK_DIR%" /Y

:: Registro de Svchost para alojar el servicio
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Svchost" /v "%SERVICE_NAME%" /t REG_MULTI_SZ /d "%SERVICE_NAME%" /f

:: Creación del servicio persistente
sc create "%SERVICE_NAME%" binPath= "%SystemRoot%\system32\svchost.exe -k %SERVICE_NAME%" type= share start= auto error= ignore DisplayName= "%DISPLAY_NAME%"

:: Configuración de recuperación y parámetros
SC failure "%SERVICE_NAME%" reset= 86400 actions= restart/60000/restart/60000/restart/60000
reg add "HKLM\SYSTEM\CurrentControlSet\Services\%SERVICE_NAME%\Parameters" /v "ServiceDll" /t REG_EXPAND_SZ /d "%WORK_DIR%\%DLL_NAME%" /f

:: Inicio del servicio
net start "%SERVICE_NAME%"
```

---

## 2. Validación en Laboratorio (Gap Analysis)

Al ejecutar este script en un entorno controlado para evaluar la capacidad de detección, se observa un hallazgo crítico: **Ni el EDR ni las reglas actuales del SIEM/HIDS generaron una alerta.**

### **Análisis Forense de la Ejecución:**

- **Proceso Padre:** `powershell.exe` o `cmd.exe`.
    
- **Comando detectado:** `cmd.exe /c .\depl.bat`.
    
- **Resultado:** Aunque las herramientas ven los procesos individuales (`sc.exe`, `reg.exe`), no interpretan la secuencia como un ataque coordinado de persistencia de APT41.
    

---

## 3. Estrategia de Correlación

Para detectar este comportamiento de manera efectiva sin inundar el SOC con falsos positivos (por instalaciones legítimas), se debe crear una consulta que **correlacione dos eventos específicos** que ocurren en un margen de tiempo corto:

1. **Evento A:** Modificación del registro en la clave `Svchost` (vía `reg.exe`).
    
2. **Evento B:** Creación de un nuevo servicio que apunte a `svchost.exe` (vía `sc.exe`).
    

Ambos eventos deben compartir el mismo **ID de dispositivo** y el mismo **Nombre de Servicio**.

---

## 4. Query de Cacería (Kusto Query Language - KQL)

Esta consulta une las dos actividades sospechosas para identificar la persistencia del APT41:

Fragmento de código

```kql
// Definimos la parte de creación en el registro
let RegServiceCreation = DeviceProcessEvents
| where Timestamp > ago(1d)
| where tolower(FileName) == "reg.exe" 
| where ProcessCommandLine contains "add" 
  and ProcessCommandLine contains "currentversion" 
  and ProcessCommandLine contains "svchost"
| extend Reg_ServiceName = tolower(extract(@'\/v\s+[\"]?(\w+)', 1, tolower(ProcessCommandLine))),
         Reg_ParentProcessId = InitiatingProcessId,
         Reg_Timestamp = Timestamp;

// Definimos la parte de creación del servicio con sc.exe
let ScServiceCreation = DeviceProcessEvents
| where Timestamp > ago(1d)
| where tolower(FileName) == "sc.exe" 
| where ProcessCommandLine contains "create" 
  and ProcessCommandLine contains "svchost.exe"
| extend Sc_ServiceName = tolower(extract(@'svchost\.exe\s+-k\s+[\"]?(\w+)', 1, tolower(ProcessCommandLine))),
         Sc_ParentProcessId = InitiatingProcessId,
         Sc_Timestamp = Timestamp;

// Unimos ambas tablas por DeviceId y Nombre del Servicio
RegServiceCreation
| join kind=inner (ScServiceCreation) on $left.DeviceId == $right.DeviceId
| where Reg_ServiceName == Sc_ServiceName
| where (Reg_ParentProcessId == Sc_ParentProcessId 
        or abs(datetime_diff('second', Reg_Timestamp, Sc_Timestamp)) < 20)
| project Timestamp, DeviceName, Reg_ServiceName, Reg_ParentProcessId, Sc_Timestamp, ProcessCommandLine
```

---

## 5. Conclusión y Despliegue

Tras ejecutar la búsqueda en un período amplio, se determina lo siguiente:

- **Falsos Positivos:** 0 (Este método de creación manual no es común en software comercial).
    
- **Acción:** La consulta se convierte en una **Regla de Detección Automática** en el SIEM.
    
- **Resultado Operativo:** Se ha transformado un indicador de CTI en una capacidad de defensa activa, elevando la madurez del proceso de Threat Hunting.
    

---

### Referencias Externas

- [MITRE ATT&CK: APT41 (G0096)](https://attack.mitre.org/groups/G0096/)
    
- [Microsoft Defender for Endpoint: Advanced Hunting](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-overview)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[09 - Uso de IoCs de fuentes abiertas]]
[[10 - Convertir inteligencia en hipótesis de hunting]]