## 1. ¿Qué es el Analytics-Driven Hunting?

El **Threat Hunting basado en analítica** utiliza datos a gran escala para detectar **desviaciones del comportamiento normal (baseline)**.

- Busca lo **desconocido-desconocido**
    
- Se apoya en estadística y visualización
    
- Identifica anomalías, no firmas
    

---

## 2. Técnicas principales

- **Outliers (valores atípicos):**
    
    - Eventos raros o únicos fuera del patrón normal
        
- **Stack Counting (frecuencia):**
    
    - Lo menos frecuente suele ser más sospechoso
        
- **Análisis temporal:**
    
    - Detección de **beaconing**
        
    - Intervalos regulares → posible C2
        

---

## 3. ¿Qué analizar?

|Objeto|Métrica|Indicador|
|---|---|---|
|Red|Bytes enviados vs recibidos|Exfiltración|
|Autenticación|Frecuencia de fallos|Brute force / spraying|
|Procesos|Procesos huérfanos|Inyección / evasión|
|DNS|Subdominios por host|DNS tunneling|

---

## 4. Rol de CTI en analítica

La analítica sin contexto genera ruido. CTI permite:

- **Contextualizar:**
    
    - Relacionar anomalías con amenazas reales
        
- **Priorizar:**
    
    - Enfocar en lo relevante según el entorno
        

---

## 5. Riesgo operativo

**Problema:** saturación del Hunter

- Mezclar hunting + CTI reduce eficiencia
    
- El Hunter pierde foco técnico
    

**Modelo recomendado:**

- CTI → detección externa
    
- Hunter → investigación interna
    

---

## 6. Flujo operativo

1. **Recolección**
    
    - SIEM / EDR
        
2. **Normalización**
    
    - Datos consistentes
        
3. **Visualización**
    
    - Dashboards, patrones
        
4. **Análisis**
    
    - Identificación de anomalías
        
5. **Enriquecimiento**
    
    - Validación con CTI
        

---

## Referencias Externas

- [https://www.sans.org/white-papers/37500/](https://www.sans.org/white-papers/37500/)
    
- [https://www.elastic.co/guide/en/kibana/current/discover.html](https://www.elastic.co/guide/en/kibana/current/discover.html)
    
- [https://www.elastic.co/guide/en/kibana/current/lens.html](https://www.elastic.co/guide/en/kibana/current/lens.html)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[04 - Threat Hunting basado en IoCs (IoC-Driven)]]  
[[05 - Threat Hunting basado en Hipótesis (Hypothesis-Driven)]]