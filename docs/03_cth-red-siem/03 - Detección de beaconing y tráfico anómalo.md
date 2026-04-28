## 1. ¿Qué es beaconing?

Comunicación periódica desde un host comprometido hacia un C2.

Características:

- Repetitiva
    
- Automatizada
    
- Diseñada para pasar desapercibida
    

---

## 2. Qué se busca

Detectar:

- Patrones de tiempo
    
- Repetición de destinos
    
- Comportamiento de red anómalo
    

Siempre correlacionar:

- Red + DNS + procesos
    

---

## 3. Indicadores clave

|Categoría|Indicador|
|---|---|
|Temporal|Intervalos regulares|
|Payload|Requests similares|
|Volumen|Más salida que entrada|
|DNS|Subdominios largos o aleatorios|
|Destino|IPs o países inusuales|
|Endpoint|Procesos con conexiones periódicas|

---

## 4. Técnicas de análisis

### 4.1 Periodicidad

- Detectar intervalos constantes
    
- Incluso con jitter
    

Métodos:

- Autocorrelación
    
- Análisis de frecuencia
    

---

### 4.2 Baseline

- Comportamiento normal por host
    
- Detectar desviaciones
    

---

### 4.3 Agrupación

Agrupar por:

- IP destino
    
- Puerto
    
- User-Agent
    
- Host
    

Buscar:

- Intervalos consistentes
    

---

### 4.4 Entropía

- Detectar datos codificados
    
- Identificar DGA o tunneling
    

Ejemplos:

- Base64
    
- Base32
    

---

## 5. Indicadores prácticos

- Conexiones cada X minutos
    
- Tráfico pequeño pero constante
    
- DNS repetitivo
    
- Procesos inusuales con red
    

---

## 6. Enfoque de hunting

- Analizar tiempo + volumen
    
- Correlacionar con endpoint
    
- Detectar patrones repetitivos
    
- Validar contra baseline
    

---

## 7. Objetivo

- Detectar C2 silencioso
    
- Identificar beaconing temprano
    
- Reducir persistencia del atacante
    

---

## Referencias Externas

- [https://attack.mitre.org/techniques/T1071/001/](https://attack.mitre.org/techniques/T1071/001/)
    
- [https://attack.mitre.org/techniques/T1568/001/](https://attack.mitre.org/techniques/T1568/001/)
    
- [https://www.elastic.co/security-labs](https://www.elastic.co/security-labs)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[04 - DNS tunneling, HTTPs sospechoso y uso de Tor]]