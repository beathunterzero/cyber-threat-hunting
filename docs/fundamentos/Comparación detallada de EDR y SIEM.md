## 1. Definición y Propósito

En un entorno de **Cyber Threat Hunting**, es vital distinguir entre la visión macro que ofrece el SIEM y la visibilidad granular (micro) que proporciona el EDR. Ambas herramientas son complementarias y necesarias para cubrir el espectro completo de una intrusión.

## 2. Matriz Comparativa: SIEM vs. EDR

|**Característica**|**SIEM (Gestión de Eventos e Información)**|**EDR (Detección y Respuesta de Endpoints)**|
|---|---|---|
|**Enfoque**|Visión amplia de la postura de seguridad organizacional. Agrega datos de red, servidores y dispositivos.|Centrado exclusivamente en puntos finales (laptops, desktops, servidores).|
|**Capacidades Clave**|Agregación, correlación en tiempo real y retención de datos a largo plazo para cumplimiento/histórico.|Monitoreo continuo de actividades, análisis de comportamiento y respuesta automatizada.|
|**Análisis de Datos**|Recopila y normaliza datos de fuentes diversas. Proporciona una visión a nivel macro.|Recopila datos detallados y granulares del dispositivo. Identifica actividades maliciosas por comportamiento.|
|**Respuesta**|Genera alertas y facilita la intervención manual. Se integra con otras herramientas para coordinación.|Respuestas inmediatas y automatizadas: cuarentena de archivos, eliminación de procesos o aislamiento del host.|
|**Casos de Uso**|Visibilidad integral, cumplimiento, detección de amenazas internas y violaciones de red.|Combate efectivo contra Ransomware, exploits de día cero y Amenazas Persistentes Avanzadas (APT).|
|**Escalabilidad**|Se adapta a volúmenes crecientes de datos de toda la infraestructura.|Se escala según el número de puntos finales (agentes) desplegados.|

## 3. Implementación en el Laboratorio: Elastic Security vs. Velociraptor

Para tu entorno de CTH, estas herramientas materializan los conceptos anteriores con las siguientes funciones técnicas:

### **Elastic Security (SIEM)**

- **Ingesta Masiva:** Uso de **Beats** y **Logstash** para centralizar telemetría de diversas fuentes.
    
- **Correlación Avanzada:** Uso de **KQL (Kibana Query Language)** para buscar patrones en múltiples índices.
    
- **Automatización:** **Detection Engine** basado en reglas YAML para disparar alertas sobre TTPs conocidos.
    
- **Inteligencia de Amenazas:** **Machine Learning (ML)** para detectar anomalías, como picos inusuales de conexiones DNS hacia dominios sospechosos.
    
- **Mapeo:** Clasificación automática de eventos bajo el framework de **MITRE ATT&CK**.
    

### **Velociraptor (EDR)**

- **Caza Forense:** Uso de **VQL (Velociraptor Query Language)** para tareas específicas como listar DLLs sospechosas cargadas en memoria o recolectar el historial de PowerShell.
    
- **Persistencia:** Artefactos de VQL diseñados para detectar **Run Keys** o creación de **Scheduled Tasks** en tiempo real.
    
- **Línea de Tiempo:** Reconstrucción de incidentes mediante **Timelines Forenses** detallados del endpoint.
    
- **Acción Directa:** Permite ejecutar acciones de contención y aislamiento de dispositivos comprometidos desde la consola.
    
- **Enriquecimiento:** Caza activa de endpoints que contactan dominios presentes en listas negras externas (Feeds de CTI).
    

## 4. Nota sobre la Sinergia Operativa

> [!IMPORTANT]
> 
> El Threat Hunter no debe elegir entre una u otra. El **SIEM** se utiliza para detectar la anomalía inicial o el "hilo" de la investigación (ej. una alerta de correlación). Una vez identificado el host afectado, se utiliza el **EDR** para realizar la cirugía forense profunda, recuperar artefactos y ejecutar la remediación.

---

### Referencias Externas

- [Elastic Security: SIEM Documentation](https://www.elastic.co/guide/en/security/current/index.html)
    
- [Velociraptor: VQL Reference & Artifacts](https://www.google.com/search?q=https://docs.velociraptor.app/artifact_references/)
    
- [MITRE ATT&CK: Enterprise Matrix](https://www.google.com/url?sa=E&source=gmail&q=https://attack.mitre.org/)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]
[[Hipótesis y casos de usos comunes]]