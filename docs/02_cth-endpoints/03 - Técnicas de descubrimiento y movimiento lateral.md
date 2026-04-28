## 1. ¿Qué se busca?

Detectar cómo el atacante:

- **Reconoce el entorno**
    
- **Identifica objetivos**
    
- **Se mueve dentro de la red**
    

Problema:

- Estas acciones se parecen a actividad administrativa legítima
    

Clave:

- Detectar **desviaciones del comportamiento normal**
    

---

## 2. Etapas típicas

|Nivel|Técnica|Indicadores|
|---|---|---|
|1|Descubrimiento de red|Escaneos, conexiones a múltiples puertos|
|2|Enumeración|Consultas masivas a AD, SMB, LDAP|
|3|Credenciales|Accesos fuera de horario, uso de hashes|
|4|Servicios remotos|RDP/WinRM inusual|
|5|Ejecución remota|PsExec, servicios remotos|
|6|WMI / Tasks|WMI anómalo, tareas nuevas|

---

## 3. Comandos comunes (LOLBins)

Indicadores de reconocimiento cuando aparecen en secuencia:

- `whoami /all`
    
- `net user /domain`
    
- `net group "Domain Admins" /domain`
    
- `nltest /dclist:`
    
- `ipconfig /all`
    
- `arp -a`
    

---

## 4. Indicadores clave

- Múltiples conexiones a:
    
    - 135 / 137 / 139 / 445
        
- Autenticaciones:
    
    - fuera de horario
        
    - desde hosts inusuales
        
- Movimiento lateral:
    
    - Workstation → Workstation
        
- Ejecución remota:
    
    - PowerShell remoting
        
    - PsExec
        
    - WMI
        

---

## 5. Estrategia de hunting

### 5.1 Contexto de ejecución

- Comandos administrativos son normales
    
- El problema es:
    
    - quién los ejecuta
        
    - desde dónde
        
    - en qué contexto
        

Ejemplo sospechoso:

- `winword.exe` → `cmd.exe` → `net user`
    

---

### 5.2 Análisis de red

- Definir baseline de RDP / SMB
    
- Detectar nuevas relaciones entre hosts
    
- Priorizar tráfico lateral no habitual
    

---

## 6. Objetivo del hunting

- Detectar expansión del atacante
    
- Identificar uso de credenciales
    
- Frenar movimiento lateral antes de impacto
    

---

## Referencias Externas

- [https://attack.mitre.org/tactics/TA0007/](https://attack.mitre.org/tactics/TA0007/)
    
- [https://attack.mitre.org/tactics/TA0008/](https://attack.mitre.org/tactics/TA0008/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]