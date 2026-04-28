## 1. ¿Qué es el modelo de madurez?

Es un marco para evaluar y mejorar la capacidad de **Threat Hunting**.

Objetivo:

- Pasar de detección reactiva → proactiva
    
- Establecer una evolución clara
    
- Medir capacidades reales
    

Se basa en:

- **Personas**
    
- **Procesos**
    
- **Herramientas**
    

---

## 2. Pilares del modelo

### 2.1 Personas

Evalúa al equipo y su nivel técnico.

|Nivel|Características|
|---|---|
|Inicial|Sin roles definidos|
|Gestionado|Liderazgo básico|
|Definido|Hunters dedicados|
|Cuantitativo|Métricas y rotación|
|Optimizado|Integración total|

---

### 2.2 Procesos

Evalúa cómo se hace hunting.

|Nivel|Características|
|---|---|
|Inicial|Sin estructura|
|Gestionado|Uso de IoCs|
|Definido|Proceso formal|
|Cuantitativo|Enfoque en TTPs|
|Optimizado|Automatización continua|

---

### 2.3 Herramientas

Evalúa capacidades tecnológicas.

|Nivel|Características|
|---|---|
|Inicial|Sin automatización|
|Gestionado|Queries básicas|
|Definido|Análisis + repositorio|
|Cuantitativo|Dashboards y visualización|
|Optimizado|ML + automatización continua|

---

## 3. Lectura operativa del modelo

- Nivel bajo → hunting reactivo
    
- Nivel medio → hunting estructurado
    
- Nivel alto → hunting continuo y automatizado
    

---

## 4. Aplicación en laboratorio

Objetivo recomendado: **Nivel 3 (Definido)**

- **Personas:**
    
    - Rol claro de hunter
        
- **Procesos:**
    
    - Hunting basado en comportamiento
        
- **Herramientas:**
    
    - Uso organizado de SIEM + EDR
        
    - Repositorio de queries (Obsidian)
        

---

## 5. Resultado esperado

- Cacerías repetibles
    
- Mejora continua
    
- Reducción del dwell time
    
- Generación de detecciones
    

---

## Referencias Externas

- [https://www.sans.org/white-papers/37702/](https://www.sans.org/white-papers/37702/)
    
- [https://www.threathunting.net/](https://www.threathunting.net/)
    

---

## Documentación Relacionada

[[02 - Técnicas de comunicación de C2 y exfiltración]]  
[[03 - Detección de beaconing y tráfico anómalo]]  
[[04 - DNS tunneling, HTTPs sospechoso y uso de Tor]]  
[[05 - Threat Hunting en SIEM]]  
[[06 - Ejemplo de hipótesis en SIEM]]  
[[07 - Casos de hunting basados en logs de firewall, proxy y autenticación]]  
[[08 - Integración con CTI]]  
[[09 - Uso de IoCs de fuentes abiertas]]  
[[10 - Convertir inteligencia en hipótesis de hunting]]  
[[01 - Filosofía y estrategia del Threat Hunting]]