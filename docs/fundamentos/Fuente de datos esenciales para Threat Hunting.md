## 1. Introducción a la Telemetría Técnica

La eficacia de una cacería de amenazas es directamente proporcional a la calidad, granularidad y confiabilidad de la telemetría disponible. Un Threat Hunter requiere visibilidad multi-capa para reconstruir el comportamiento de un adversario que intenta mimetizarse con la actividad legítima del sistema.

## 2. Logs del Sistema Operativo

Constituyen la base mínima de visibilidad, aunque su utilidad es limitada sin una configuración de auditoría avanzada.

### 2.1 Microsoft Windows (Event Logs)

- **Security (Log):** Crucial para identificar autenticaciones (**4624/4625**), uso de privilegios (**4672**) y creación de procesos (**4688**).
    
- **PowerShell (Log):** Los eventos **4103** y **4104** (Script Block Logging) son vitales para detectar scripts ofuscados y ataques _fileless_.
    
- **WMI (Log):** Eventos **5857/5858** para identificar persistencia y ejecución mediante el instrumental de administración.
    

### 2.2 Linux (Logs de Sistema)

- **auth.log / secure:** Monitorización de intentos de acceso SSH y escalada de privilegios (sudo).
    
- **bash_history:** Registro de comandos ejecutados (aunque fácilmente manipulable por el atacante).
    
- **auditd:** Proporciona un nivel de detalle superior sobre llamadas al sistema y acceso a archivos.
    

## 3. Sysmon (System Monitor)

Herramienta de la suite Sysinternals que transforma la visibilidad del endpoint mediante telemetría detallada de eventos de alta fidelidad.

- **Event ID 1 (Process Creation):** Incluye el hash del archivo y la línea de comandos completa.
    
- **Event ID 3 (Network Connection):** Vincula procesos específicos con destinos de red.
    
- **Event ID 7 (Image Loaded):** Identifica la carga de DLLs sospechosas (DLL Hijacking/Injection).
    
- **Event ID 11 (File Create):** Monitoriza la creación de artefactos maliciosos en directorios sensibles.
    
- **Event ID 22 (DNS Query):** Registro de resoluciones de dominio directamente desde el proceso origen.
    

## 4. EDR (Endpoint Detection & Response)

Representa la fuente de datos más rica y dinámica. Herramientas como **Microsoft Defender for Endpoint**, **CrowdStrike** o **Velociraptor** actúan como sensores avanzados en tiempo real.

- **Capacidades:** Construcción de árboles de procesos, análisis de comportamiento de memoria y generación de **IOAs** (Indicadores de Ataque).
    
- **Hunting:** Permite detectar el uso de **LOLBins**, inyección de código y movimientos laterales antes de que se consoliden en el sistema.
    

## 5. SIEM (Security Information and Event Management)

El SIEM (Elastic Stack, Splunk, Sentinel) actúa como el repositorio centralizado donde ocurre la correlación de datos de diversas fuentes.

- **Función en CTH:** Ejecución de queries complejas de larga duración, análisis estadístico (apilamiento o _stacking_) y visualización de patrones de ataque distribuidos en múltiples hosts de la infraestructura.
    

## 6. Telemetría de Red

Fuente de verdad irrefutable. Si el atacante compromete el endpoint, la comunicación hacia el exterior sigue siendo detectable en los flujos de red.

- **DNS Logs:** Identificación de **DNS Tunneling** y dominios de reciente creación.
    
- **Proxy/Web Logs:** Análisis de User-Agents inusuales y conexiones a infraestructuras C2.
    
- **NetFlow:** Detección de **Beaconing** mediante el análisis de la frecuencia y el volumen de las conexiones entre hosts internos y externos.
    

## 7. Matriz de Cobertura de Hunting

|**Fuente de Datos**|**Nivel de Visibilidad**|**Principal Caso de Uso**|
|---|---|---|
|**OS Logs**|Básico|Auditoría de acceso y servicios.|
|**Sysmon**|Alto|Visibilidad técnica profunda del proceso.|
|**EDR**|Crítico|Detección de comportamiento y respuesta.|
|**Network**|Crítico|Detección de C2 y Exfiltración.|
|**SIEM**|Estratégico|Correlación y análisis histórico.|

---

### Referencias Externas

- [Microsoft: Sysmon Documentation and Event IDs](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    
- [NSA: Spotting the Adversary with Windows Event Log Monitoring](https://www.google.com/search?q=https://www.nsa.gov/Portals/70/documents/what-we-do/cybersecurity/professional-resources/csf-windows-event-log-monitoring-guidance.pdf)
    
- [SANS Institute: Network Intrusion Detection with NetFlow](https://www.sans.org/white-papers/33314/)
    
- [Splunk: Threat Hunting with EDR Telemetry](https://www.google.com/search?q=https://www.splunk.com/en_us/blog/security/threat-hunting-with-edr.html)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]