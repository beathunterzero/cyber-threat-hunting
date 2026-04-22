## 1. Requerimientos Técnicos: Datos y Telemetría

La efectividad de una cacería depende directamente de la visibilidad. Si un evento no se registra, es invisible para el cazador. La telemetría debe ser rica, contextual y recolectada de diversas fuentes para cubrir todos los puntos ciegos.

- **Logs de Sistema Operativo (Windows/Linux):** Eventos de autenticación (4624/4625), creación de servicios y limpieza de logs.
    
- **Sysmon:** Crucial para visibilidad profunda en Windows (Process Creation, Network Connections, File Creation Time).
    
- **Telemetría de EDR (Velociraptor):** Recolección de artefactos en caliente, análisis de memoria y persistencia en el endpoint.
    
- **Registros de Red:** Tráfico DNS, flujos de red (NetFlow) y logs de Firewall para detectar C2 o exfiltración.
    
- **Identidad y Cloud:** Registros de autenticación (Azure AD/Okta) y logs de actividad en la nube (CloudTrail).
    

## 2. La Pirámide del Dolor (The Pyramid of Pain)

En el Threat Hunting, buscamos movernos hacia la cúspide de la pirámide. Cuanto más arriba operamos, más difícil y costoso es para el atacante evadir nuestra detección.

|**Nivel**|**Indicador**|**Valor para el Hunter**|**"Dolor" para el Atacante**|
|---|---|---|---|
|**Bajo**|Valores Hash / IPs|Bajo (fáciles de cambiar)|Trivial / Nada|
|**Medio**|Nombres de Dominio|Moderado|Fastidioso|
|**Alto**|Artefactos de Red / Host|Alto (herramientas específicas)|Molesto|
|**Cúspide**|**TTPs (Tácticas y Técnicas)**|**Máximo (Comportamiento)**|**Extremo (Requiere reentrenarse)**|

- **Enfoque Operativo:** No perdemos tiempo cazando solo IPs; cazamos el comportamiento (ej. el uso de un LOLBin para descargar un payload).
    

## 3. Capacidades y Herramientas del Laboratorio

Para ejecutar las cacerías definidas en la filosofía de la Parte 1, utilizamos el stack tecnológico configurado en los documentos previos:

- **SIEM (Elastic Security):** Centraliza la telemetría y permite correlacionar eventos de múltiples fuentes mediante **KQL** (Kibana Query Language).
    
- **EDR (Velociraptor):** Permite realizar "hunts" proactivos en los endpoints para extraer evidencias forenses antes de que sean borradas.
    
- **Framework MITRE ATT&CK:** Actúa como nuestra base de conocimientos para entender cómo operan los adversarios y qué buscar específicamente.
    
- **Scripts (Python/PowerShell):** Automatización de tareas repetitivas y análisis personalizado de grandes volúmenes de datos.
    

## 4. Perfil del Analista (Mindset)

El "Cazador" no solo conoce las herramientas, sino que posee un perfil analítico específico:

- **Pensamiento Crítico:** Capacidad para cuestionar la normalidad del tráfico y los procesos.
    
- **Dominio de TTPs:** Entender no solo qué hace el malware, sino cómo se mueve el atacante.
    
- **Correlación de Datos:** Habilidad para unir un evento de red aislado con una ejecución de proceso en un endpoint.
    

## 5. Objetivos Finales y Métricas de Éxito

El éxito de una jornada de hunting no se mide solo por encontrar incidentes, sino por la mejora continua del sistema de defensa:

1. **Reducción del Dwell Time:** Detectar al atacante antes de que logre su objetivo final (exfiltración o cifrado).
    
2. **Descubrimiento de "Invisibles":** Identificar ataques que han pasado por debajo del radar de las herramientas automáticas.
    
3. **Ingeniería de Detección:** Cada cacería manual exitosa debe terminar en la creación de una **nueva regla de alerta** en el SIEM.
    
4. **Resiliencia y Madurez:** Aumentar la capacidad del SOC para resistir ataques similares en el futuro.
    

---

### Referencias Externas

- [The Pyramid of Pain - David J Bianco](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
    
- [MITRE ATT&CK Matrix for Enterprise](https://www.google.com/url?sa=E&source=gmail&q=https://attack.mitre.org/)
    
- [Sysmon Documentation - Microsoft Learn](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    

### Documentación Relacionada
[[01 - Filosofía y estrategia del Threat Hunting]]