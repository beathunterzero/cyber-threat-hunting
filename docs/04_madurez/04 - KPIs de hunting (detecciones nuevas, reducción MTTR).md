## 1. Importancia de las Métricas en el Mantenimiento de Seguridad

El éxito de un programa de hunting no se mide solo por los incidentes encontrados, sino por la capacidad de mejorar la resiliencia del SOC. El **MTTR (Mean Time to Respond)** y la **Tasa de Conversión de Reglas** son los indicadores definitivos de que el equipo está pasando de una postura reactiva a una proactiva.

---

## 2. Estructura de Documentación de KPIs (6 Pasos Integrados)

### **I. Identificación del caso**

- **ID de Métrica:** MET-HUNT-01 (Métricas de Eficiencia Operativa).
    
- **Entorno Evaluado:** Ciclo de vida de incidentes en SIEM/SOAR.
    
- **Modelo Diamante (Víctima):** El KPI mide la protección de la **Víctima** (infraestructura) reduciendo el tiempo de exposición ante el **Adversario**.
    

### **II. Hipótesis y objetivo**

- **Hipótesis Operativa:** "Un programa de hunting maduro reduce el tiempo de permanencia del atacante y automatiza la detección de TTPs conocidos".
    
- **Objetivo:** Cuantificar el retorno de inversión (ROI) del tiempo dedicado a la cacería.
    
- **Cyber Kill Chain:** El objetivo es detectar la amenaza en las fases de **Entrega** o **Explotación**, evitando que llegue a **Acciones sobre Objetivos**.
    

### **III. Fuentes de datos utilizadas**

- **Telemetría:** Timestamps de detección y respuesta en el SIEM/SOAR, registros de casos cerrados, repositorio de reglas (Git/Wiki).
    
- **Mapeo MITRE ATT&CK:** Cobertura de técnicas detectables antes vs. después del hunt.
    

### **IV. Evidencias y resultados (Los KPIs)**

De acuerdo a la inteligencia recolectada, estos son los pilares de medición:

|**KPI**|**Descripción Técnica**|**Propósito del Modelo**|
|---|---|---|
|**Conversión de Detecciones**|% de reglas nuevas que surgieron de actividades de hunting manual.|**Capacidad:** Mejora las herramientas defensivas del SOC.|
|**Reducción de MTTR**|Disminución del tiempo promedio de respuesta ante incidentes detectados proactivamente.|**Kill Chain:** Interrupción temprana de la cadena de ataque.|
|**Precisión de Hallazgos**|Tasa de hallazgos válidos vs. falsos positivos.|**Diamante:** Identificación precisa de la relación Infra-Adversario.|
|**Time to Rule (TTRu)**|Tiempo promedio para convertir un hallazgo en una regla operativa en el SIEM.|**Agilidad:** Velocidad de transferencia de conocimiento técnico.|
|**Cobertura de Amenazas**|Incremento porcentual de técnicas cubiertas en el framework MITRE ATT&CK.|**Visibilidad:** Reducción de puntos ciegos en la infraestructura.|

### **V. Análisis y conclusiones**

- **Interpretación:** Un MTTR bajo indica que el hunting está generando detecciones de alta fidelidad que el SOAR puede orquestar rápidamente.
    
- **Validación:** Si el _Time to Rule_ es alto, existe un cuello de botella en la ingeniería de detección que debe resolverse.
    
- **Correlación:** La mejora en la **Cobertura de Amenazas** (MITRE) reduce directamente las posibilidades del **Adversario** (Diamante) de avanzar sin ser detectado.
    

### **VI. Recomendaciones y acciones**

- **Contención:** Implementar playbooks de SOAR para los casos con MTTR más crítico.
    
- **Ingeniería de Detección:** Priorizar la creación de reglas para técnicas de MITRE con baja cobertura (Gap Analysis).
    
- **Mejora Continua:** Revisar trimestralmente la tasa de falsos positivos para refinar las queries de hunting.
    

---

## 3. Fórmulas de Control

Para tu seguimiento técnico, puedes usar estas métricas de rendimiento:

- **Tasa de Conversión:**
    
    $$(Nuevas Detecciones / Hunts Ejecutados) \times 100$$
    
- **MTTR Global:**
    
    $$(\sum Tiempo de Respuesta) / Nro. de Incidentes$$
    

---

### Referencias

- [SANS: Measuring and Improving SOC Performance](https://www.sans.org/)
    
- [MITRE ATT&CK: Evaluation Methodology](https://www.google.com/url?sa=E&source=gmail&q=https://attack.mitre.org/)
    

### Documentación Relacionada

[[01 - Madurez y métricas de hunting]]