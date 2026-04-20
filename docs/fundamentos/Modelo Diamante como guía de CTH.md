## 1. Definición y Enfoque Relacional

El **Diamond Model of Intrusion Analysis** es un marco conceptual que analiza eventos de seguridad mediante la interconexión de cuatro elementos fundamentales: **Adversario, Infraestructura, Capacidad y Víctima**. A diferencia de otros modelos, el Diamante no es lineal ni técnico-específico, sino **relacional**, permitiendo al hunter pivotear entre datos aislados para reconstruir una campaña completa.

## 2. Los Cuatro Vértices del Diamante

### 2.1 Adversary (Adversario)

Representa al actor responsable del ataque.

- **Perfiles:** APT (ej. APT29), cibercriminales (ej. FIN7), insiders o hacktivistas.
    
- **Uso en CTH:** Mapeo de TTPs conocidos y predicción de comportamientos futuros basados en inteligencia de amenazas (CTI).
    

### 2.2 Infrastructure (Infraestructura)

El medio lógico o físico que el adversario emplea para interactuar con la víctima.

- **Componentes:** Servidores C2, dominios, direcciones IP, servicios Cloud abusados, infraestructuras _Fast-Flux_.
    
- **Uso en CTH:** Ejecución de hunts orientados a red y detección de actividad de mando y control mediante telemetría de tráfico.
    

### 2.3 Capability (Capacidad)

Herramientas, malware o técnicas tácticas que el adversario despliega.

- **Recursos:** Frameworks (Cobalt Strike), scripts, malware (LockBit), o técnicas de explotación de vulnerabilidades.
    
- **Uso en CTH:** Identificación de patrones repetitivos en el endpoint y creación de detecciones basadas en el comportamiento del artefacto.
    

### 2.4 Victim (Víctima)

El objetivo del ataque, definido por el sector, geografía o activos específicos.

- **Entidades:** Usuarios con privilegios, bases de datos críticas, servidores de dominio o infraestructura OT.
    
- **Uso en CTH:** Priorización de jornadas de caza basadas en el valor del activo y detección de patrones de "Targeting".
    

## 3. Dinámica de Pivoteo y Relaciones

El valor operativo reside en las aristas que conectan los vértices:

- **Adversario ↔ Infraestructura:** Identificación de recursos recurrentes de un actor.
    
- **Infraestructura ↔ Víctima:** Correlación de hosts internos con centros de mando externos.
    
- **Capacidad ↔ Víctima:** Análisis del impacto técnico en activos específicos.
    
- **Adversario ↔ Capacidad:** Vinculación de herramientas con firmas de comportamiento características de un grupo.
    

## 4. Implementación en el Proceso de Hunting

### 4.1 Metodología de Pivoteo

1. **Vértice Inicial:** Se identifica un IoC (ej. un dominio sospechoso en la Infraestructura).
    
2. **Expansión:** Se analiza qué víctimas se conectaron a ese dominio y qué capacidades (procesos/scripts) se ejecutaron tras la conexión.
    
3. **Hipótesis:** _"Si el dominio detectado pertenece a la infraestructura de FIN7, identificaremos el uso de herramientas de escalada de privilegios en los hosts afectados"_.
    

### 4.2 Ejemplo de Aplicación Técnica (KQL)

Búsqueda de procesos hijos anómalos (Capacidad) en hosts que han interactuado con IPs sospechosas (Infraestructura):

Fragmento de código

```kql
DeviceNetworkEvents
| where RemoteIP == "X.X.X.X" // IP identificada como Infraestructura
| project DeviceName, Timestamp
| join kind=inner (
    DeviceProcessEvents
    | where FileName in ("powershell.exe", "cmd.exe", "wmic.exe")
) on DeviceName
| where Timestamp1 between (Timestamp .. datetime_add('hour', 1, Timestamp))
```

## 5. Comparativa de Frameworks Estratégicos

|**Framework**|**Enfoque Principal**|**Aplicación en Hunting**|
|---|---|---|
|**MITRE ATT&CK**|Técnicas y Tácticas|**Qué** buscar (comportamiento técnico).|
|**Cyber Kill Chain**|Fases temporales|**Cuándo** intervenir (etapa del ataque).|
|**Diamond Model**|Relaciones|**Cómo** se conecta el evento con el actor.|

---

### Referencias Externas

- [The Diamond Model of Intrusion Analysis (Original Paper)](https://apps.dtic.mil/sti/pdfs/ADA586960.pdf)
    
- [SANS Institute: Intrusión Analysis with the Diamond Model](https://www.google.com/search?q=https://www.sans.org/white-papers/35292/)
    
- [Microsoft: Tracking threat actors with the Diamond Model](https://www.microsoft.com/en-us/security/blog/)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]
[[MITRE ATT&CK como guía de CTH]]
[[Cyber Kill Chain como guía de CTH]]