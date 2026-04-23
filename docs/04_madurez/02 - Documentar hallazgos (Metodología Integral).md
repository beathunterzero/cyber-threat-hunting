## 1. Propósito de la Documentación

Registrar de manera estructurada todo el proceso y los resultados obtenidos, garantizando trazabilidad, validación y mejora continua mediante el uso de marcos de trabajo estandarizados en la industria.

---

## 2. Estructura de Documentación en 6 Pasos con Modelos Integrados

### **I. Identificación del caso**

- **Título o ID del hunt:** Nombre único de la investigación.
    
- **Metadatos:** Fecha, analista responsable y entorno evaluado (red, endpoints, nube, etc.).
    
- **Modelo Diamante (Contexto Inicial):**
    
    - **Víctima:** Identificar el activo crítico o usuario afectado.
        
    - **Infraestructura:** IPs o dominios iniciales detectados.
        

### **II. Hipótesis y objetivo**

- **Descripción de la hipótesis:** Por ejemplo: "Posible comunicación C2 mediante DNS tunneling".
    
- **Objetivo:** Qué se buscaba confirmar o descartar.
    
- **Cyber Kill Chain:** Identificar en qué fase se sitúa la hipótesis (ej. ¿Estamos buscando **Entrega**, **Instalación** o **Comando y Control**?).
    

### **III. Fuentes de datos utilizadas**

- **Logs analizados:** Firewall, proxy, DNS, autenticación, EDR, etc.
    
- **Herramientas y queries:** Código exacto ejecutado (KQL/VQL) incluyendo filtros del SIEM.
    
- **Mapeo MITRE ATT&CK:** Identificar las fuentes de datos (Data Sources) sugeridas por el framework para la técnica investigada.
    

### **IV. Evidencias y resultados**

- **Eventos detectados:** IPs, dominios, procesos, usuarios y timestamps.
    
- **Indicadores de Compromiso (IoCs):** Hashes, mutexes o cadenas detectadas.
    
- **MITRE ATT&CK (TTPs):** Mapeo específico de la Táctica (ej. TA0003) y Técnica (ej. T1543.003).
    
- **Modelo Diamante (Capacidades):** Describir las herramientas o exploits (Capacidades) que el adversario utilizó para generar la evidencia encontrada.
    

### **V. Análisis y conclusiones**

- **Interpretación:** Por qué los hallazgos son relevantes o benignos.
    
- **Validación:** Confirmación de la hipótesis (validada o descartada).
    
- **Impacto:** Alcance potencial del compromiso en la organización.
    
- **Correlación de Modelos:** Resumen de cómo el **Adversario** (Diamante) avanzó a través de la **Kill Chain** usando técnicas de **ATT&CK**.
    

### **VI. Recomendaciones y acciones**

- **Contención y Mitigación:** Medidas inmediatas para detener la amenaza.
    
- **Actualización de Detección:** Conversión de la query de hunting en una regla de alerta permanente en el SIEM.
    
- **Lecciones aprendidas:** Análisis de brechas (Gap Analysis) para fortalecer futuras investigaciones.
    

---

## 3. Matriz de Aplicación de Modelos

|**Paso del Reporte**|**Modelo Diamante**|**Cyber Kill Chain**|**MITRE ATT&CK**|
|---|---|---|---|
|**Identificación**|Adversario / Víctima|-|-|
|**Hipótesis**|-|Fase del Ataque|-|
|**Fuentes de Datos**|Infraestructura|-|Data Sources|
|**Evidencias**|Capacidades|-|Tácticas / Técnicas|
|**Conclusiones**|Relación Adversario-Infra|Progreso del Intruso|Comportamiento (TTP)|
|**Acciones**|Bloqueo de Infra|Romper la Cadena|Mitigación de Técnicas|

---

## 4. Plantilla Maestra para Obsidian (Markdown Técnico)


```markdown
# [HUNT-ID] - [Título del Hallazgo]
**Analista:** beathunterzero | **Entorno:** [Ej. MultiCloud/Fedora Lab]

## 1. Identificación y Modelo Diamante
- **Adversario:** [Nombre/Perfil] | **Infraestructura:** [IPs/Dominios]
- **Víctima:** [Activo Crítico] | **Capacidad:** [Herramienta detectada]

## 2. Hipótesis y Cyber Kill Chain
- **Hipótesis:** [Suposición técnica]
- **Fase de la Cadena:** [Ej. Comando y Control / Exfiltración]

## 3. Fuentes de Datos y Queries
- **Logs:** [Ej. Sysmon / DNS Logs]
- **Query:** ```kql
// Query técnica aquí

## 4. Evidencias y MITRE ATT&CK

- **Táctica/Técnica:** [Ej. TA0005 - T1071.004]
    
- **IoCs:** [Lista de artefactos confirmados]
    

## 5. Análisis y Conclusiones

- **Interpretación:** [Análisis forense del hallazgo]
    
- **Hipótesis:** [Validada / Descartada]
    

## 6. Recomendaciones y Acciones

- **Contención:** [Pasos inmediatos]
    
- **Ingeniería de Detección:** [Lógica para la nueva regla de alerta]
    

```

---

### Referencias
* [MITRE ATT&CK Framework](https://attack.mitre.org/)
* [Lockheed Martin Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)
* [Diamond Model for Intrusion Analysis](https://www.activeresponse.org/wp-content/uploads/2013/07/diamond_model.pdf)

### Documentación Relacionada

[[01 - Madurez y métricas de hunting]]
