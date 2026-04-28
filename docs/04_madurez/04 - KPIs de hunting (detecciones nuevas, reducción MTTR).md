## 1. Propósito

Los KPIs en Threat Hunting existen para responder una pregunta:

> **¿El hunting está mejorando la capacidad de detección del SOC o solo genera actividad?**

El valor no está en “cazar”, sino en:

- Reducir tiempos de detección y respuesta
    
- Aumentar cobertura de TTPs
    
- Generar detecciones reutilizables
    

---

## 2. Principio Operativo

> Un programa de hunting maduro se mide por lo que automatiza, no por lo que investiga.

---

## 3. KPIs Clave (Correctos y Accionables)

---

### 1. Conversión de Detecciones (Detection Conversion Rate)

- **Definición:**  
    % de hunts que terminan en una regla productiva
    
- **Por qué importa:**  
    Mide si el hunting genera valor real
    
- **Objetivo:**  
    Aumentar progresivamente
    

---

### 2. MTTR (Mean Time to Respond)

- **Definición:**  
    Tiempo desde detección → contención
    
- **Por qué importa:**  
    Mide la capacidad de respuesta del SOC
    
- **Relación directa:**  
    SIEM (detección) + SOAR (respuesta)
    

---

### 3. MTTD (Mean Time to Detect)

- **Definición:**  
    Tiempo desde compromiso → detección
    
- **Por qué importa:**  
    Reduce el _dwell time_
    

---

### 4. Time to Rule (TTRu)

- **Definición:**  
    Tiempo desde hallazgo → regla en producción
    
- **Por qué importa:**  
    Mide la velocidad de ingeniería de detección
    

---

### 5. Precisión de Detección

- **Definición:**  
    % de alertas válidas vs falsos positivos
    
- **Por qué importa:**  
    Impacta directamente en fatiga del analista
    

---

### 6. Cobertura de TTPs

- **Definición:**  
    % de técnicas cubiertas en MITRE ATT&CK
    
- **Por qué importa:**  
    Mide visibilidad real, no volumen de logs
    

---

## 4. KPIs que debes evitar o reinterpretar

Eliminar o reducir:

- Uso del Diamond Model en métricas
    
- Uso de Kill Chain como indicador
    
- KPIs teóricos sin impacto operativo
    

---

## 5. Fórmulas Operativas

---

### Tasa de Conversión

Conversion\ Rate = \frac{Detections\ Created}{Hunts\ Executed} \times 100

---

### MTTR

MTTR = \frac{\sum Response\ Time}{Total\ Incidents}

---

### MTTD

MTTD = \frac{\sum Detection\ Time}{Total\ Incidents}

---

### Time to Rule

TTRu = \frac{\sum Time\ to\ Production}{Total\ Detections}

---

## 6. Interpretación Correcta

- **Alta conversión + bajo TTRu →** equipo eficiente
    
- **Bajo MTTR →** buena automatización (SOAR)
    
- **Alto MTTD →** problema en detección
    
- **Alta cobertura MITRE →** reducción de puntos ciegos
    

---

## 7. Uso Real en el SOC

Estos KPIs deben alimentar:

- Dashboards operativos
    
- Reportes de madurez
    
- Priorización de hunts
    
- Roadmap de detección
    

---

## 8. Conclusión Técnica

Los KPIs no son métricas decorativas.

---

### Principio final

> Si no puedes medirlo, no puedes mejorar el hunting.

---

## Referencias Externas

- [https://attack.mitre.org/](https://attack.mitre.org/)
    
- [https://attack.mitre.org/resources/working-with-attack/](https://attack.mitre.org/resources/working-with-attack/)
    
- [https://www.sans.org/white-papers/37702/](https://www.sans.org/white-papers/37702/)
    

---

## Documentación Relacionada

[[01 - Madurez y métricas de hunting]]  
[[02 - Documentar hallazgos (Metodología Integral)]]  
[[03 - Conversión de hunts en casos de uso para SIEM y SOAR]]  
[[05 - Threat Hunting en SIEM]]