## 1. Definición del Concepto

Convertir inteligencia en hipótesis significa transformar la **Inteligencia de Amenazas (CTI)** bruta (tácticas, técnicas, procedimientos o IoCs) en suposiciones lógicas y verificables dentro de tu infraestructura. No es una adivinanza, sino una predicción informada basada en el comportamiento observado de los adversarios.

---

## 2. El Proceso de 5 Pasos

|**Paso**|**Fase**|**Descripción Operativa**|
|---|---|---|
|**1**|**Preparación y Recolección de Inteligencia**|Reunir inteligencia de fuentes internas y externas (reportes, campañas recientes, TTPs). Se debe filtrar qué amenazas son realmente relevantes para tu industria y entorno tecnológico.|
|**2**|**Formulación de la Hipótesis**|Generar suposiciones concretas de cómo se manifestaría la amenaza en tu red. Ejemplo: _"El actor X podría usar spear-phishing para desplegar una baliza de Cobalt Strike"_.|
|**3**|**Alcance de Datos y Priorización**|Definir las fuentes de datos necesarias (Logs de red, Endpoints, DNS, etc.) y los segmentos de red a investigar. Se priorizan activos críticos (Crown Jewels) para optimizar el esfuerzo.|
|**4**|**Diseño de Consultas y Ejecución**|Traducir la hipótesis a lenguaje técnico (Queries en KQL, Splunk SPL, etc.). Ejecutar búsquedas iterativas en el SIEM/EDR, ajustando parámetros según los resultados iniciales.|
|**5**|**Análisis, Feedback y Refinamiento**|Validar hallazgos, descartar falsos positivos y documentar lo descubierto. La inteligencia se retroalimenta incorporando los nuevos IoCs o patrones detectados durante la caza.|

---

## 3. De la Teoría a la Práctica (Caso de Ejemplo)

Para que tu documentación tenga sentido operativo, aquí tienes cómo se vería la transformación de un dato de CTI:

- **Inteligencia Recibida:** _"El grupo Lazarus está utilizando archivos .ISO maliciosos que contienen un LNK para ejecutar una DLL mediante regsvr32.exe"_.
    
- **Hipótesis de Hunting:** _"Si Lazarus está en mi red, veré procesos `regsvr32.exe` cargando DLLs desde rutas inusuales o siendo llamados por `explorer.exe` tras montar una imagen de disco"_.
    
- **Acción Técnica:** Diseñar una query en el EDR que busque procesos hijos de `explorer.exe` que involucren montaje de ISOs y ejecución de archivos de sistema.
    

---

## 4. Por qué es vital este proceso

Sin una hipótesis, el Threat Hunting es como buscar una aguja en un pajar sin saber si la aguja existe. Este flujo asegura que:

1. La caza esté **enfocada** (ahorro de tiempo).
    
2. La caza sea **reproducible** (mejora continua).
    
3. Se incremente la **madurez** del SOC al convertir hallazgos en detecciones automáticas.
    

---

### Referencias Externas

- [CrowdStrike: What is Threat Hunting?](https://www.crowdstrike.com/cybersecurity-101/threat-hunting/)
    
- [MITRE: TTP-Based Hypothesis Generation](https://attack.mitre.org/resources/working-with-attack/)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[08 - Integración con CTI]]
[[09 - Uso de IoCs de fuentes abiertas]]