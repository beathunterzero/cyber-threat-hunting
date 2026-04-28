## 1. ¿Por qué es importante la telemetría?

La eficacia del Threat Hunting depende de la **calidad y cobertura de la telemetría**.

- Sin datos → no hay visibilidad
    
- Sin contexto → no hay análisis
    
- Sin correlación → no hay detección
    

El objetivo es lograr **visibilidad multi-capa** para reconstruir el comportamiento del atacante.

---

## 2. Logs del Sistema Operativo

Base mínima de visibilidad. Requiere configuración adecuada para ser útil.

### 2.1 Windows (Event Logs)

- **Security Log:**
    
    - 4624 / 4625 → autenticación
        
    - 4672 → privilegios elevados
        
    - 4688 → creación de procesos
        
- **PowerShell:**
    
    - 4103 / 4104 → ejecución de scripts
        
    - Detección de ataques _fileless_
        
- **WMI:**
    
    - 5857 / 5858 → ejecución remota y persistencia
        

---

### 2.2 Linux

- **auth.log / secure:** accesos SSH y uso de `sudo`
    
- **bash_history:** comandos ejecutados (no confiable)
    
- **auditd:** visibilidad avanzada de sistema y archivos
    

---

## 3. Sysmon

Extiende la visibilidad del endpoint con eventos de alta fidelidad.

Eventos clave:

- **Event ID 1:** creación de procesos (con hash y command line)
    
- **Event ID 3:** conexiones de red por proceso
    
- **Event ID 7:** carga de DLLs (inyección / hijacking)
    
- **Event ID 11:** creación de archivos
    
- **Event ID 22:** consultas DNS
    

---

## 4. EDR

Fuente de telemetría más completa a nivel endpoint.

Ejemplos: Defender for Endpoint, CrowdStrike, Velociraptor

Capacidades:

- Árboles de procesos
    
- Análisis de memoria
    
- Detección de comportamiento (**IOAs**)
    
- Hunting en tiempo real
    

Permite detectar:

- Uso de **LOLBins**
    
- Inyección de código
    
- Movimiento lateral
    

---

## 5. SIEM

Punto central de correlación.

Ejemplos: Elastic, Splunk, Sentinel

Funciones:

- Búsquedas complejas
    
- Correlación entre múltiples fuentes
    
- Análisis histórico
    
- Identificación de patrones distribuidos
    

---

## 6. Telemetría de Red

Fuente crítica, independiente del endpoint.

- **DNS Logs:**
    
    - DNS tunneling
        
    - dominios nuevos o sospechosos
        
- **Proxy/Web Logs:**
    
    - User-Agents anómalos
        
    - conexiones a C2
        
- **NetFlow:**
    
    - detección de **beaconing**
        
    - análisis de frecuencia y volumen de tráfico
        

---

## 7. Cobertura de Telemetría

|Fuente|Nivel|Uso principal|
|---|---|---|
|OS Logs|Básico|Accesos y auditoría|
|Sysmon|Alto|Procesos y actividad técnica|
|EDR|Crítico|Comportamiento y respuesta|
|Network|Crítico|C2 y exfiltración|
|SIEM|Estratégico|Correlación e histórico|

---

## Referencias Externas

- [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    
- [https://www.nsa.gov/Portals/70/documents/what-we-do/cybersecurity/professional-resources/csf-windows-event-log-monitoring-guidance.pdf](https://www.nsa.gov/Portals/70/documents/what-we-do/cybersecurity/professional-resources/csf-windows-event-log-monitoring-guidance.pdf)
    
- [https://www.sans.org/white-papers/33314/](https://www.sans.org/white-papers/33314/)
    
- [https://www.splunk.com/en_us/blog/security/threat-hunting-with-edr.html](https://www.splunk.com/en_us/blog/security/threat-hunting-with-edr.html)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]