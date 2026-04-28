## 1. ¿Qué se busca?

Detectar **accesos remotos y autenticaciones anómalas** que indiquen:

- Movimiento lateral
    
- Uso indebido de credenciales
    
- Acceso no autorizado
    

---

## 2. RDP (Remote Desktop)

Indicadores:

- Conexiones desde hosts no habituales
    
- Intentos fallidos seguidos de éxito
    
- **LogonType 10** (RemoteInteractive)
    
- Accesos fuera de horario
    
- Uso de cuentas no administrativas
    

---

### Ejemplo (KQL)

```kql
SecurityEvent
| where EventID == 4624
| where LogonType == 10
| where AccountType != "Machine"
| summarize count() by Account, Computer, bin(TimeGenerated, 1h)
| where count_ > 3
```

---

## 3. SMB (movimiento lateral)

Indicadores:

- Conexiones masivas a puerto 445
    
- Transferencias a `\\share` inusuales
    
- Uso de herramientas:
    
    - `psexec`
        
    - ejecución remota
        

---

### Ejemplo (KQL)

```kql
DeviceNetworkEvents
| where RemotePort == 445
| summarize connections = count() by DeviceId, RemoteIP, bin(TimeGenerated, 1h)
| where connections > 10
```

---

## 4. Pass-the-Hash (PtH)

Uso de hashes en lugar de contraseñas.

Indicadores:

- Autenticación **NTLM** inusual
    
- Misma cuenta en múltiples hosts
    
- Acceso a `lsass.exe`
    
- Herramientas como Mimikatz
    

---

### Ejemplo (KQL)

```kql
SecurityEvent
| where EventID in (4624, 4776)
| where AuthenticationPackage == "NTLM"
| summarize dcount(Computer) by AccountName, bin(TimeGenerated, 1d)
| where dcount_Computer > 3
```

---

## 5. Evidencia en endpoint

Buscar:

- Dumps de `lsass`
    
- Archivos temporales sospechosos
    
- Historial de autenticaciones
    
- Uso anómalo de cuentas
    

---

## 6. Campos clave para análisis

- `EventID` → tipo de evento
    
- `LogonType` → tipo de acceso
    
- `AccountName` → usuario
    
- `ProcessCommandLine` → comandos
    
- `ParentProcessId` → origen
    
- `RemoteIP / Port` → conexión
    
- `AuthenticationPackage` → NTLM / Kerberos
    

---

## 7. Enfoque de hunting

- Correlacionar autenticación + red
    
- Identificar uso anómalo de cuentas
    
- Detectar patrones repetitivos
    
- Validar contra baseline
    

---

## Referencias Externas

- [https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624)
    
- [https://attack.mitre.org/techniques/T1021/001/](https://attack.mitre.org/techniques/T1021/001/)
    
- [https://attack.mitre.org/techniques/T1021/002/](https://attack.mitre.org/techniques/T1021/002/)
    
- [https://attack.mitre.org/techniques/T1550/002/](https://attack.mitre.org/techniques/T1550/002/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]