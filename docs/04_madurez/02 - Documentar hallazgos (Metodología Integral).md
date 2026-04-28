## 1. Propósito de la Documentación

La documentación en Threat Hunting tiene como objetivo **convertir una investigación manual en una capacidad de detección reutilizable y medible**.

Debe permitir:

- Trazabilidad
    
- Reproducibilidad
    
- Conversión a detección
    
- Mejora continua
    

---

## 2. Enfoque Operativo Correcto

### Modelo principal:

- Hypothesis-Driven Hunting
    

### Soporte técnico:

- MITRE ATT&CK
    

### Uso opcional:

- Cyber Kill Chain (solo contexto)
    
- Diamond Model (solo pivoting)
    

---

## 3. Estructura Operativa de Documentación

---

### I. Identificación del Hunt

- Hunt ID
    
- Fecha
    
- Analista
    
- Scope
    

---

### II. Hipótesis

Debe ser clara, verificable y basada en CTI o comportamiento.

---

### III. Telemetría

- Fuentes de datos
    
- Campos clave
    

---

### IV. Query

- Query exacta
    
- Rango temporal
    
- Scope
    

---

### V. Evidencias

- Procesos
    
- Conexiones
    
- Usuarios
    
- IoCs (solo si aportan valor)
    
- Mapeo a TTPs
    

---

### VI. Análisis

- Interpretación
    
- Resultado:
    
    - Confirmado
        
    - Falso positivo
        
    - Sospechoso
        

---

### VII. Producción (Detection Engineering)

- Regla generada
    
- Lógica
    
- Cobertura MITRE
    

---

## 4. Eliminación de Ruido

Evitar:

- Sobrecarga de frameworks
    
- Teoría innecesaria
    
- IoCs como base
    
- Uso forzado de modelos
    

---

## 5. Uso Correcto de Frameworks

### MITRE ATT&CK

✔ Obligatorio  
✔ Define comportamiento  
✔ Permite medir cobertura

---

### Cyber Kill Chain

✔ Contexto  
✘ No base del hunt

---

### Diamond Model

✔ Pivoting  
✘ No obligatorio

---

## 6. Plantilla Final (Obsidian)

````markdown
# [HUNT-ID] - [Título]

**Analista:**  
**Fecha:**  
**Entorno:**  

---

## 1. Hipótesis
[Hipótesis clara]

---

## 2. Telemetría
- Fuentes:
- Campos:

---

## 3. Query
// Query

---

## 4. Evidencias
- Procesos: 
- Red:
- Usuarios:

---

## 5. MITRE ATT&CK
- Táctica:
- Técnica:

---

## 6. Análisis
- Interpretación:
- Resultado:

---

## 7. Detección
- Regla:
- Lógica:
- Cobertura:

````
---

## 7. Relación con Métricas

Se conecta directamente con:

- MTTD  
- MTTR  
- Detection Yield  
- Cobertura de TTPs  

---

## 8. Conclusión Técnica

La documentación es parte del ciclo de detección.

> Un hunt termina cuando se convierte en detección.

---

## Referencias Externas

- https://attack.mitre.org/  
- https://attack.mitre.org/resources/working-with-attack/  
- https://www.sans.org/white-papers/37172/  
- https://www.sans.org/white-papers/37702/  

---

## Documentación Relacionada

[[01 - Madurez y métricas de hunting]]  
[[03 - Conversión de hunts en casos de uso para SIEM y SOAR]]  
[[10 - Convertir inteligencia en hipótesis de hunting]]  
[[05 - Threat Hunting en SIEM]]  
[[06 - Queries y hunting en EDR]]
[[08 - Integración con CTI]]  