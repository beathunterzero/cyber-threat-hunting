## 1. ¿Qué se busca?

Detectar **uso, abuso o escalamiento de privilegios** fuera de lo normal.

Objetivo:

- Identificar accesos indebidos
    
- Detectar elevaciones no autorizadas
    
- Analizar comportamiento de cuentas privilegiadas
    

---

## 2. Enfoque de análisis

### 2.1 Desviaciones de privilegios

- Definir baseline por usuario/grupo
    
- Detectar cambios no esperados
    

Indicadores:

- Usuario estándar → privilegios altos
    
- Cambios en grupos críticos
    

Eventos clave:

- 4672 (privilegios especiales)
    
- 4728 / 4732 (agregado a grupos)
    

---

### 2.2 Manipulación de tokens

Uso de privilegios para suplantar identidad.

Indicadores:

- Uso de:
    
    - `SeDebugPrivilege`
        
    - `SeImpersonatePrivilege`
        
- Acceso a procesos sensibles
    

Eventos:

- Sysmon 10 (Process Access)
    

---

### 2.3 Uso de cuentas privilegiadas

Analizar:

- Cuándo se usan
    
- Desde dónde
    
- Qué ejecutan
    

Patrón crítico:

> Cuenta privilegiada + horario inusual + comando administrativo

Herramientas comunes:

- `net user`
    
- `wmic`
    
- `psexec`
    
- `powershell`
    

---

### 2.4 Persistencia vía privilegios

Buscar rutas indirectas de escalamiento:

- Relaciones entre grupos
    
- Permisos heredados
    
- ACLs mal configuradas
    

Ejemplos:

- `GenericAll`
    
- `WriteDacl`
    

Herramienta:

- BloodHound
    

---

### 2.5 Elevación temporal

Patrón sospechoso:

- Elevar privilegios
    
- Ejecutar acción
    
- Revocar acceso
    

En ventana corta → alto riesgo

---

## 3. Indicadores clave

- Cambios en grupos privilegiados
    
- Uso de cuentas fuera de contexto
    
- Acceso a `lsass.exe`
    
- Ejecución remota con privilegios
    

---

## 4. Enfoque de hunting

- Comparar contra baseline
    
- Correlacionar autenticación + ejecución
    
- Priorizar cuentas críticas
    
- Analizar secuencias de eventos
    

---

## Referencias Externas

- [https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4672](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4672)
    
- [https://attack.mitre.org/techniques/T1134/](https://attack.mitre.org/techniques/T1134/)
    
- [https://attack.mitre.org/techniques/T1078/](https://attack.mitre.org/techniques/T1078/)
    
- [https://bloodhoundenterprise.io/](https://bloodhoundenterprise.io/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]