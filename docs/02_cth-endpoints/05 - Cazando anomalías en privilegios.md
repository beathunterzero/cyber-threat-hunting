## 1. Definición y Enfoque Técnico

El objetivo de este bloque es **identificar y analizar comportamientos inusuales relacionados con el uso, asignación o elevación de privilegios dentro de sistemas y redes.** Técnicamente, esto implica comparar la actividad actual con patrones normales para detectar escalamientos no autorizados, accesos indebidos o abusos de cuentas privilegiadas.

## 2. Marco Analítico de Caza (5 Pilares Técnicos)

Basado en el diagrama de flujo operativo del curso, la caza se estructura en cinco pilares analíticos interconectados:

### **Pilar 1: Análisis de Desviaciones en privilegios administrativos**

Este pilar se enfoca en establecer una "línea base" de lo que es normal para cada usuario o grupo y detectar escalamientos de privilegios.

- **Definir Línea Base:** Crear una línea base de privilegios normales por usuario o grupo de seguridad.
    
- **Detección de Escaladas:** Identificar elevaciones no programadas (ej. un usuario estándar que obtiene permisos de Domain Admin).
    
- **Event IDs Críticos:** Monitorear **Windows Event ID 4672** (Logon Type 3 con privilegios especiales), **4728** (Miembro añadido a grupo global) y **4732** (Miembro añadido a grupo local).
    

### **Pilar 2: Monitoreo de creación y abuso de tokens de acceso**

Se centra en la manipulación técnica de los tokens de autenticación para suplantar o duplicar identidades privilegiadas.

- **Identificación Técnica:** Detecta anomalías en la generación de tokens mediante privilegios como `SeDebugPrivilege` o `SeImpersonatePrivilege`.
    
- **Detección con Sysmon:** Utiliza **Sysmon Event ID 10** (Process access) enfocándose en la duplicación de tokens para ejecución lateral.
    

### **Pilar 3: Caza basada en comportamiento de cuentas privilegiadas**

Analiza el "cuándo" y "dónde" se usan las cuentas con altos privilegios.

> [!CAUTION] **Fórmula de Anomalía:** Cuenta privilegiada **+** actividad fuera de horario laboral habitual **+** comando administrativo **=** Prioridad de Investigación Máxima.

- **LOLBins Comunes a vigilar:** `net user`, `wmic`, `psexec`, `rundll32`, `powershell` remoto.
    

### **Pilar 4: Análisis de persistencia mediante privilegios heredados**

Investiga el uso de relaciones de confianza complejas y persistencia en grupos intermedios.

- **Auditoría de Grupos:** Audita relaciones de pertenencia transitiva (rutas de "bajo-priv a alto-priv").
    
- **Herramientas Clave:** Uso de **BloodHound** para mapear caminos transitivos.
    
- **Abuso de ACLs:** Detecta abusos de Listas de Control de Acceso, como `GenericAll` o `WriteDacl`.
    

### **Pilar 5: Correlación de privilegios temporales con eventos de ejecución**

Analiza la temporalidad de la asignación y revocación de privilegios para detectar automatización maliciosa (ej. ataques _Just-in-Time elevation_).

> [!TIP] **Regla de Caza de Oro:** La secuencia **Elevar → Ejecutar → Revocar** es altamente sospechosa si ocurre en una ventana de tiempo muy corta (≤ 5 min) y no hay justificación administrativa documentada.

---

### Referencias Externas

- [Microsoft: Security Event ID 4672 - Special privileges assigned to new logon](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4672)
    
- [MITRE ATT&CK: Access Token Manipulation (T1134)](https://attack.mitre.org/techniques/T1134/)
    
- [MITRE ATT&CK: Valid Accounts (T1078)](https://attack.mitre.org/techniques/T1078/)
    
- [BloodHound Enterprise: Attack Path Management](https://bloodhoundenterprise.io/)
    

### Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]