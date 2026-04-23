## 1. Definición

La **madurez en Threat Hunting** es el nivel de desarrollo, automatización y proactividad que una organización alcanza en su capacidad para detectar amenazas ocultas que evaden los controles de seguridad tradicionales. No se trata solo de encontrar amenazas, sino de cuán eficiente, repetible y medible es ese proceso.

---

## 2. Métricas Clave de Desempeño (KPIs)

Para medir la eficacia del programa de hunting, se deben monitorear los siguientes indicadores:

|**#**|**Métrica / Indicador**|**Descripción Técnica**|**Objetivo Operativo**|
|---|---|---|---|
|**01**|**Mean Time to Detect (MTTD)**|Tiempo promedio en identificar una amenaza desde el momento en que ocurre el compromiso inicial.|Reducir el "dwell time" (tiempo de permanencia) del atacante en la red.|
|**02**|**Mean Time to Respond (MTTR)**|Tiempo promedio que toma el equipo en contener o mitigar una amenaza una vez ha sido detectada.|Minimizar el impacto y el daño colateral de una intrusión confirmada.|
|**03**|**Porcentaje de Hunts Exitosos**|Relación entre la cantidad de investigaciones que derivan en hallazgos válidos frente al total de ejecuciones.|Validar la calidad de las hipótesis y la precisión de la inteligencia utilizada.|
|**04**|**Nivel de Automatización**|Grado en que se integran herramientas SIEM/EDR y CTI para reducir el esfuerzo manual en las búsquedas.|Aumentar la escalabilidad del equipo y permitir búsquedas continuas (Nivel 5 de madurez).|
|**05**|**Ciclo de Retroalimentación**|Frecuencia con la que los hallazgos de una caza se convierten en nuevas reglas de detección, dashboards o casos de uso.|Asegurar que una amenaza detectada una vez manualmente sea detectada automáticamente siempre en el futuro.|

---

## 3. Relación entre Madurez y Valor de Negocio

A medida que las métricas mejoran, el valor del equipo de seguridad cambia:

- **Madurez Baja:** Enfoque reactivo, MTTD muy alto, dependencia total de alertas de terceros.
    
- **Madurez Alta:** Enfoque proactivo, MTTD reducido drásticamente, creación de propiedad intelectual propia (reglas y queries personalizadas).
    


---

### Referencias Externas

- [SANS Institute: Measuring the Effectiveness of Threat Hunting](https://www.google.com/search?q=https://www.sans.org/white-papers/37702/)
    
- [MITRE: TTP-Based Metrics for Detection](https://attack.mitre.org/resources/working-with-attack/)
    

### Documentación Relacionada

[[02 - Documentar hallazgos (Metodología Integral)]]
[[03 - Conversión de hunts en casos de uso para SIEM y SOAR]]
[[04 - KPIs de hunting (detecciones nuevas, reducción MTTR)]]
[[05 - Beneficios de implementar Red Team y Blue Team]]
[[01 - Filosofía y estrategia del Threat Hunting]]