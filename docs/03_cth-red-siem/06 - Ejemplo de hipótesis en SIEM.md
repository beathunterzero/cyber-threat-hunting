## 1. Ejemplos de Hipótesis Basadas en Amenazas

La formulación de hipótesis debe ser específica y basarse en inteligencia real (CTI) para ser efectiva.

### **Escenario A: Actor de Amenazas (Grupo Lazarus)**

- **Contexto:** Una evaluación de amenazas organizacionales identificó al **Grupo Lazarus** como una amenaza de alta prioridad. Las técnicas atribuidas a este actor están detalladas en el Navegador de MITRE ATT&CK.
    
- **Hipótesis:** _"Si este actor de amenazas está presente en nuestra red, seremos capaces de detectar evidencia de múltiples técnicas desplegadas de manera consistente con sus rutas de ataque conocidas"._
    

### **Escenario B: Herramienta (WannaCry Ransomware)**

- **Contexto:** La CTI y nuestra conciencia situacional sugieren que la organización es vulnerable a una variante de **WannaCry**, ya que todavía se utiliza el protocolo **SMBv1**.
    
- **Hipótesis:** _"Si nuestra red está infectada con WannaCry, observaremos un aumento anómalo en la tasa de cambio de nombre de archivos (renaming) en los sistemas afectados"._
    

### **Escenario C: Técnica (Movimiento Lateral vía MS17-010)**

- **Contexto:** El movimiento lateral mediante la explotación de servicios remotos puede realizarse explotando la vulnerabilidad **MS17-010** (EternalBlue). Específicamente, mediante módulos de Metasploit que utilizan peticiones SMB de un tamaño específico.
    
- **Hipótesis:** _"Podemos detectar evidencia de esta técnica aislando peticiones SMB con tamaños de paquete específicos y anómalos en nuestros logs de red"._
    

---

## 2. Análisis de Activos Críticos (Crown Jewels Analysis - CJA)

El CJA es un proceso fundamental para priorizar dónde cazar. Se compone de los siguientes pasos:

1. **Identificar las misiones centrales:** Determinar los objetivos principales de la organización.
    
2. **Mapeo de activos e información:** Identificar los datos y activos de los que dependen dichas misiones.
    
3. **Documentación de activos de red:** Registrar formalmente todos los activos tecnológicos utilizados.
    
4. **Construcción de grafos de ataque:** Determinar dependencias, analizar rutas de ataque y calificar la severidad de las vulnerabilidades.
    

---

## 3. Flujo de Trabajo: Detectando lo Desconocido

El proceso de Threat Hunting es un ciclo de retroalimentación constante:

- **Insumos:** Inteligencia de Amenazas (CTI), Conciencia Situacional y Experiencia de Dominio.
    
- **Proceso:** 1. **Crear Hipótesis.**
    
    2. **Priorizar Hipótesis** (según recursos disponibles).
    
    3. **Informar y Enriquecer Analíticas.**
    
    4. **Investigar** mediante herramientas y técnicas (SOC Analysts).
    
- **Resultados:**
    
    - **No Probada:** ¿Necesitamos mejorar la visibilidad de los datos?
        
    - **Maliciosa:** Descubrimiento de nuevos patrones y TTPs $\rightarrow$ Respuesta a Incidentes (CIR).
        
    - **Sospechosa/Riesgosa:** Gestión de Vulnerabilidades.
        

---

## 4. Queries en Elastic Security (KQL)

Aquí tienes las consultas optimizadas para detectar los escenarios discutidos:

### **1. Detección de transferencias masivas de datos (Exfiltración)**

Esta consulta identifica conexiones donde se transfieren grandes volúmenes de datos hacia el exterior sumando los bytes de red.

Fragmento de código

```kql
FROM logs-*
| WHERE network.direction IN("egress","outbound","external")
| STATS bytes_out=SUM(network.bytes), protocols=VALUES(network.protocol), first_seen=MIN(@timestamp), last_seen=MAX(@timestamp) BY source.ip, destination.ip
| WHERE bytes_out > 1000000
| KEEP first_seen, last_seen, source.ip, destination.ip, protocols, bytes_out
```

### **2. Identificación de consultas DNS inusualmente largas (Tunneling)**

Detecta consultas DNS excesivamente largas, un indicador clásico de túneles DNS utilizados para exfiltración encubierta.

Fragmento de código

```kql
FROM logs-*
| WHERE network.protocol == "dns"
  AND LENGTH(dns.question.name) > 100
| KEEP source.ip, dns.question.name, @timestamp
```

### **3. Detección de payloads codificados en tráfico HTTP**

Identifica cuerpos de peticiones HTTP inusualmente grandes en formato de texto plano, lo que puede indicar exfiltración de datos mediante cargas codificadas (Base64, etc.).

Fragmento de código

```kql
FROM logs-*
| WHERE network.protocol == "http"
  AND http.request.mime_type == "text/plain"
  AND LENGTH(TO_STRING(http.request.body.bytes)) > 1000
| KEEP source.ip, destination.domain, http.request.mime_type, http.request.body.bytes, @timestamp
```

---

### Referencias Externas

- [MITRE ATT&CK Navigator: Lazarus Group](https://attack.mitre.org/groups/G0032/)
    
- [Microsoft Security: Guía sobre MS17-010](https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
[[05 - Threat Hunting en SIEM]]