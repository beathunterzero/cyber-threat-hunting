## 1. Definición y Propósito

El uso de **IoCs (Indicators of Compromise)** de fuentes abiertas consiste en integrar inteligencia pública (IPs, dominios, hashes) dentro del flujo operativo del **SIEM/EDR** para:

- Detectar actividad maliciosa conocida
    
- Ejecutar búsquedas retrospectivas (_retro-hunting_)
    
- Enriquecer eventos en tiempo real
    

**Limitación estructural:**  
Los IoCs son **indicadores volátiles**, por lo que su valor depende del contexto y la velocidad de integración.

---

## 2. Modelo de Madurez en el uso de IoCs

El valor de los IoCs no está en el indicador en sí, sino en **cómo se operacionaliza**.

|**Nivel**|**Etapa de Madurez**|**Descripción Técnica y Operativa**|
|---|---|---|
|**1**|**Inicial (Matching básico)**|Búsquedas manuales o reglas simples (`equals`, `in`). Alta dependencia de feeds externos.|
|**2**|**Contextualización**|Filtrado según activos, tecnología y exposición real. Reducción de ruido.|
|**3**|**Hipótesis Proactiva**|Uso de IoCs como punto de partida para hunting basado en comportamiento.|
|**4**|**Integración Avanzada**|Automatización, enriquecimiento en pipeline y correlación con TTPs + modelos analíticos.|

---

## 3. Limitación Técnica: Pirámide del Dolor

Referencia:  
[https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)

### Interpretación operativa

- **Hashes / IPs**
    
    - Baja durabilidad
        
    - Alta rotación por parte del atacante
        
- **Dominios**
    
    - Valor intermedio
        
    - Útiles para correlación
        
- **TTPs**
    
    - Alta durabilidad
        
    - Base real del Threat Hunting
        

**Conclusión técnica:**

> Los IoCs deben evolucionar hacia comportamiento, no quedarse en coincidencias estáticas.

---

## 4. Fuentes OSINT relevantes

### 4.1 Repositorios de IoCs

- **AlienVault OTX**  
    [https://otx.alienvault.com/](https://otx.alienvault.com/)
    
- **Abuse.ch (URLhaus / MalwareBazaar)**  
    [https://abuse.ch/](https://abuse.ch/)
    
- **MISP Project**  
    [https://www.misp-project.org/](https://www.misp-project.org/)
    

### 4.2 Características clave

- Actualización continua
    
- Alta variabilidad en calidad
    
- Necesidad de validación interna
    

---

## 5. Estrategias de Uso Correcto en SIEM

### 5.1 Enriquecimiento en tiempo real

- Enriquecer eventos con:
    
    - Reputación IP
        
    - Categoría de dominio
        
- Uso en pipelines (Elastic Ingest / Sentinel Enrichment)
    

---

### 5.2 Búsqueda retrospectiva (Retro-Hunt)

Ejemplo conceptual:

- Nuevo IoC → buscar últimos 30–90 días
    
- Identificar:
    
    - Primer contacto
        
    - Frecuencia
        
    - Hosts afectados
        

---

### 5.3 Correlación con contexto

No usar:

- IoC aislado
    

Usar:

- IoC + proceso
    
- IoC + usuario
    
- IoC + comportamiento
    

---

## 6. Ejemplo de Query (KQL)

### Detección de conexiones a IoCs conocidos

```kql
DeviceNetworkEvents
| where RemoteIP in ("1.2.3.4", "5.6.7.8")
   or RemoteUrl in ("malicious-domain.com")
| summarize count() by DeviceName, RemoteIP, RemoteUrl, bin(Timestamp, 1h)
| where count_ > 5
```

### Interpretación

- Evita eventos aislados
    
- Prioriza repetición (persistencia o beaconing)
    

---

## 7. Buenas Prácticas Operativas

### 7.1 Reducción de falsos positivos

- Filtrar:
    
    - CDN legítimos
        
    - Infraestructura compartida (Cloudflare, AWS)
        

---

### 7.2 Normalización

- Uso de esquemas:
    
    - ECS (Elastic) → [https://www.elastic.co/guide/en/ecs/current/index.html](https://www.elastic.co/guide/en/ecs/current/index.html)
        

---

### 7.3 Enriquecimiento contextual

- Geolocalización
    
- ASN
    
- Categoría del dominio
    

---

### 7.4 Rotación de feeds

- Eliminar IoCs antiguos
    
- Priorizar IoCs recientes (< 7–30 días)
    

---

## 8. Integración con Threat Hunting

El flujo correcto es:

1. IoC recibido (CTI / OSINT)
    
2. Validación contextual
    
3. Retro-hunting
    
4. Correlación con eventos internos
    
5. Evolución a hipótesis
    

---

## 9. Conclusión Técnica

El uso de IoCs de fuentes abiertas es:

- Útil como punto de partida
    
- Insuficiente como estrategia principal
    

**Principio operativo:**

> IoC → contexto → comportamiento → detección duradera

---

## Referencias Externas

- [https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
    
- [https://www.cisa.gov/news-events/news/understanding-indicators-compromise](https://www.cisa.gov/news-events/news/understanding-indicators-compromise)
    
- [https://otx.alienvault.com/](https://otx.alienvault.com/)
    
- [https://abuse.ch/](https://abuse.ch/)
    
- [https://www.misp-project.org/](https://www.misp-project.org/)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[08 - Integración con CTI]]  
[[10 - Convertir inteligencia en hipótesis de hunting]]