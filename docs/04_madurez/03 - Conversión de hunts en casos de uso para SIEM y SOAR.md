## 1. Sinergia Defensiva: SIEM + SOAR

La evolución de un _hunt_ (búsqueda manual) a un caso de uso (detección automática) requiere entender el rol de cada herramienta en el ecosistema de seguridad:

|**Aspecto**|**SIEM (Security Information & Event Management)**|**SOAR (Security Orchestration, Automation & Response)**|
|---|---|---|
|**Enfoque Principal**|Analiza datos de seguridad y proporciona _insights_ de amenazas.|Automatiza flujos de respuesta y aumenta la eficiencia.|
|**Automatización**|Limitada a la recolección y alertas básicas.|Alta automatización de incidentes; reduce tareas manuales.|
|**Integración**|Se integra con fuentes de logs.|Fuerte integración entre herramientas (comunicación fluida).|
|**Respuesta a Incidentes**|Genera alertas; requiere intervención humana.|Gestión centralizada; acelera el tiempo de respuesta.|
|**Escalabilidad**|Consume muchos recursos en despliegues grandes.|Altamente adaptable y escalable.|

---

## 2. Proceso de Conversión (Ciclo de Vida)

El camino para fortalecer la defensa proactiva sigue este flujo:

**Discover (Descubrir) $\rightarrow$ Define (Definir) $\rightarrow$ Develop (Desarrollar) $\rightarrow$ Test (Probar) $\rightarrow$ Deploy (Desplegar)**

---

## 3. Estructura de Documentación de Conversión (6 Pasos Integrados)

### **I. Identificación del caso (Discover)**

- **ID de Conversión:** Vinculación del ID del _hunt_ con el nuevo ID del caso de uso en SIEM/SOAR.
    
- **Modelo Diamante (Activos):** Identificar la **Víctima** (activos críticos) que el SIEM debe monitorear y la **Infraestructura** (nodos/IPs) que el SOAR debe ser capaz de bloquear automáticamente.
    

### **II. Hipótesis y objetivo (Define)**

- **De Hipótesis a Regla:** Transformar la suposición del _hunt_ en una lógica de detección permanente.
    
- **Cyber Kill Chain:** Definir en qué fase de la cadena de ataque actúa esta nueva regla (ej. si detecta **Explotación**, el SIEM alerta; si es **C2**, el SOAR bloquea el tráfico).
    

### **III. Fuentes de datos utilizadas (Develop)**

- **Normalización:** Asegurar que los logs (Firewall, EDR, Proxy) estén correctamente mapeados en el SIEM.
    
- **Integración SOAR:** Definir qué APIs o conectores son necesarios para que el SOAR ejecute acciones de respuesta basadas en los datos del SIEM.
    
- **MITRE ATT&CK (Data Sources):** Consultar el framework para asegurar que estamos recolectando la telemetría necesaria para la técnica específica.
    

### **IV. Evidencias y resultados (Develop & Test)**

- **Abstracción de Patrones:** Identificar los TTPs de **MITRE ATT&CK** detectados en el _hunt_ para crear firmas de comportamiento.
    
- **Modelo Diamante (Capacidades):** Documentar qué herramientas del adversario (Capacidades) se detectaron para configurar "playbooks" en el SOAR que neutralicen esas herramientas específicamente.
    

### **V. Análisis y conclusiones (Test & Tuning)**

- **Validación de Alertas:** Probar la regla en el SIEM para medir la tasa de falsos positivos.
    
- **Correlación de Modelos:** Verificar que la automatización del SOAR rompa la **Cyber Kill Chain** de manera efectiva basándose en la relación **Adversario-Infraestructura** del Diamante.
    

### **VI. Recomendaciones y acciones (Deploy & Feedback)**

- **Despliegue (Deploy):** Implementación de la regla en producción.
    
- **Acciones SOAR:** Configuración de la respuesta automática (ej. aislamiento de host, reseteo de credenciales).
    
- **Gap Analysis Continuo:** Retroalimentar el proceso para identificar qué nuevas técnicas de ATT&CK siguen sin cobertura.
    

---

## 4. Plantilla de Caso de Uso para Obsidian

```markdown
# [UC-ID] - Conversión de Hunt: [HUNT-ID]
**Estado:** [Desarrollo / Producción] | **Componentes:** [SIEM + SOAR]

## 1. Inteligencia del Modelo Diamante
- **Infraestructura a Bloquear:** [IoCs detectados]
- **Capacidad Mitigada:** [Herramienta del atacante]

## 2. Lógica de Detección (SIEM)
- **Táctica MITRE:** [Ej. TA0011 - Command and Control]
- **Fase Kill Chain:** [Ej. Comando y Control]
- **Query de Producción:**
```kql
// Insertar query optimizada aquí

## 3. Playbook de Respuesta (SOAR)

- **Trigger:** Alerta de [UC-ID]
    
- **Acciones:**
    
    1. Bloquear IP en Firewall perimetral.
        
    2. Aislar endpoint vía EDR.
        
    3. Notificar al analista de guardia.
        

## 4. Feedback y Mejora Continua

- **Falsos Positivos detectados:** [Detalles]
    
- **Ajuste de umbral:** [Métrica]
    
```

---

### Referencias
* [SIEM vs SOAR: Gartner Market Guide](https://www.gartner.com/)
* [MITRE ATT&CK: Data Sources for Detection](https://attack.mitre.org/datasources/)
* [Diamond Model in SOC Automation](https://www.activeresponse.org/)

### Documentación Relacionada

[[01 - Madurez y métricas de hunting]]