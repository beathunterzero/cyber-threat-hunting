## 1. Definición y Concepto Operativo

El **Threat Hunting** es la práctica proactiva de buscar amenazas que han evadido las soluciones de seguridad tradicionales y ya se encuentran dentro del entorno. A diferencia del monitoreo convencional, no es reactivo; es una actividad estratégica y analítica basada en la formulación de hipótesis.

- **Premisa:** No se espera la generación de una alerta; el cazador toma la iniciativa para localizar al atacante antes de que ejecute su objetivo final.
    

## 2. Justificación Estratégica

Las defensas tradicionales (AV, Firewalls, IDS basados en firmas) resultan insuficientes ante adversarios modernos que emplean:

- **LOLBins (Living off the Land Binaries):** Uso de herramientas legítimas del sistema para actividades maliciosas.
    
- **Movimiento Lateral:** Desplazamiento interno sin disparar alertas de perímetro.
    
- **Evasión de Firmas:** Técnicas de ofuscación que evitan la detección estática.
    
- **Persistencia Silenciosa:** Ocultamiento en procesos normales para maximizar el **Dwell Time** (tiempo de permanencia).
    

## 3. Características Clave

- **Proactivo:** El cazador inicia la búsqueda sin indicios previos de compromiso.
    
- **Basado en Hipótesis:** Cada cacería parte de una suposición fundamentada (ej. _"Si hay persistencia, debe existir un servicio o tarea programada de reciente creación"_).
    
- **Iterativo:** El proceso es un ciclo continuo que genera nuevas detecciones, reglas y conocimiento.
    
- **Centrado en Comportamiento:** Prioriza la identificación de **TTPs** (Tácticas, Técnicas y Procedimientos) sobre los simples indicadores de compromiso (IoCs).
    

## 4. Diferenciación Funcional (¿Qué NO es Threat Hunting?)

Es fundamental distinguir esta disciplina de otras áreas operativas:

- **No es Monitoreo de Alertas:** Eso corresponde al SOC Nivel 1.
    
- **No es Respuesta a Incidentes (IR):** El IR comienza una vez que la amenaza ha sido confirmada.
    
- **No es Análisis Forense:** El forense suele ser post-mortem; el hunting ocurre durante la actividad del atacante.
    
- **No es revisión de logs sin propósito:** Requiere un objetivo analítico claro y guiado.
    

## 5. El Ciclo del Threat Hunting

El modelo operativo consta de 4 fases principales:

1. **Hipótesis:** Generada a partir de inteligencia de amenazas, anomalías observadas o experiencia previa.
    
2. **Recolección y Análisis:** Consulta de telemetría, revisión de logs y correlación de eventos.
    
3. **Investigación:** Fase de validación para confirmar o descartar actividad maliciosa.
    
4. **Acción y Mejora:** Documentación, ajuste de alertas existentes y creación de nuevas capacidades de detección.
    

## 6. Requerimientos Técnicos y Capacidades

- **Datos y Telemetría:** Logs de SO (Windows/Linux), Sysmon, telemetría de EDR, DNS, registros de autenticación y tráfico de red.
    
- **Herramientas:** SIEM (Elastic, Splunk, Sentinel), EDR (Velociraptor, Defender, CrowdStrike), Scripts (Python, PowerShell) y el marco de **MITRE ATT&CK**.
    
- **Perfil del Analista:** Pensamiento crítico, dominio de TTPs, capacidad de correlación de datos y conocimiento profundo de sistemas operativos.
    

## 7. Objetivos Finales

El éxito de una jornada de hunting se mide por:

- Reducción del **Dwell Time** del atacante.
    
- Descubrimiento de ataques invisibles para las herramientas automáticas.
    
- Creación de **nuevas detecciones** (Ingeniería de Detección).
    
- Aumento de la resiliencia y madurez del SOC.
    

---

### Referencias Externas

- [MITRE ATT&CK® Matrix](https://www.google.com/url?sa=E&source=gmail&q=https://attack.mitre.org/)
    
- [The Threat Hunting Project](https://www.threathunting.net/)
    
- [Sigma HQ - Generic Signature Format](https://github.com/SigmaHQ/sigma)
    
- [SANS Digital Forensics and Incident Response Resources](https://www.sans.org/digital-forensics-incident-response/)
    
- [Atomic Red Team Library](https://atomicredteam.io/)
    

### Documentación Relacionada

[[Tipos de Threat Hunting]]
[[Fuente de datos esenciales para Threat Hunting]]