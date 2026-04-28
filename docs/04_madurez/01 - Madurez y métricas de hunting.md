## 1. Definición

La **madurez en Threat Hunting** representa la capacidad de una organización para ejecutar cacerías de forma:

- **Consistente** (repetible)
    
- **Medible** (basada en métricas reales)
    
- **Evolutiva** (mejora continua)
    

No se mide por cuántas amenazas se encuentran, sino por:

> Qué tan sistemáticamente el hunting se convierte en detección operativa.

---

## 2. Enfoque Correcto

El Threat Hunting no debe evaluarse como actividad aislada, sino como parte del ciclo de **Detection Engineering**:

**Flujo real:**

CTI → TTP → Telemetría → Hipótesis → Query → Detección → Métricas

---

### Principio operativo

> El valor del hunting no está en el hallazgo, sino en su conversión a detección repetible.

---

## 3. Métricas Clave (KPIs)

Las métricas se ajustan a un enfoque operativo real, eliminando ruido y priorizando impacto:

|**#**|**Métrica**|**Descripción Técnica**|**Objetivo Operativo**|
|---|---|---|---|
|**01**|**MTTD (Mean Time to Detect)**|Tiempo desde la actividad maliciosa hasta su detección.|Reducir el dwell time del atacante.|
|**02**|**MTTR (Mean Time to Respond)**|Tiempo desde detección hasta contención.|Minimizar impacto del incidente.|
|**03**|**Detection Yield**|Porcentaje de hunts que terminan en detecciones productivas.|Asegurar impacto real del hunting.|
|**04**|**False Positive Rate (FPR)**|Nivel de ruido generado por detecciones.|Reducir fatiga del SOC.|
|**05**|**Cobertura de TTPs**|Cobertura de técnicas relevantes en MITRE ATT&CK.|Reducir puntos ciegos.|
|**06**|**Time to Production**|Tiempo en convertir un hunt en regla activa.|Acelerar defensa operativa.|
|**07**|**Reusabilidad de Queries**|Porcentaje de queries reutilizables.|Optimizar eficiencia del equipo.|

---

## 4. Métrica Crítica

### Detection Yield

> % de hunts que terminan en detección real

---

### Interpretación

- Bajo → Hunting sin impacto
    
- Alto → Hunting alineado a detección
    

---

## 5. Modelo de Madurez (Operativo)

### Nivel 1 — Reactivo

- Dependencia total de alertas
    
- Sin hipótesis
    
- Sin métricas
    

---

### Nivel 2 — Exploratorio

- Hunts manuales
    
- Sin estandarización
    
- Bajo impacto en detección
    

---

### Nivel 3 — Estructurado

- Hipótesis definidas
    
- Queries reutilizables
    
- Métricas iniciales
    

---

### Nivel 4 — Integrado

- Hunting → detecciones automáticas
    
- Cobertura basada en TTPs
    
- Métricas activas
    

---

### Nivel 5 — Optimizado

- Hunting continuo
    
- Automatización avanzada
    
- Métricas guían decisiones
    

---

## 6. Qué NO medir (Corrección)

Eliminar métricas que no aportan valor:

- Número de hunts ejecutados
    
- Número de alertas generadas
    
- Cantidad de IoCs consumidos
    

---

## 7. Relación con el Negocio

### Baja madurez

- Alto MTTD
    
- Alta dependencia de vendors
    
- Respuesta reactiva
    

---

### Alta madurez

- Detección propia basada en comportamiento
    
- Reducción del dwell time
    
- Menor dependencia de IoCs
    

---

## 8. Integración con el Proceso de Hunting

Este documento se integra con el flujo completo:

- [[10 - Convertir inteligencia en hipótesis de hunting]] → Entrada (CTI → hipótesis)
    
- [[05 - Threat Hunting en SIEM]] → Ejecución en logs centralizados
    
- [[06 - Queries y hunting en EDR]] → Ejecución en endpoint
    
- [[08 - Integración con CTI]] → Fuente de inteligencia
    
- [[09 - Uso de IoCs de fuentes abiertas]] → Input táctico
    
- [[03 - Conversión de hunts en casos de uso para SIEM y SOAR]] → Salida (detección)
    
- [[02 - Documentar hallazgos (Metodología Integral)]] → Formalización
    
- [[04 - KPIs de hunting (detecciones nuevas, reducción MTTR)]] → Medición avanzada
    

---

## 9. Conclusión Técnica

La madurez en Threat Hunting no es una función aislada, es un sistema:

- Hipótesis → ejecución → validación → detección → mejora
    

---

### Principio clave

> Si un hunt no se convierte en detección, no mejora la postura de seguridad.

---

## Referencias Externas

- [https://www.sans.org/white-papers/37702/](https://www.sans.org/white-papers/37702/)
    
- [https://attack.mitre.org/resources/working-with-attack/](https://attack.mitre.org/resources/working-with-attack/)
    

---

## Documentación Relacionada

[[02 - Documentar hallazgos (Metodología Integral)]]  
[[03 - Conversión de hunts en casos de uso para SIEM y SOAR]]  
[[04 - KPIs de hunting (detecciones nuevas, reducción MTTR)]]  
[[05 - Beneficios de implementar Red Team y Blue Team]]  
[[10 - Convertir inteligencia en hipótesis de hunting]]  
[[08 - Integración con CTI]]  
[[09 - Uso de IoCs de fuentes abiertas]]  
[[05 - Threat Hunting en SIEM]]  
[[06 - Queries y hunting en EDR]]  
[[01 - Filosofía y estrategia del Threat Hunting]]