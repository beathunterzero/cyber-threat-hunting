## 1. Definición y Propósito

Consiste en el monitoreo, detección y análisis de actividades relacionadas con accesos remotos y autenticaciones anómalas dentro de un entorno informático. El objetivo es identificar el uso no autorizado de protocolos de administración y el movimiento lateral antes de que el adversario logre comprometer activos críticos.

## 2. Identificación de RDP (Remote Desktop Protocol)

El protocolo RDP es uno de los vectores más comunes para el movimiento lateral y la persistencia.

**Indicadores clave:**

- Nuevas conexiones RDP desde hosts internos anómalos o desde Internet.
    
- Múltiples intentos de autenticación fallida seguidos de un éxito (indicativo de _Brute Force_ o _Credential Stuffing_).
    
- Inicio de sesión con **LogonType 10** (RemoteInteractive) por cuentas que no tienen perfiles de administración asignados.
    
- Sesiones RDP iniciadas por cuentas de servicio o ejecutadas fuera del horario laboral establecido.
    

**Consulta de detección (Hunting Query - KQL):**

Fragmento de código

```kql
SecurityEvent
| where EventID == 4624
| where LogonType == 10
| where AccountType != "Machine" 
| where TimeGenerated between (ago(7d) .. now())
| summarize count() by Account, Computer, bin(TimeGenerated, 1h)
| where count_ > 3
```

## 3. Identificación de SMB (Server Message Block)

El abuso de SMB permite a los atacantes transferir herramientas y ejecutar comandos de forma remota (ej. vía `PsExec`).

**Indicadores clave:**

- Transferencias de archivos inusuales hacia recursos compartidos (`\\share`) desde equipos no autorizados.
    
- Conexiones SMB masivas a múltiples hosts en un periodo corto de tiempo (escaneo de red).
    
- Uso de utilidades administrativas como `psexec.exe`, `smbclient` o la creación remota de servicios a través de SMB.
    
- Acceso a archivos sensibles o directorios restringidos por cuentas que no pertenecen a dichos grupos de acceso.
    

**Consulta de detección (Hunting Query - KQL):**

Fragmento de código

```kql
DeviceNetworkEvents
| where RemotePort == 445
| summarize connections = count() by DeviceId, RemoteIP, bin(TimeGenerated, 1h)
| where connections > 10
```

## 4. Identificación de Pass-the-Hash (PtH)

Técnica donde el atacante utiliza el hash de una contraseña para autenticarse, evadiendo la necesidad del texto plano.

**Indicadores clave:**

- Autenticaciones NTLM inusuales entre hosts (EventID 4776 o 4624 con `AuthenticationPackage` = "NTLM").
    
- Uso de una misma cuenta privilegiada desde múltiples hosts en un tiempo reducido sin cambios de contraseña.
    
- Detección de herramientas de volcado de credenciales (ej. _Mimikatz_) y accesos anómalos al proceso `lsass.exe`.
    
- Creación de sesiones remotas con credenciales reutilizadas evidenciadas por el origen del inicio de sesión.
    

**Consulta de detección (Hunting Query - KQL):**

Fragmento de código

```kql
SecurityEvent
| where EventID in (4624, 4776)
| where AuthenticationPackage == "NTLM"
| summarize dcount(Computer) by AccountName, bin(TimeGenerated, 1d)
| where dcount_Computer > 3
```

## 5. Artefactos y Evidencia Forense

La validación de estas amenazas requiere la búsqueda de los siguientes elementos en los hosts afectados:

- **Dumps de memoria:** Presencia de volcados de `LSASS` o ficheros creados por herramientas de dumping en directorios temporales.
    
- **Tickets de Autenticación:** Tickets NTLM/Kerberos malformados o evidencia de reutilización de tickets (_Pass-the-Ticket_).
    
- **Historial de Cuentas:** Análisis de los últimos hosts donde la cuenta se ha autenticado para identificar saltos laterales.
    

## 6. Mapeo de Campos de Eventos (Estandarización)

Para el análisis profundo y la creación de reglas en el SIEM, es fundamental normalizar los siguientes campos según el modelo de datos de la captura:

|**Campo**|**Descripción Técnica**|
|---|---|
|**EventID**|Identificador del evento Windows (ej. 4624, 4625, 4776).|
|**LogonType**|Tipo de inicio de sesión (ej. 10 = RDP, 3 = Red).|
|**AccountName / Domain**|Identidad del usuario y su dominio de origen.|
|**ProcessCommandLine**|Línea de comandos completa ejecutada (crítico para detectar SMB/PsExec).|
|**ParentProcessId**|Identificador del proceso padre para rastrear el origen de la ejecución.|
|**RemoteIP / Port**|Dirección de origen y puerto de destino (ej. 445 para SMB, 3389 para RDP).|
|**AuthenticationPackage**|Protocolo utilizado (NTLM vs Kerberos).|

> [!abstract]- 🕵️‍♂️ Técnica 1: RDP (Remote Desktop Protocol)
> **Vector:** Conexión Remota Anómala
> **Campos Críticos:** `EventID 4624`, `LogonType 10`
> 
> **Indicadores de Alerta:**
> - Nuevas conexiones desde hosts anómalos o Internet.
> - Múltiples intentos fallidos seguidos de éxito (Brute Force).
> 
> **Query KQL:**
> ```kql
> SecurityEvent
> | where EventID == 4624
> | where LogonType == 10
> | where AccountType != "Machine" 
> | where TimeGenerated between (ago(7d) .. now())
> | summarize count() by Account, Computer, bin(TimeGenerated, 1h)
> | where count_ > 3
> ```

> [!warning]- 📂 Técnica 2: SMB / PsExec
> **Vector:** Transferencia de archivos y ejecución remota
> **Campos Críticos:** `Puerto TCP 445`, `ProcessCommandLine`
> 
> **Indicadores de Alerta:**
> - Transferencias inusuales hacia `\\share`.
> - Conexiones masivas a múltiples hosts en poco tiempo.
> 
> **Query KQL:**
> ```kql
> DeviceNetworkEvents
> | where RemotePort == 445
> | summarize connections = count() by DeviceId, RemoteIP, bin(TimeGenerated, 1h)
> | where connections > 10
> ```

> [!danger]- 🔑 Técnica 3: Pass-the-Hash (PtH)
> **Vector:** Reutilización de credenciales robadas
> **Campos Críticos:** `AuthenticationPackage NTLM`, `EventID 4776 / 4624`
> 
> **Indicadores de Alerta:**
> - Autenticaciones NTLM inusuales entre hosts.
> - Misma cuenta privilegiada saltando entre múltiples hosts rápidamente.
> 
> **Query KQL:**
> ```kql
> SecurityEvent
> | where EventID in (4624, 4776)
> | where AuthenticationPackage == "NTLM"
> | summarize dcount(Computer) by AccountName, bin(TimeGenerated, 1d)
> | where dcount_Computer > 3
> ```
---

### Referencias Externas

- [Microsoft: Security Event ID 4624 - An account was successfully logged on](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624)
    
- [MITRE ATT&CK: Remote Desktop Protocol (T1021.001)](https://attack.mitre.org/techniques/T1021/001/)
    
- [MITRE ATT&CK: SMB/Windows Admin Shares (T1021.002)](https://attack.mitre.org/techniques/T1021/002/)
    
- [MITRE ATT&CK: Pass the Hash (T1550.002)](https://attack.mitre.org/techniques/T1550/002/)
    

### Documentación Relacionada

[[Técnicas de persistencia y ejecución en endpoints]]