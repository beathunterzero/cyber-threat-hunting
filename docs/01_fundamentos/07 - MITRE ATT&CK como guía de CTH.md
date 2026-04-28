## 1. ¿Qué es MITRE ATT&CK?

**MITRE ATT&CK** es una base de conocimiento que describe **cómo operan los atacantes en entornos reales**.

En Threat Hunting se usa para:

- Convertir comportamiento en **búsquedas técnicas**
    
- Estandarizar el análisis
    
- Guiar la formulación de hipótesis
    

---

## 2. Estructura básica

- **Tácticas:** objetivo del atacante (por qué)
    
- **Técnicas:** método utilizado (cómo)
    
- **Subtécnicas:** detalle específico
    
- **Procedimientos:** implementación real observada
    

---

## 3. ¿Cómo se usa en Threat Hunting?

Flujo práctico:

1. **Seleccionar técnica**
    
    - Ej: ejecución de comandos
        
2. **Analizar en MITRE**
    
    - Plataformas afectadas
        
    - Ejemplos reales
        
    - Recomendaciones de detección
        
3. **Formular hipótesis**
    
    - Ej: uso de PowerShell para ejecución en memoria
        
4. **Definir telemetría**
    
    - Logs de proceso, red, PowerShell
        
5. **Ejecutar búsqueda**
    
    - Queries en SIEM / EDR
        
6. **Convertir en detección**
    
    - Regla persistente
        

---

## 4. Uso operativo

MITRE permite:

- **Estandarizar lenguaje**
    
    - Blue Team, Red Team, SOC
        
- **Enfocar en comportamiento**
    
    - TTPs sobre IoCs
        
- **Identificar brechas**
    
    - Qué técnicas no estás cubriendo
        

---

## 5. Herramientas clave

- **ATT&CK Navigator:**
    
    - Visualización de cobertura
        
    - Identificación de gaps
        
- **Mapeo de CTI:**
    
    - Relación entre actores y técnicas
        

---

## 6. Enfoque práctico

- No usar MITRE como teoría
    
- Usarlo como **guía directa de hunting**
    
- Cada técnica → posible hipótesis
    
- Cada hipótesis → posible detección
    

---

## Referencias Externas

- [https://attack.mitre.org/](https://attack.mitre.org/)
    
- [https://mitre-attack.github.io/attack-navigator/](https://mitre-attack.github.io/attack-navigator/)
    
- [https://car.mitre.org/](https://car.mitre.org/)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[08 - Cyber Kill Chain como guía de CTH]]  
[[09 - Modelo Diamante como guía de CTH]]