## 1. Definición y Propósito

El Hunting en EDR es un **proceso proactivo** donde los analistas buscan amenazas mediante consultas sobre la telemetría de los endpoints. Recopila eventos de procesos, red, archivos y autenticaciones para detectar anomalías o TTPs (Tácticas, Técnicas y Procedimientos) no identificados automáticamente por las reglas estáticas. Además, permite ejecutar acciones de respuesta inmediata ante indicios de compromiso.

## 2. Ciclo de Vida del Hunt: Preparación y Ejecución (Fases 1 a 4)

### **Fase 1: Revisión**

- Se definen las fuentes de datos y los eventos que el EDR debe capturar: procesos, red, archivos, registro y autenticaciones.
    
- Se establece la retención de datos (7, 30 o 90 días) y se normalizan los campos (por ejemplo, nombre de usuario, proceso, hora) para facilitar las consultas.
    
- Se mapea la telemetría con el marco MITRE ATT&CK y se verifican permisos y cobertura de agentes en la flota.
    

### **Fase 2: Formulación de hipótesis (Horas antes del hunt)**

- Basada en inteligencia de amenazas o indicadores recientes (TTP, IOC, CVE, alertas).
    
- Se plantea una hipótesis clara, como: _"Buscar ejecuciones de PowerShell con parámetros codificados en hosts críticos"_.
    
- Se identifican los campos relevantes a consultar y se documenta el propósito del hunt.
    

### **Fase 3: Diseño y optimización de queries (Minutos a horas)**

- Se elige el tipo de consulta: basada en indicadores, comportamiento o anomalías estadísticas.
    
- Se optimiza el rendimiento filtrando por campos indexados y acotando el rango temporal.
    
- Se prueban consultas en subconjuntos pequeños antes de ejecutarlas en toda la flota.
    

**Ejemplo de Query Optimizado (KQL):**

Fragmento de código

```kql
DeviceProcessEvents
| where FileName == "powershell.exe"
| where ProcessCommandLine contains "EncodedCommand"
| where Timestamp > ago(7d)
| project Timestamp, DeviceId, InitiatingProcessFileName, ProcessCommandLine
```

### **Fase 4: Ejecución del hunt (Segundos a minutos)**

- Se lanza la búsqueda en modo ad-hoc o programado.
    
- Se registran los parámetros del hunt (fecha, hipótesis, lookback, alcance).
    
- El analista evalúa el volumen de resultados y prioriza los hallazgos relevantes para pasar a la fase de análisis.
    

---

## 3. Ciclo de Vida del Hunt: Análisis, Respuesta y Mejora (Fases 5 a 8)

### **Fase 5: Triage y enriquecimiento (Minutos a horas)**

- Se valida la legitimidad de los resultados cruzando con inteligencia de amenazas, reputación de IPs o análisis de hash.
    
- Se investiga la jerarquía de procesos, módulos cargados y conexiones establecidas.
    
- Se marcan resultados sospechosos para investigación forense profunda.
    

### **Fase 6: Investigación y respuesta (Horas a días)**

- Se recolectan evidencias (logs, artefactos, memoria) y se aíslan los endpoints comprometidos.
    
- Se determina si el evento fue legítimo (actividad administrativa real), falso positivo o un ataque confirmado.
    
- Se ejecutan acciones de respuesta directa desde el EDR: bloqueo de cuentas, revocación de privilegios o eliminación de malware.
    

### **Fase 7: Retroalimentación y detección (Días a semanas)**

- Las queries exitosas se transforman en reglas automáticas o alertas permanentes en el SIEM/EDR.
    
- Se ajustan los umbrales, listas blancas y excepciones para reducir la fatiga de alertas.
    
- Se actualizan playbooks de respuesta y se comparte la inteligencia generada con los demás equipos de seguridad.
    

### **Fase 8: Medición e iteración (Proceso continuo)**

- Se analizan métricas de rendimiento operativo como el tiempo medio de detección (MTTD), contención (MTTC) y la reducción del _dwell time_ del atacante.
    
- Se planifican hunts regulares basados en TTPs o comportamientos anómalos recurrentes descubiertos en iteraciones previas.
    
- Se mantiene una biblioteca viva (repositorio) de queries y escenarios de caza para la evolución constante del equipo.
    

---

### Referencias Externas

- [Microsoft Defender XDR: Advanced Hunting with KQL](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-query-language)
    
- [MITRE ATT&CK: Data Sources for EDR Telemetry](https://attack.mitre.org/datasources/)
    
- [SANS Institute: The Threat Hunting Project & Methodology](https://www.google.com/search?q=https://www.sans.org/reading-room/whitepapers/threats/hunt-evil-practical-guide-threat-hunting-36422)
    

### Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]