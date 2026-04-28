## 1. ¿Qué es Threat Hunting?

El **Threat Hunting** es una práctica **proactiva** orientada a identificar amenazas que ya están dentro del entorno y no han sido detectadas por controles tradicionales.

- No depende de alertas
    
- Parte de una **hipótesis**
    
- Asume compromiso (**Assume Breach**)
    

---

## 2. ¿Por qué es necesario?

Las defensas tradicionales (AV, Firewalls, IDS basados en firmas) son insuficientes frente a técnicas modernas:

- **LOLBins:** uso de herramientas legítimas (`powershell.exe`, `certutil.exe`, `wmic.exe`)
    
- **Movimiento lateral:** desplazamiento interno sin alertas perimetrales
    
- **Evasión de firmas:** malware ofuscado o polimórfico
    
- **Persistencia:** ocultamiento en servicios, procesos o tareas programadas (**Dwell Time** elevado)
    

---

## 3. Principios del Threat Hunting

- **Proactivo:** no espera alertas
    
- **Basado en hipótesis:** cada búsqueda parte de una suposición clara
    
- **Iterativo:** genera aprendizaje y nuevas detecciones
    
- **Centrado en comportamiento:** enfoque en **TTPs** sobre IoCs
    

---

## 4. ¿Qué NO es Threat Hunting?

- No es monitoreo del SIEM (SOC L1)
    
- No es respuesta a incidentes (IR)
    
- No es análisis forense
    
- No es revisión de logs sin objetivo
    

---

## 5. Flujo de Threat Hunting (Modelo SANS)

1. **Hipótesis (Purpose)**
    
    - Define qué se busca y por qué (basado en TTPs, CTI o riesgos)
        
2. **Alcance (Scope)**
    
    - Define activos, entorno y periodo de análisis
        
3. **Datos y herramientas (Tooling/Data)**
    
    - Fuentes: Sysmon, Windows Event Logs, logs de red
        
    - Herramientas: Elastic Security, Velociraptor
        
4. **Investigación (Investigation)**
    
    - Búsqueda de patrones que validen o descarten la hipótesis
        
5. **Hallazgos (Findings)**
    
    - Clasificación de resultados (falsos positivos vs actividad sospechosa)
        
6. **Automatización (Automation)**
    
    - Conversión en reglas de detección en el SIEM
        
    - Evita repetir hunting manual
        

---

## 6. Monitoreo vs Threat Hunting

|Monitoreo (Reactivo)|Threat Hunting (Proactivo)|
|---|---|
|Basado en alertas|Basado en hipótesis|
|Enfocado en incidentes conocidos|Enfocado en lo desconocido|
|Uso de IoCs|Uso de TTPs y comportamiento|
|Cierre de tickets|Generación de detecciones|

---

## Referencias Externas

- [https://attack.mitre.org/](https://attack.mitre.org/)
    
- [https://www.sans.org/posters/threat-hunting/](https://www.sans.org/posters/threat-hunting/)
    
- [https://github.com/SigmaHQ/sigma](https://github.com/SigmaHQ/sigma)
    

---

## Documentación Relacionada

[[02 - Telemetría, capacidades y objetivos del Hunter]]  
[[03 - Fuente de datos esenciales para Threat Hunting]]  
[[04 - Threat Hunting basado en IoCs (IoC-Driven)]]  
[[05 - Threat Hunting basado en Hipótesis (Hypothesis-Driven)]]  
[[06 - Threat Hunting basado en Analítica (Analytics-Driven)]]  
[[07 - MITRE ATT&CK como guía de CTH]]  
[[08 - Cyber Kill Chain como guía de CTH]]  
[[09 - Modelo Diamante como guía de CTH]]  
[[10 - Hipótesis y casos de usos comunes]]  
[[11 - Preparación del entorno de Hunting]]  
[[12 - Comparación detallada de EDR y SIEM]]  
[[13 - Dataset de ataque simulado (logs y malware samples controlados)]]  
[[01 - Creación de elastic-security-lab]]