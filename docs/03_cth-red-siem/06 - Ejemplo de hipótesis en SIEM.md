## 1. Ejemplos de hipótesis

Las hipótesis deben ser:

- Específicas
    
- Basadas en CTI
    
- Accionables
    

---

### 1.1 Actor (Lazarus)

**Contexto:**

- Actor relevante según CTI
    
- TTPs conocidos en MITRE
    

**Hipótesis:**

- Presencia del actor → evidencia de sus TTPs
    

---

### 1.2 Malware (WannaCry)

**Contexto:**

- Uso de SMBv1
    
- Riesgo de ransomware
    

**Hipótesis:**

- Incremento anómalo de cambios de archivos
    

---

### 1.3 Técnica (MS17-010)

**Contexto:**

- Vulnerabilidad explotable (EternalBlue)
    

**Hipótesis:**

- Tráfico SMB con patrones anómalos
    

---

## 2. Crown Jewels Analysis (CJA)

Define dónde priorizar hunting.

Pasos:

1. Identificar objetivos del negocio
    
2. Mapear activos críticos
    
3. Inventariar infraestructura
    
4. Analizar rutas de ataque
    

---

## 3. Flujo de hunting

### Entradas

- CTI
    
- Contexto
    
- Experiencia
    

---

### Proceso

1. Crear hipótesis
    
2. Priorizar
    
3. Diseñar analítica
    
4. Investigar
    

---

### Resultados

- No concluyente → falta de datos
    
- Malicioso → IR
    
- Sospechoso → revisión
    

---

## 4. Queries (KQL)

### 4.1 Exfiltración

```kql
FROM logs-*
| WHERE network.direction IN ("egress","outbound","external")
| STATS bytes_out=SUM(network.bytes) BY source.ip, destination.ip
| WHERE bytes_out > 1000000
```

---

### 4.2 DNS Tunneling

```kql
FROM logs-*
| WHERE network.protocol == "dns"
| WHERE LENGTH(dns.question.name) > 100
```

---

### 4.3 HTTP sospechoso

```kql
FROM logs-*
| WHERE network.protocol == "http"
| WHERE http.request.mime_type == "text/plain"
| WHERE LENGTH(TO_STRING(http.request.body.bytes)) > 1000
```

---

## 5. Enfoque de hunting

- Basar hipótesis en amenazas reales
    
- Priorizar activos críticos
    
- Validar con datos
    
- Iterar continuamente
    

---

## Referencias Externas

- [https://attack.mitre.org/groups/G0032/](https://attack.mitre.org/groups/G0032/)
    
- [https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010](https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[05 - Threat Hunting en SIEM]]