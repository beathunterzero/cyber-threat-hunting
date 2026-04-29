# Cyber Threat Hunting

Base de conocimiento estructurada y laboratorio de Threat Hunting enfocado en investigaciones basadas en hipótesis, desarrollo de detecciones y análisis de seguridad utilizando metodologías reales.

Este repositorio está diseñado como una base de conocimiento profesional, no como un simple backup de notas, y está alineado con:

- MITRE ATT&CK
    
- Cyber Kill Chain
    
- Threat Hunting basado en hipótesis
    

---

## Propósito

Este proyecto tiene como objetivo:

- Documentar conceptos de Threat Hunting de forma estructurada
    
- Desarrollar y registrar hipótesis de caza
    
- Convertir investigaciones en lógica de detección
    
- Construir una base de conocimiento reutilizable
    
- Soportar laboratorios prácticos (Elastic Stack)
    

---

## Metodología

El contenido sigue un enfoque estructurado de Threat Hunting:

1. Entender el contexto (MITRE ATT&CK, Kill Chain)
    
2. Formular hipótesis
    
3. Validar con telemetría y logs
    
4. Documentar hallazgos
    
5. Convertir en detecciones o casos de uso
    

---

## Estructura del repositorio

```text
cyber-threat-hunting/  
│  
├── docs/ # Base de conocimiento (desde fundamentos hasta nivel avanzado) 
│ ├── 01_fundamentos/ # Conceptos base, marcos y estrategia 
│ ├── 02_cth-endpoints/ # Técnicas de hunting en endpoints  
│ ├── 03_cth-red-siem/ # Hunting en red y SIEM 
│ ├── 04_madurez/ # Métricas, procesos y evolución 
│ └── 05_glosario/ # Terminología 
│  
├── hipotesis/ # Investigaciones basadas en hipótesis 
│ ├── endpoint/  
│ ├── red/  
│ └── siem/  
│  
├── labs/ # Implementaciones prácticas 
│ └── elastic-security-lab/
│ └── velociraptor-security-lab/
│ └── wireshark-security-lab/
```


---

## Base de conocimiento (docs)

Incluye:

- Metodologías de hunting (IoC, hipótesis, analítica)
    
- MITRE ATT&CK y Cyber Kill Chain
    
- Fuentes de datos y telemetría
    
- Estrategias de detección
    
- Comparación EDR vs SIEM
    
- Datasets de ataque simulado
    

---

## Threat Hunting basado en hipótesis

La sección hipotesis contiene investigaciones estructuradas orientadas a:

- Definir problemas de detección
    
- Validar comportamientos de atacante
    
- Generar conocimiento accionable
    

---

## Laboratorios

Incluye un entorno práctico basado en:

- Elastic Stack (Elasticsearch, Kibana, Filebeat)
    
- Velociraptor
    
- Wireshark
    
- Ingesta de logs
    
- Creación de reglas de detección
    
- Flujos de Threat Hunting
    

---

## Posicionamiento

Este repositorio representa:

- Una base de conocimiento de Threat Hunting
    
- Fundamentos de Detection Engineering
    
- Un proyecto de portafolio orientado a SOC
    

---

## Alcance

- Uso educativo y desarrollo profesional
    
- No contiene datos sensibles ni de producción
    

---

## Autor

beathunterzero

[[01 - Filosofía y estrategia del Threat Hunting]]