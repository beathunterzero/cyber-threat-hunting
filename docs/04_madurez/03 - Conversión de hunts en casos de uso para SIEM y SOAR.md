## 1. Propósito

La conversión de un _hunt_ a un caso de uso tiene un único objetivo:

> **Transformar detección manual en detección automática y accionable.**

Esto representa el punto donde el Threat Hunting aporta valor real al SOC:

- Reduce MTTD
    
- Reduce MTTR
    
- Aumenta cobertura de TTPs
    
- Elimina dependencia de hunts repetitivos
    

---

## 2. Roles Claros: SIEM vs SOAR

|Aspecto|SIEM|SOAR|
|---|---|---|
|Rol|Detección|Respuesta|
|Función|Identificar anomalías y TTPs|Ejecutar acciones automáticas|
|Salida|Alerta|Acción|
|Dependencia|Logs y correlación|Triggers del SIEM|

---

### Principio clave

> **SIEM detecta. SOAR actúa.**

---

## 3. Flujo Real de Conversión

Modelo operativo correcto:

**Hunt → Detección → Validación → Producción → Automatización**

---

### Fase 1: Extracción del patrón

Desde el hunt se obtiene:

- Comportamiento detectado
    
- Condiciones específicas
    
- Contexto mínimo necesario
    

---

### Fase 2: Diseño de detección (SIEM)

Se traduce a:

- Query optimizada
    
- Lógica clara
    
- Umbrales definidos
    

---

### Fase 3: Validación

- Ejecución en histórico
    
- Medición de ruido
    
- Ajuste de falsos positivos
    

---

### Fase 4: Producción

- Regla activa en SIEM
    
- Alertas generadas automáticamente
    

---

### Fase 5: Automatización (SOAR)

- Trigger: alerta del SIEM
    
- Acción: respuesta automatizada
    

---

## 4. Uso Correcto de Frameworks

### MITRE ATT&CK

✔ Obligatorio en conversión  
✔ Define qué técnica estás cubriendo  
✔ Permite medir cobertura

---

### Cyber Kill Chain

✔ Opcional (solo contexto)  
✘ No necesario en la conversión

---

### Diamond Model

✘ Eliminar en este proceso  
✘ No aporta valor en detección automática

---

## 5. Qué se convierte realmente

Un error común es intentar convertir todo el hunt.

Solo se debe convertir:

- El patrón repetible
    
- El comportamiento detectable
    
- La señal con baja ambigüedad
    

---

### No convertir:

- Hipótesis
    
- Contexto narrativo
    
- IoCs temporales
    

---

## 6. Estructura Operativa del Caso de Uso

---

### I. Identificación

- UC-ID
    
- Hunt origen
    
- Estado
    

---

### II. Lógica de detección (SIEM)

- Query productiva
    
- Condiciones
    
- Umbrales
    
- **Mapeo MITRE:**
    
    - Táctica
        
    - Técnica
        

---

### III. Validación

- Falsos positivos
    
- Ajustes
    
- Scope
    

---

### IV. Respuesta (SOAR)

- Trigger
    
- Acciones automatizadas
    

---

### V. Métricas

- Impacto en MTTD
    
- Impacto en MTTR
    
- Volumen de alertas
    

---

## 7. Plantilla Final para Obsidian

````markdown
# [UC-ID] - [Nombre del Caso de Uso]

**Origen:** [HUNT-ID]  
**Estado:** [Testing / Producción]  

---

## 1. Detección (SIEM)

### Lógica
[Descripción breve del patrón]

### Query
// Query optimizada

### MITRE ATT&CK
- Táctica:
- Técnica:

---

## 2. Validación

- Falsos positivos:
- Ajustes:
- Scope:

---

## 3. Respuesta (SOAR)

### Trigger
Alerta [UC-ID]

### Acciones
1. Acción automática 1
2. Acción automática 2
3. Notificación

---

## 4. Métricas

- MTTD:
- MTTR:
- Volumen de alertas:
````

---

## 8. Conclusión Técnica

La conversión es el punto donde Threat Hunting deja de ser exploración y se convierte en capacidad defensiva.

---

### Principio final

> Si no se convierte en detección, el hunt no escala.

---

## Referencias Externas

- https://attack.mitre.org/  
- https://attack.mitre.org/datasources/  
- https://www.sans.org/white-papers/37172/  

---

## Documentación Relacionada

[[02 - Documentar hallazgos (Metodología Integral)]]  
[[01 - Madurez y métricas de hunting]]  
[[05 - Threat Hunting en SIEM]]  
[[06 - Queries y hunting en EDR]]
[[10 - Convertir inteligencia en hipótesis de hunting]]  