## 1. Definición y Propósito

El **Threat Hunting en el SIEM** (Security Information and Event Management) es el proceso proactivo de anticipar, detectar y mitigar ataques avanzados mediante el uso de inteligencia de amenazas y la mejora continua de las capacidades de detección. A diferencia de las alertas automáticas, el hunting busca lo que aún no ha sido descubierto, utilizando la centralización de registros para identificar anomalías que pasan desapercibidas.

---

## 2. El Ciclo de Vida del Hunting en SIEM

El proceso se divide en cinco fases críticas que aseguran una investigación estructurada y resultados de alta fidelidad:

|**Fase**|**Actividad Principal**|**Descripción Técnica**|
|---|---|---|
|**1**|**Definición de Hipótesis**|Se formula una hipótesis de amenaza basada en **Inteligencia de Amenazas (CTI)**, patrones anómalos previamente observados o **Indicadores de Compromiso (IoCs)**.|
|**2**|**Agregación y Enriquecimiento de Datos**|Se centralizan y normalizan las fuentes de datos (endpoints, red, nube). Los registros se enriquecen con contexto (**Geo-IP, reputación de dominios, mapeo de MITRE ATT&CK**) para permitir un análisis contextualizado y preciso.|
|**3**|**Ejecución de Consultas y Descubrimiento de Patrones**|La hipótesis se traduce en consultas (queries) o reglas de correlación. Se busca identificar comportamientos sospechosos, secuencias de eventos inusuales y tácticas adversarias específicas.|
|**4**|**Validación y Análisis Contextual**|Los resultados se comparan con las **líneas base (baselines)** del comportamiento normal. Mediante análisis forense y contextual, se valida la legitimidad del hallazgo para reducir drásticamente los falsos positivos.|
|**5**|**Documentación y Mejora Continua**|Se documentan los hallazgos y se actualizan reglas de detección, dashboards y casos de uso. Este paso fortalece la madurez del SOC y retroalimenta el ciclo de inteligencia para futuras amenazas.|

---

## 3. Pilares de la Efectividad en el SIEM

Para que este ciclo sea exitoso, el Hunter debe priorizar tres elementos en su plataforma:

1. **Normalización (Parsing):** Asegurar que los datos de diferentes fabricantes hablen el mismo idioma (ej. ECS en Elastic o ASIM en Sentinel).
    
2. **Correlación Cruzada:** La capacidad de unir un evento de firewall con un evento de creación de proceso en el endpoint.
    
3. **Reducción de Ruido:** El objetivo de la fase de validación es asegurar que solo las anomalías reales lleguen a la fase de respuesta.
    

---

### Referencias Externas

- [MITRE ATT&CK: Design and Evaluate Threat Hunting](https://www.google.com/url?sa=E&source=gmail&q=https://mitre-attack.github.io/attack-navigator/)
    
- [SANS Institute: Generating Hypotheses for Threat Hunting](https://www.sans.org/white-papers/37172/)
    
- [Microsoft Learn: Azure Sentinel Threat Hunting](https://learn.microsoft.com/en-us/azure/sentinel/hunting)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[06 - Ejemplo de hipótesis en SIEM]]