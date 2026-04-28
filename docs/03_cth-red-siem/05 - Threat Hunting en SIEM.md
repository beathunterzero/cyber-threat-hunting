## 1. ¿Qué es el hunting en SIEM?

Proceso proactivo para detectar amenazas usando datos centralizados.

Diferencia clave:

- No responde a alertas
    
- Busca lo que aún no ha sido detectado
    

---

## 2. Ciclo de hunting en SIEM

### 2.1 Hipótesis

- Basada en CTI, IoCs o anomalías
    
- Define qué buscar
    

---

### 2.2 Datos

- Centralizar fuentes:
    
    - endpoint
        
    - red
        
    - cloud
        
- Enriquecer con:
    
    - GeoIP
        
    - reputación
        
    - MITRE
        

---

### 2.3 Búsqueda

- Crear queries o correlaciones
    
- Detectar patrones y secuencias
    

---

### 2.4 Validación

- Comparar contra baseline
    
- Analizar contexto
    
- Reducir falsos positivos
    

---

### 2.5 Mejora

- Documentar hallazgos
    
- Crear reglas
    
- Ajustar detecciones
    

---

## 3. Pilares clave

### 3.1 Normalización

- Unificar datos
    
- Ej: ECS, ASIM
    

---

### 3.2 Correlación

- Unir eventos de distintas fuentes
    
- Ej: red + endpoint
    

---

### 3.3 Reducción de ruido

- Filtrar actividad legítima
    
- Priorizar anomalías reales
    

---

## 4. Enfoque de hunting

- Pensar en comportamiento
    
- Usar múltiples fuentes
    
- Validar siempre contra baseline
    
- Iterar continuamente
    

---

## 5. Objetivo

- Detectar amenazas no visibles
    
- Mejorar cobertura
    
- Fortalecer el SOC
    

---

## Referencias Externas

- [https://mitre-attack.github.io/attack-navigator/](https://mitre-attack.github.io/attack-navigator/)
    
- [https://www.sans.org/white-papers/37172/](https://www.sans.org/white-papers/37172/)
    
- [https://learn.microsoft.com/en-us/azure/sentinel/hunting](https://learn.microsoft.com/en-us/azure/sentinel/hunting)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[06 - Ejemplo de hipótesis en SIEM]]