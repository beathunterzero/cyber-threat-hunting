## 1. Definición y Concepto Operativo

El **Threat Hunting** es la práctica **proactiva** de buscar amenazas que han evadido las soluciones de seguridad tradicionales y ya se encuentran dentro del entorno. A diferencia del monitoreo convencional, no es reactivo; es una actividad estratégica y analítica basada en la formulación de **hipótesis**.

- **Premisa Fundamental:** No se espera la generación de una alerta; el cazador toma la iniciativa para localizar al atacante antes de que ejecute su objetivo final (**Assume Breach**).
    

## 2. Justificación Estratégica

Las defensas tradicionales (AV, Firewalls, IDS basados en firmas) resultan insuficientes ante adversarios modernos que emplean técnicas avanzadas para permanecer ocultos:

- **LOLBins (Living off the Land Binaries):** Uso de herramientas legítimas del sistema (como `powershell.exe`, `certutil.exe` o `wmic.exe`) para actividades maliciosas, evitando alarmas por software desconocido.
    
- **Movimiento Lateral:** Desplazamiento interno entre sistemas para ganar privilegios o localizar datos críticos sin disparar alertas perimetrales.
    
- **Evasión de Firmas:** Técnicas de ofuscación y malware polimórfico que evitan la detección estática de los antivirus tradicionales.
    
- **Persistencia Silenciosa:** Ocultamiento en procesos normales, servicios o tareas programadas para maximizar el **Dwell Time** (tiempo de permanencia del atacante en la red).
    

## 3. Características Clave del Hunter

Para que una cacería sea efectiva, debe poseer los siguientes atributos:

1. **Proactividad:** El analista inicia la búsqueda sin indicios previos o alertas confirmadas de compromiso.
    
2. **Basado en Hipótesis:** Cada proceso parte de una suposición fundamentada (ej. _"Si un atacante ha logrado persistencia, debe haber creado un servicio o tarea programada de reciente creación"_).
    
3. **Iterativo:** El proceso es un ciclo continuo que genera nuevas detecciones, reglas de alerta y conocimiento acumulativo.
    
4. **Centrado en Comportamiento:** Prioriza la identificación de **TTPs** (Tácticas, Técnicas y Procedimientos) sobre los simples indicadores de compromiso (IoCs) que son fácilmente alterables por el atacante.
    

## 4. Diferenciación Funcional (¿Qué NO es Threat Hunting?)

Es fundamental distinguir esta disciplina de otras áreas operativas del SOC para no desvirtuar su propósito:

- **No es Monitoreo de Alertas:** Responder a lo que el SIEM ya detectó es tarea del SOC Nivel 1.
    
- **No es Respuesta a Incidentes (IR):** El IR comienza una vez que la amenaza ha sido confirmada; el hunting es el paso previo que descubre dicha amenaza.
    
- **No es Análisis Forense:** El forense suele ser _post-mortem_ (después del incidente); el hunting ocurre mientras el atacante está activo.
    
- **No es revisión de logs sin propósito:** Requiere un objetivo analítico claro, una metodología y una hipótesis que guíe la búsqueda.
    

## 5. El Ciclo del Threat Hunting (Modelo SANS)

Para asegurar que una cacería sea sistemática y genere valor real al SOC, adoptamos el modelo de 6 etapas propuesto por SANS, el cual define un flujo iterativo desde la idea hasta la automatización.

1. **Propósito e Hipótesis (Purpose):**
    
    - Se define el "qué" y el "por qué". Se establece una hipótesis basada en TTPs, inteligencia de amenazas (CTI) o vectores de ataque críticos para la organización.
        
2. **Alcance y Contexto (Scope):**
    
    - Se delimita el entorno a investigar (ej. Servidores críticos de la red DMZ, endpoints del departamento financiero). Se define el periodo de tiempo y los activos involucrados.
        
3. **Herramientas y Datos (Tooling/Data):**
    
    - Identificación de las fuentes de datos necesarias (Sysmon, Windows Event Logs, logs de Red) y preparación de las herramientas de consulta (**Elastic Security**, **Velociraptor**).
        
4. **Investigación y Cacería (Investigation):**
    
    - Ejecución técnica de la búsqueda. Se analizan los datos en busca de patrones que confirmen o descarten la hipótesis planteada.
        
5. **Hallazgos (Findings):**
    
    - Documentación de lo descubierto. Se separan los falsos positivos de las actividades sospechosas o maliciosas confirmadas. Se extraen conclusiones tácticas.
        
6. **Automatización e Ingeniería de Detección (Automation):**
    
    - **La fase más crítica:** El conocimiento adquirido se convierte en una alerta automática en el SIEM. La cacería manual se transforma en detección continua para que el SOC no tenga que buscar lo mismo dos veces.

## 6. Comparativa: Monitoreo Tradicional vs. Threat Hunting

Para entender el valor del Hunter en el SOC, es crucial contrastar el enfoque reactivo frente al proactivo:

|**Característica**|**Monitoreo Tradicional (Reactivo)**|**Threat Hunting (Proactivo)**|
|---|---|---|
|**Punto de Partida**|Una alerta generada por el sistema.|Una hipótesis generada por el analista.|
|**Naturaleza**|Orientado a incidentes conocidos.|Orientado a lo desconocido/evasivo.|
|**Objetivo Primario**|Contención y resolución.|Descubrimiento y maduración de la detección.|
|**Fuentes**|Firmas e indicadores estáticos (IoCs).|Comportamientos, TTPs y anomalías.|
|**Resultado**|Cierre del ticket.|Nuevas reglas de detección y mejora de visibilidad.|

---

### Referencias Externas

- MITRE ATT&CK® Matrix
    
- The Threat Hunting Project
    
- Sigma HQ - Generic Signature Format
    

### Documentación Relacionada

[[02 - Telemetría, capacidades y objetivos del Hunter]]
[[03 - Fuente de datos esenciales para Threat Hunting]]
[[04 - Threat Hunting basado en IoCs (IoC-Driven)]]
[[05 - Threat Hunting basado en Hipótesis (Hypothesis-Driven)]]
[[06 - Threat Hunting basado en Analítica (Analytics-Driven)]]
[[07 - MITRE ATT&CK como guía de CTH]]
[[08 - Cyber Kill Chain como guía de CTH]]
[[09 - Modelo Diamante como guía de CTH]]
[[10 - Hipótesis y casos de usos comunes]]
[[11 - Preparación del entorno de Hunting]]
[[12 - Comparación detallada de EDR y SIEM]]
[[13 - Dataset de ataque simulado (logs y malware samples controlados)]]
[[01 - Creación de elastic-security-lab]]
