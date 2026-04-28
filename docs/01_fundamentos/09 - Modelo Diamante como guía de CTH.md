## 1. ¿Qué es el Diamond Model?

El **Diamond Model** analiza intrusiones a través de la relación entre cuatro elementos:

- **Adversario**
    
- **Infraestructura**
    
- **Capacidad**
    
- **Víctima**
    

No es un modelo lineal.  
Se usa para **pivotear entre datos** y reconstruir actividad del atacante.

---

## 2. Componentes del modelo

### 2.1 Adversario

- Actor que ejecuta el ataque
    
- Ej: APTs, cibercriminales, insiders
    

Uso en hunting:

- Asociar TTPs conocidos
    
- Anticipar comportamiento
    

---

### 2.2 Infraestructura

- Medio usado por el atacante
    

Ejemplos:

- IPs
    
- Dominios
    
- Servidores C2
    
- Cloud abusado
    

Uso en hunting:

- Detección de comunicación externa
    
- Identificación de C2
    

---

### 2.3 Capacidad

- Herramientas y técnicas utilizadas
    

Ejemplos:

- Malware
    
- Scripts
    
- Frameworks (Cobalt Strike)
    

Uso en hunting:

- Identificar comportamiento repetitivo
    
- Crear detecciones
    

---

### 2.4 Víctima

- Objetivo del ataque
    

Ejemplos:

- Usuarios privilegiados
    
- Servidores críticos
    
- Bases de datos
    

Uso en hunting:

- Priorizar activos
    
- Detectar targeting
    

---

## 3. Valor del modelo

El valor está en las **relaciones**:

- Adversario ↔ Infraestructura
    
- Infraestructura ↔ Víctima
    
- Capacidad ↔ Víctima
    
- Adversario ↔ Capacidad
    

Permite:

- Conectar eventos aislados
    
- Ampliar contexto
    
- Identificar campañas completas
    

---

## 4. Uso en Threat Hunting

### Flujo básico

1. **Punto inicial**
    
    - IoC o evento sospechoso
        
2. **Pivotear**
    
    - Qué host se conecta
        
    - Qué procesos ejecuta
        
    - Qué técnica usa
        
3. **Expandir contexto**
    
    - Relacionar con actor o campaña
        
4. **Generar hipótesis**
    
    - Basada en relaciones observadas
        

---

## 5. Ejemplo práctico (KQL)

Correlación entre red (infraestructura) y procesos (capacidad):

```kql
DeviceNetworkEvents
| where RemoteIP == "X.X.X.X"
| project DeviceName, Timestamp
| join kind=inner (
    DeviceProcessEvents
    | where FileName in ("powershell.exe", "cmd.exe", "wmic.exe")
) on DeviceName
| where Timestamp1 between (Timestamp .. datetime_add('hour', 1, Timestamp))
```

---

## 6. Relación con otros frameworks

|Framework|Enfoque|Uso|
|---|---|---|
|MITRE ATT&CK|Técnicas|Qué buscar|
|Cyber Kill Chain|Fases|Cuándo detectar|
|Diamond Model|Relaciones|Cómo conectar|

---

## Referencias Externas

- [https://apps.dtic.mil/sti/pdfs/ADA586960.pdf](https://apps.dtic.mil/sti/pdfs/ADA586960.pdf)
    
- [https://www.sans.org/white-papers/35292/](https://www.sans.org/white-papers/35292/)
    
- [https://learn.microsoft.com/en-us/security/operations/incident-response-playbooks](https://learn.microsoft.com/en-us/security/operations/incident-response-playbooks)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[07 - MITRE ATT&CK como guía de CTH]]  
[[08 - Cyber Kill Chain como guía de CTH]]