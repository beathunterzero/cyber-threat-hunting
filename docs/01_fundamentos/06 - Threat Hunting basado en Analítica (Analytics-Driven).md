## 1. Definición y Concepto

El **Threat Hunting basado en Analítica** es el enfoque que utiliza métodos estadísticos, algoritmos de detección de anomalías y visualización masiva de datos para identificar patrones que se desvían del comportamiento "normal" (baseline) de la red o los endpoints. Se centra en encontrar lo **desconocido-desconocido** mediante el análisis de telemetría a gran escala.

## 2. Tipos de Cacería por Analítica

Basado en la taxonomía técnica, las técnicas principales son:

- **Detección de Outliers (Valores Atípicos):** Identificación de eventos únicos o raros que se desvían drásticamente del promedio.
    
- **Análisis de Frecuencia (Stack Counting):** Técnica de apilamiento donde se cuentan ocurrencias. Los resultados con menor frecuencia (_Least Frequent Occurrences_) suelen indicar la presencia de herramientas de ataque personalizadas.
    
- **Análisis Temporal:** Identificación de patrones de balizamiento (_Beacons_) o conexiones que ocurren a intervalos exactos, sugiriendo comunicación automatizada de C2.
    

## 3. Cuadro de Objetivos y Visibilidad Analítica

Para ejecutar este hunting con éxito, el analista debe monitorear los siguientes atributos y métricas según lo establecido en el curso:

|**Objeto de Análisis**|**Métrica Analítica**|**Indicador de Amenaza**|
|---|---|---|
|**Tráfico de Red**|Volumen de bytes enviados vs. recibidos.|Posible exfiltración de datos o transferencia de archivos pesados.|
|**Autenticación**|Frecuencia de fallos por cuenta/IP en tiempo reducido.|Ataques de _Brute Force_ o _Password Spraying_.|
|**Procesos**|Relación de procesos "huérfanos" (sin padre legítimo).|Técnicas de inyección de código o persistencia.|
|**DNS**|Cantidad de subdominios únicos consultados por un solo host.|Canal de C2 mediante _DNS Tunneling_.|

## 4. El Rol de CTI en la Analítica

La Inteligencia de Amenazas (CTI) potencia la analítica al proporcionar el contexto necesario para filtrar el ruido masivo de los logs:

- **Contextualización:** Determina si una anomalía estadística coincide con comportamientos documentados de actores de amenaza conocidos.
    
- **Priorización:** Ayuda a decidir qué desviación investigar primero basándose en las amenazas activas en el sector.
    

## 5. Nota Crítica: Saturación vs. Eficiencia Operativa

> [!IMPORTANT]
> 
> **Dependencia de un equipo de CTI:** Para que el enfoque _Analytics-Driven_ sea sostenible, es imperativo que la organización cuente con un equipo de CTI dedicado.
> 
> **Saturación Laboral:** Cargar la recolección, filtrado y análisis de inteligencia externa directamente al **Threat Hunter** genera una saturación de carga laboral que degrada su capacidad de investigación técnica. Un Hunter saturado se convierte en un analista reactivo de feeds. La madurez del SOC se alcanza cuando CTI actúa como el radar (detección externa) y el Hunter como el interceptor (investigación interna).

## 6. Flujo Operativo: Del Dato a la Amenaza

1. **Agregación de Telemetría:** Recolección desde **Elastic Security** y **Velociraptor**.
    
2. **Normalización:** Asegurar consistencia en los campos para permitir la correlación cruzada.
    
3. **Visualización:** Uso de dashboards para detectar picos de actividad o patrones visuales anómalos.
    
4. **Enriquecimiento:** Cruzar las anomalías con fuentes de inteligencia para confirmar la amenaza.
    

---

### Referencias Externas

- SANS: Applied Resources for Data Analytics in Threat Hunting.
    
- Kibana Guide: Analyzing Data with Discover and Lens.
    

### Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]
[[04 - Threat Hunting basado en IoCs (IoC-Driven)]]
[[05 - Threat Hunting basado en Hipótesis (Hypothesis-Driven)]]