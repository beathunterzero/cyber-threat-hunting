## 1. ¿SIEM vs EDR?

En Threat Hunting:

- **SIEM:** visión global (macro)
    
- **EDR:** visibilidad profunda (micro)
    

No compiten → se complementan.

---

## 2. Comparativa rápida

|Característica|SIEM|EDR|
|---|---|---|
|Enfoque|Global (infraestructura)|Endpoint|
|Datos|Multifuente|Detallados del host|
|Análisis|Correlación|Comportamiento|
|Respuesta|Alertas|Acciones directas|
|Uso|Visibilidad, detección|Investigación, contención|
|Escala|Datos|Agentes|

---

## 3. ¿Qué hace cada uno en hunting?

### SIEM

- Centraliza logs
    
- Detecta patrones entre múltiples fuentes
    
- Permite búsquedas históricas
    
- Genera alertas
    

Uso típico:

- Encontrar anomalía inicial
    

---

### EDR

- Observa el endpoint en detalle
    
- Analiza procesos, memoria, persistencia
    
- Permite acciones directas
    

Uso típico:

- Investigar y confirmar
    

---

## 4. Ejemplo operativo

1. SIEM detecta:
    
    - actividad anómala (ej. DNS sospechoso)
        
2. Se identifica el host
    
3. EDR analiza:
    
    - procesos
        
    - comandos ejecutados
        
    - artefactos
        
4. Se confirma o descarta la amenaza
    

---

## 5. Stack del laboratorio

### SIEM (Elastic)

- Ingesta de logs
    
- Queries (KQL)
    
- Correlación
    
- Reglas de detección
    
- Mapeo a MITRE
    

---

### EDR (Velociraptor)

- Queries (VQL)
    
- Recolección forense
    
- Análisis de persistencia
    
- Timeline de eventos
    
- Acciones en endpoint
    

---

## 6. Idea clave

- SIEM → encuentra el problema
    
- EDR → lo explica
    

---

## Referencias Externas

- [https://www.elastic.co/guide/en/security/current/index.html](https://www.elastic.co/guide/en/security/current/index.html)
    
- [https://docs.velociraptor.app/](https://docs.velociraptor.app/)
    
- [https://attack.mitre.org/](https://attack.mitre.org/)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]