## 1. Definición y Propósito

El **DNS Tunneling** es una técnica avanzada de evasión en la que los atacantes ocultan datos o comandos dentro del tráfico DNS, utilizando consultas y respuestas aparentemente legítimas para comunicarse con un servidor externo (C2). Dado que el tráfico DNS rara vez es bloqueado por los firewalls perimetrales, se convierte en un canal ideal tanto para el Comando y Control como para la exfiltración silenciosa.

## 2. Vectores de Detección e Infraestructura

El análisis de este comportamiento se divide en cuatro enfoques analíticos desde la perspectiva de la resolución de nombres y la visibilidad del dominio:

### **1. DNS Tunneling detectado por sensores DNS / Infoblox**

- **Análisis de Entropía:** Monitorear consultas DNS con etiquetas inusualmente largas o con alta entropía en los nombres de dominio (el campo `qname`).
    
- **Tasa de Frecuencia:** Analizar la tasa de consultas por host hacia dominios poco vistos, infrecuentes o de reciente creación.
    
- **Registros de Carga Útil:** Verificar las respuestas que incluyen recursos `TXT` u otros tipos de registro atípicos, ya que son los más utilizados para transportar comandos o datos codificados desde y hacia el atacante.
    

### **2. HTTPS sospechoso desde la óptica del DNS y visibilidad de dominio**

- **Correlación TLS/DNS:** Usar el servicio de DNS para correlacionar los dominios consultados con los dominios de destino en el tráfico TLS. Si un host consulta repetidamente un dominio que luego utiliza para establecer una sesión HTTPS prolongada o atípica, puede ser un fuerte indicio de balizamiento (_beaconing_).
    
- **Análisis de Reputación:** Utilizar inteligencia de reputación de dominios. Si el dominio de destino consultado tiene mala reputación, se deben alertar e interceptar inmediatamente las conexiones HTTPS asociadas a él.
    

### **3. Detección de uso de Tor (Infraestructura de resolución)**

El enrutamiento cebolla (Tor) se utiliza para anonimizar el C2. Su detección a nivel DNS implica:

- **Resolución hacia Nodos:** Identificar resoluciones DNS hacia nodos de Tor (por ejemplo, dominios `.onion` o direcciones IP conocidas de salida de Tor) cruzando la telemetría con listas públicas de _exit nodes_.
    
- **Consultas Inversas:** Monitorizar consultas DNS inversas o directas que correspondan inequívocamente a IPs de la red Tor.
    
- **Prevención en el Resolver:** Configurar bloqueos o alertas directamente en el resolver DNS corporativo para cualquier dominio relacionado con Tor o sus nodos de salida.
    

### **4. Casos de Uso: ¿Qué describe Infoblox Threat Protection?**

Herramientas corporativas de seguridad DNS como Infoblox operan bajo premisas de comportamiento automatizado:

- **Reglas de Umbral:** Detectan la exfiltración de datos mediante reglas que observan paquetes DNS buscando tamaños atípicos y frecuencias de consulta inusuales.
    
- **Bloqueo Dinámico:** Si un host excede ciertos umbrales volumétricos en sus consultas DNS (indicativo de fuga de datos o _tunneling_ masivo), el sistema bloquea temporalmente la comunicación para aislar la amenaza.
    

---

### Referencias Externas

- [MITRE ATT&CK: Application Layer Protocol: DNS (T1071.004)](https://attack.mitre.org/techniques/T1071/004/)
    
- [MITRE ATT&CK: Protocol Tunneling (T1572)](https://attack.mitre.org/techniques/T1572/)
    
- [MITRE ATT&CK: Proxy: Multi-hop Proxy / Tor (T1090.003)](https://attack.mitre.org/techniques/T1090/003/)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[03 - Detección de beaconing y tráfico anómalo]]