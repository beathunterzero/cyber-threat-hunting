## 1. ¿Qué datos necesita el Threat Hunting?

La efectividad del hunting depende directamente de la **visibilidad**.  
Si un evento no se registra, no existe para el analista.

La telemetría debe ser **rica, contextual y diversa**:

- **Logs de Sistema Operativo (Windows/Linux):**
    
    - Autenticación (4624, 4625)
        
    - Creación de servicios
        
    - Limpieza de logs
        
- **Sysmon:**
    
    - Creación de procesos
        
    - Conexiones de red
        
    - Cambios en archivos
        
- **Telemetría EDR (Velociraptor):**
    
    - Recolección de artefactos en vivo
        
    - Persistencia en endpoint
        
    - Análisis de memoria
        
- **Registros de Red:**
    
    - DNS
        
    - NetFlow
        
    - Logs de firewall
        
    - Detección de C2 y exfiltración
        
- **Identidad y Cloud:**
    
    - Autenticaciones (Azure AD, Okta)
        
    - Actividad en cloud (CloudTrail, etc.)
        

---

## 2. Enfoque: Pirámide del Dolor

El objetivo del hunting es operar en niveles altos de la pirámide:  
**a mayor nivel, mayor impacto en el atacante**.

|Nivel|Indicador|Valor para el Hunter|Impacto en el Atacante|
|---|---|---|---|
|Bajo|Hash / IP|Bajo|Nulo|
|Medio|Dominio|Moderado|Bajo|
|Alto|Artefactos host/red|Alto|Medio|
|Cúspide|**TTPs**|**Máximo**|**Alto**|

**Enfoque operativo:**

- Evitar hunting basado solo en IoCs
    
- Priorizar comportamiento (**TTPs**)
    
- Ejemplo: uso de LOLBins para descarga de payloads
    

---

## 3. Herramientas del Hunting

Stack mínimo para ejecutar cacerías:

- **SIEM (Elastic Security):**
    
    - Centralización de logs
        
    - Correlación de eventos
        
    - Uso de **KQL**
        
- **EDR (Velociraptor):**
    
    - Hunting en endpoints
        
    - Recolección de evidencia en vivo
        
- **Framework MITRE ATT&CK:**
    
    - Base para identificar qué buscar
        
    - Mapeo de TTPs
        
- **Scripts (Python / PowerShell):**
    
    - Automatización
        
    - Análisis de datos a medida
        

---

## 4. Perfil del Hunter

El valor no está solo en las herramientas, sino en el análisis:

- **Pensamiento crítico:** cuestionar comportamientos “normales”
    
- **Dominio de TTPs:** entender cómo opera el atacante
    
- **Correlación:** conectar eventos entre distintas fuentes
    

---

## 5. Objetivos del Threat Hunting

El hunting no solo busca incidentes, busca mejorar la defensa:

- **Reducir Dwell Time:** detectar antes del impacto
    
- **Descubrir actividad no detectada:** lo que el SIEM no vio
    
- **Generar detección:** convertir hunting en reglas SIEM
    
- **Mejorar madurez del SOC:** aprendizaje continuo
    

---

## Referencias Externas

- [https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
    
- [https://attack.mitre.org/](https://attack.mitre.org/)
    
- [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]