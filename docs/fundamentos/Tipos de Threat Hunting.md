## 1. Introducción a los Enfoques de Caza

En la práctica del Threat Hunting existen tres enfoques principales. La madurez de un cazador de amenazas se determina por la capacidad de dominar cada uno de ellos y discernir el momento idóneo para su aplicación operativa.

## 2. Hunting Basado en IoCs (IOC-driven)

Es el enfoque más básico y se sitúa en el nivel inferior de la pirámide del dolor (_Pyramid of Pain_).

### 2.1 Definición de IoC

Un **Indicator of Compromise** es una evidencia técnica puntual de actividad maliciosa, tales como hashes de archivos, direcciones IP, dominios C2 o firmas de antivirus.

### 2.2 Metodología Operativa

El proceso se activa mediante la recepción de indicadores provenientes de reportes de seguridad o feeds de inteligencia. El hunter realiza búsquedas retrospectivas en logs (DNS, Proxy, EDR) para confirmar la presencia del indicador en el entorno.

### 2.3 Análisis de Eficiencia

- **Ventajas:** Alta velocidad de ejecución y facilidad de automatización.
    
- **Desventajas:** Carácter reactivo; limitado a amenazas conocidas; alta volatilidad (los atacantes modifican IoCs con facilidad).
    

## 3. Hunting Basado en Hipótesis (Hypothesis-driven)

Considerado el estándar del Threat Hunting profesional, este enfoque no busca evidencias estáticas, sino comportamientos anómalos.

### 3.1 Definición de Hipótesis

Es una suposición fundamentada sobre el modus operandi de un adversario en un entorno específico.

- **Ejemplo:** _"Si existe movimiento lateral, deben identificarse conexiones RDP inusuales entre estaciones de trabajo"_.
    

### 3.2 Análisis de Eficiencia

- **Ventajas:** Proactividad real; detección de amenazas desconocidas (_Zero-days_); difícil de evadir para el atacante al basarse en TTPs.
    
- **Desventajas:** Requiere alta experiencia técnica y telemetría de alta fidelidad.
    

## 4. Hunting Basado en Inteligencia de Amenazas (CTI-driven)

Utiliza la **Cyber Threat Intelligence** para orientar la cacería hacia amenazas específicas que tienen una alta probabilidad de dirigir ataques contra la organización.

### 4.1 Aplicación de CTI

Se transforman reportes de APTs o campañas activas en búsquedas técnicas. Si un reporte indica que un grupo utiliza **WMI** para movimiento lateral, el hunter busca ejecuciones remotas de `wmic.exe` o eventos de persistencia asociados.

### 4.2 Análisis de Eficiencia

- **Ventajas:** Proporciona un contexto operativo real y permite adelantarse a campañas dirigidas.
    
- **Desventajas:** Dependencia absoluta de la calidad y relevancia del feed de inteligencia.
    

## 5. Matriz Comparativa de Enfoques

| **Tipo de Hunting**   | **Proactivo** | **Detecta Amenazas Nuevas** | **Complejidad** | **Uso Ideal**                            |
| --------------------- | ------------- | --------------------------- | --------------- | ---------------------------------------- |
| **IOC-driven**        | ❌             | ❌                           | Bajo            | Confirmar compromisos conocidos.         |
| **Hypothesis-driven** | ✔️            | ✔️                          | Alto            | Cazar amenazas avanzadas/comportamiento. |
| **CTI-driven**        | ✔️            | ✔️                          | Medio           | Enfrentar campañas activas dirigidas.    |

## 6. Conclusión y Objetivos de Implementación

El enfoque basado en **Hipótesis** representa la mayor capacidad de descubrimiento al no depender de firmas. No obstante, un modelo de defensa resiliente integra los tres métodos: IoCs para lo conocido, CTI para lo inminente e Hipótesis para lo invisible.

---

### Referencias Externas

- [The Pyramid of Pain - David Bianco](https://www.google.com/search?q=https://www.detect-respond.com/posts/pyramid-of-pain/)
    
- [MITRE ATT&CK: TTPs vs IoCs](https://attack.mitre.org/resources/faq/)
    
- [SANS Institute: Generating Hypotheses for Threat Hunting](https://www.sans.org/white-papers/37172/)
    
- [CrowdStrike: Indicator of Attack (IOA) vs Indicator of Compromise (IOC)](https://www.google.com/search?q=https://www.crowdstrike.com/cybersecurity-101/indicators-of-compromise/ioa-vs-ioc/)
    

### Documentación Relacionada

[[MITRE ATT&CK como guía de CTH]]
[[Cyber Kill Chain como guía de CTH]]
[[Modelo Diamante como guía de CTH]]