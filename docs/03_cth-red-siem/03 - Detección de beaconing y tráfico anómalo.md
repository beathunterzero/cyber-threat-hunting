## 1. Definición y Propósito

**Beaconing** se refiere a comunicaciones periódicas o repetitivas (frecuentemente llamadas "heartbeat" o latidos) establecidas desde un _host_ comprometido hacia un servidor de Comando y Control (C2). Es detectable a través del análisis de patrones temporales, la repetición de destinos y las características del flujo de red (tamaño, temporización, proporción de bytes e intervalos).

Dado que un adversario frecuentemente intentará mezclar el _beaconing_ con el tráfico legítimo de la red (como tráfico HTTPS normal o llamadas a servicios en la nube), la estrategia defensiva eficaz exige la combinación de señales de red con la telemetría de procesos y DNS en el endpoint.

## 2. Señales e Indicadores (Prioridad de Caza)

La identificación de tráfico anómalo debe enfocarse en dos frentes de recolección de datos que revelen los siguientes patrones:

|**Categoria de Anomalía**|**Indicador Técnico Detallado**|
|---|---|
|**Patrones Temporales**|**Periodicidad fuerte:** Conexiones de salida (_egress_) con intervalos de tiempo muy regulares (ej. exactamente cada N minutos) dirigidas hacia la misma IP, _hostname_ o _endpoint_.|
|**Análisis de Payload**|**Baja entropía en payloads repetidos:** Peticiones (_requests_) en la red donde los cuerpos (_bodies_) o los parámetros se mantienen muy similares, lo cual es un fuerte indicador de _beaconing_ codificado.|
|**Volumen de Datos**|**Proporción de bytes egress/ingress anómala:** Hosts que presentan un volumen de tráfico de salida (_egress_) constante o sostenido, pero un tráfico de entrada (_ingress_) muy bajo, sugiriendo una posible exfiltración continua.|
|**Anomalías de DNS**|**Dominios con subdominios largos/aleatorios:** Consultas DNS con etiquetas (_labels_) inusuales y con alta entropía, lo cual es característico de técnicas de _DNS tunneling_.|
|**Destinos Sospechosos**|**Conexiones a destinos no habituales o de anonimato:** Comunicaciones dirigidas a la red Tor, IPs con baja reputación, dominios recién creados o países sin justificación operativa para el negocio.|
|**Actividad del Endpoint**|**Concurrencia de señales del endpoint:** Procesos locales que generan conexiones periódicas o que realizan llamadas a bibliotecas de red poco habituales para su contexto normal de ejecución.|

## 3. Métricas y Técnicas Analíticas Útiles

Para automatizar la caza de estas amenazas de forma eficaz en plataformas EDR o SIEM (como Elastic), se aplican modelos estadísticos y matemáticos:

- **Análisis de Periodicidad (FFT / Dominio de la Frecuencia / Autocorrelación):** Utilizada para convertir series temporales de conexiones en picos de periodicidad. Esta técnica es fundamental para detectar _beaconing_ del tipo "low-noise" (bajo ruido), donde el atacante introduce _jitter_ (variación aleatoria) para ofuscar el intervalo de conexión.
    
- **Historial por Host (Cálculo de Baseline):** Establecimiento del patrón normal de comportamiento del host (frecuencias y destinos comunes) y detección de valores atípicos (_outliers_) a través de la aplicación de _z-score_ o modelos de aprendizaje automático de clase única (_one-class models_).
    
- **Agrupación y Cálculo de Intervalos:** Se utiliza la agrupación de logs a través de las claves `(dest_ip, dest_port, user_agent, hostname)` y se calcula el tiempo exacto entre los eventos. El objetivo de la consulta (_query_) es buscar consistencia en los intervalos entre las balizas (_inter-beacon intervals_). _(Enfoque nativo en plataformas como Elastic)_.
    
- **Análisis de Entropía en Strings:** Evaluación profunda de subdominios y rutas en las URIs para detectar etiquetas generadas de forma algorítmica o datos codificados para exfiltración (ej. formatos _Base32_ o _Base64_).
    

---

### Referencias Externas

- [MITRE ATT&CK: Application Layer Protocol - Web Protocols (T1071.001)](https://attack.mitre.org/techniques/T1071/001/)
    
- [MITRE ATT&CK: Dynamic Resolution - Fast Flux DNS (T1568.001)](https://attack.mitre.org/techniques/T1568/001/)
    
- [Elastic Security Labs: Detecting Beaconing with KQL](https://www.elastic.co/security-labs)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[04 - DNS tunneling, HTTPs sospechoso y uso de Tor]]