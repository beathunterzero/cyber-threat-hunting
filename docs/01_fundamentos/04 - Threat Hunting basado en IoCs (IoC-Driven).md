## 1. Definición y Concepto

El **Threat Hunting basado en IoCs** (Indicadores de Compromiso) es un enfoque donde la cacería se dispara a partir de datos tácticos obtenidos de **Ciberinteligencia (CTI)**. Se busca evidencia de actividad maliciosa ya conocida en el entorno para determinar si el adversario ha tenido presencia histórica o actual.

## 2. Indicadores de Infraestructura y Red (Taxonomía)

Para una cacería efectiva en red, debemos clasificar los artefactos según su función dentro de la comunicación del atacante:

|**Categoría de Objeto**|**Indicadores Específicos (IoCs)**|**Valor de Caza**|
|---|---|---|
|**Certificados TLS/SSL**|Fingerprints (JA3/JA3S), Nombres de Emisor, SNI inusuales, Certificados auto-firmados.|Identifica herramientas (Cobalt Strike) e infra de C2.|
|**SSH**|Claves públicas reutilizadas, algoritmos de cifrado específicos.|Vincula diferentes campañas a un mismo actor.|
|**Dominios**|Algoritmos DGA, dominios de reciente creación, Typosquatting.|Detecta puntos de contacto de malware y phishing.|
|**Patrones DNS**|Longitud excesiva de consultas, registros TXT inusuales, alta frecuencia de peticiones.|Detecta exfiltración de datos y canales de C2 ocultos.|

## 3. Flujo Operativo del Hunt

1. **Ingesta de Inteligencia:** Recepción de reportes de CTI detallando la infraestructura del atacante.
    
2. **Extracción de Artefactos:** Identificación de certificados, claves SSH o patrones DNS específicos.
    
3. **Búsqueda Retrospectiva:** Consultas en **Kibana** sobre logs de red buscando coincidencias históricas.
    
4. **Validación y Enriquecimiento:** Verificar si el SNI o el certificado coinciden con servicios legítimos para descartar falsos positivos.
    

## 4. Limitaciones y la Pirámide del Dolor

Operamos en los niveles **Bajo y Medio** de la Pirámide:

- **Durabilidad:** Los atacantes rotan certificados y dominios con facilidad.
    
- **Evasión:** El uso de servicios legítimos (_Domain Fronting_) puede enmascarar estos indicadores.
    

## 5. Aplicación Práctica en el Lab (Consultas KQL)

- **SNI sospechoso:** `network.protocol: "tls" AND tls.server.name: /.*secure-update.*/`
    
- **DGAs (DNS):** `dns.question.name: /.{25,}/`
    
- **Huella JA3:** `tls.client.ja3_hash : "7739105ed22b10..."`
    

## 6. Clasificación de Indicadores según Obtención y Utilidad

Para priorizar la búsqueda, clasificamos los indicadores según el esfuerzo que requiere conseguirlos y su relevancia para la investigación:

|**Tipo de Indicador**|**Facilidad de Obtención**|**Utilidad para el Hunter**|
|---|---|---|
|**Fácil (Low Hanging Fruit)**|Alta (Listas públicas, feeds gratuitos)|Media/Baja (Son volátiles)|
|**Específico de la Amenaza**|Media (Reportes de CTI cerrados, análisis de malware)|Alta (Identifica campañas concretas)|
|**Generado por la Investigación**|Baja (Requiere análisis manual y forense)|Muy Alta (Es telemetría propia y única)|
|**Comportamientos (TTPs)**|Muy Baja (Requiere correlación avanzada)|Máxima (Detección duradera)|

---

### Referencias Externas

- MITRE ATT&CK® Matrix
    
- SANS Institute: Threat Hunting with Tactical Analysis
    

### Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]
[[05 - Threat Hunting basado en Hipótesis (Hypothesis-Driven)]]
[[06 - Threat Hunting basado en Analítica (Analytics-Driven)]]