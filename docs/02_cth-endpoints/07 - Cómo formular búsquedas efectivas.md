## 1. ¿Qué es una búsqueda efectiva?

Es la traducción de una **hipótesis** en una consulta técnica clara.

- No es prueba y error
    
- Es un proceso estructurado
    
- Combina lógica + datos + contexto
    

---

## 2. Secuencia de búsqueda

### 2.1 Definir objetivo

- Qué quieres encontrar
    
- Qué comportamiento buscas
    

Ejemplo:

- Persistencia mediante tareas programadas
    

---

### 2.2 Seleccionar datos

Elegir fuentes correctas:

- Endpoint (Sysmon, Windows)
    
- Red (DNS, NetFlow, Proxy)
    
- Autenticación (AD, cloud)
    
- SIEM / EDR
    

---

### 2.3 Diseñar query

Convertir objetivo en consulta.

Balance:

- Muy amplia → ruido
    
- Muy restrictiva → pierdes eventos
    

---

### 2.4 Analizar resultados

- Validar contexto
    
- Correlacionar eventos
    
- Identificar comportamiento
    

Apoyo:

- TTPs
    
- MITRE ATT&CK
    

---

### 2.5 Refinar y documentar

- Ajustar query
    
- Reducir falsos positivos
    
- Documentar hallazgos
    
- Convertir en detección
    

---

## 3. Errores comunes

- No definir objetivo
    
- Usar datos incorrectos
    
- Queries sin contexto
    
- No validar resultados
    
- No iterar
    

---

## 4. Buenas prácticas

- Pensar en comportamiento
    
- Empezar simple → iterar
    
- Usar ventanas de tiempo acotadas
    
- Correlacionar múltiples fuentes
    
- Documentar siempre
    

---

## 5. Resultado esperado

- Query reutilizable
    
- Detección automatizable
    
- Mejora continua del hunting
    

---

## Referencias Externas

- [https://mitre-attack.github.io/attack-navigator/](https://mitre-attack.github.io/attack-navigator/)
    
- [https://www.sans.org/white-papers/36422/](https://www.sans.org/white-papers/36422/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]