## 1. Definición y Propósito

**MITRE ATT&CK** (Adversarial Tactics, Techniques, and Common Knowledge) es una base de conocimiento global, abierta y fundamentada en observaciones del mundo real sobre el comportamiento de los adversarios. En el ámbito del **Threat Hunting**, actúa como el marco de referencia principal para transformar la inteligencia abstracta en búsquedas técnicas accionables.

## 2. Estructura de la Matriz

El marco organiza el comportamiento del atacante en una jerarquía que facilita el análisis:

- **Tácticas:** Representan el objetivo táctico del adversario (el _porqué_, ej. Persistencia).
    
- **Técnicas:** Los métodos específicos utilizados para alcanzar el objetivo (el _cómo_, ej. Tareas programadas).
    
- **Subtécnicas:** Detalles operativos adicionales para una técnica dada.
    
- **Procedimientos:** Implementaciones reales y específicas observadas en grupos de amenazas (ej. comandos exactos usados por un APT).
    

## 3. Actualizaciones Críticas (Versión v19 - Abril 2026)

Un cambio significativo en la arquitectura de MITRE ATT&CK impacta directamente en la formulación de hipótesis:

- **División de Defense Evasion (TA0005):** Esta táctica se ha bifurcado en dos categorías independientes:
    
    - **Stealth (Sigilo):** Enfocada en técnicas de ocultamiento y mimetismo.
        
    - **Impair Defenses (Degradación de Defensas):** Enfocada en acciones que desactivan o corrompen los controles de seguridad.
        
- **Impacto en CTH:** Esta separación permite una clasificación más granular y el diseño de consultas (queries) más precisas para diferenciar entre un atacante que se esconde y uno que sabotea la infraestructura de defensa.
    

## 4. Metodología de Aplicación en CTH

El flujo de trabajo para integrar MITRE en una cacería sigue estos pasos:

1. **Selección de Objetivo:** Identificar una técnica relevante (ej. T1059 - Command and Scripting Interpreter).
    
2. **Análisis de la Técnica:** Revisar en MITRE las plataformas afectadas, ejemplos reales y recomendaciones de detección.
    
3. **Formulación de Hipótesis:** Convertir la técnica en una suposición lógica (ej. _"Uso de PowerShell para ejecución de payloads en memoria"_).
    
4. **Identificación de Telemetría:** Determinar los logs necesarios (Event ID 4104, logs de procesos, conexiones de red).
    
5. **Ejecución de Consultas:** Implementar queries (KQL, SQL, Splunk) buscando patrones como `EncodedCommand` o procesos hijos anómalos.
    
6. **Institucionalización:** Convertir los hallazgos exitosos en reglas permanentes en el SIEM/EDR.
    

## 5. Herramientas de Apoyo

- **ATT&CK Navigator:** Utilizado para visualizar la cobertura actual del SOC, identificar brechas (gaps) y planificar los próximos hunts.
    
- **Mapeo de CTI:** Estructuración de reportes de inteligencia mediante la vinculación de grupos APT con sus técnicas preferidas.
    

## 6. Valor Operativo

La adopción de MITRE ATT&CK garantiza que el hunting sea:

- **Estandarizado:** Proporciona un lenguaje común entre Blue, Red y Threat Hunting Teams.
    
- **Comportamental:** Desplaza el foco de los simples IoCs hacia el análisis de TTPs difíciles de evadir.
    
- **Medible:** Permite cuantificar la resiliencia de la organización frente a técnicas de ataque específicas.
    

---

### Referencias Externas

- [MITRE ATT&CK Official Website](https://www.google.com/url?sa=E&source=gmail&q=https://attack.mitre.org/)
    
- [ATT&CK Navigator Tool](https://www.google.com/url?sa=E&source=gmail&q=https://mitre-attack.github.io/attack-navigator/)
    
- [MITRE v19 Release Notes - April 2026](https://attack.mitre.org/resources/updates/)
    
- [Cyber Analytics Repository (CAR)](https://car.mitre.org/)
    

### Documentación Relacionada

[[Tipos de Threat Hunting]]
[[Modelo Diamante como guía de CTH]]
[[Cyber Kill Chain como guía de CTH]]