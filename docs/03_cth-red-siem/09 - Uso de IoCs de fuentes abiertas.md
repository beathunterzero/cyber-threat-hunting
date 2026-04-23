## 1. Definición y Propósito

El uso de **IoCs (Indicators of Compromise)** de fuentes abiertas consiste en aprovechar inteligencia pública —como direcciones IP maliciosas, dominios sospechosos o hashes de archivos (MD5/SHA256)— para realizar búsquedas retrospectivas o en tiempo real dentro de los registros del SIEM. El objetivo es identificar coincidencias que confirmen la presencia de actividad hostil conocida dentro de la infraestructura.

---

## 2. Modelo de Madurez en el uso de IoCs

La efectividad de los IoCs depende de cómo se integran en el flujo de trabajo. No es lo mismo una búsqueda manual que una integración con Machine Learning.

|**Nivel**|**Etapa de Madurez**|**Descripción Técnica y Operativa**|
|---|---|---|
|**1**|**Nivel Inicial**|Uso de IoCs básicos (hashes, IPs, dominios) extraídos directamente de _feeds_ públicos. La búsqueda suele ser manual o mediante reglas simples de coincidencia exacta.|
|**2**|**Contextualización**|Los IoCs se filtran según el entorno propio. Se analiza qué indicadores aplican realmente a la tecnología de la organización y qué hosts específicos podrían estar en riesgo.|
|**3**|**Hipótesis Proactiva**|Los IoCs dejan de ser solo reactivos. Se utilizan como "pistas" iniciales para formular hipótesis de caza más complejas, buscando comportamientos asociados a esos indicadores.|
|**4**|**Integración Avanzada**|Los IoCs alimentan reglas de correlación automática, enriquecimiento de logs en tiempo real y modelos de **Machine Learning** para detectar desviaciones de comportamiento.|

---

## 3. La Pirámide del Dolor (Contexto Técnico)

En el uso de IoCs de fuentes abiertas, es vital recordar que los indicadores de nivel inicial (Hashes e IPs) son los más fáciles de obtener, pero también los que el atacante cambia con mayor facilidad.

- **Hashes/IPs:** Bajo valor (el atacante los cambia en segundos).
    
- **Nombres de Dominio:** Valor medio.
    
- **TTPs (Tácticas, Técnicas y Procedimientos):** Alto valor (lo que realmente buscamos en niveles de madurez 3 y 4).
    

---

## 4. Fuentes Comunes de IoCs Abiertos (OSINT)

Para alimentar tu SIEM o EDR en el laboratorio, puedes considerar estas fuentes:

- **AlienVault OTX:** Repositorio masivo de pulsos de amenazas.
    
- **Abuse.ch (URLhaus / MalwareBazaar):** Enfoque en malware activo y URLs de distribución.
    
- **MISP Project:** Plataforma para compartir inteligencia de amenazas de forma estructurada.
    

---

### Referencias Externas

- [The Pyramid of Pain - David Bianco](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
    
- [CISA: Understanding Indicators of Compromise](https://www.google.com/search?q=https://www.cisa.gov/news-events/news/understanding-indicators-compromise)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[08 - Integración con CTI]]
[[10 - Convertir inteligencia en hipótesis de hunting]]