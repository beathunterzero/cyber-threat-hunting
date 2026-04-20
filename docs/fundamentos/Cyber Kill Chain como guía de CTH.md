## 1. Definición y Propósito Operativo

El **Cyber Kill Chain**, desarrollado por Lockheed Martin, es un modelo lineal que describe las etapas críticas de un ataque dirigido (APT). En el contexto del **Threat Hunting**, este framework permite mapear la progresión del adversario e identificar puntos de detección específicos por etapa.

## 2. Las 7 Fases del Ciclo de Vida del Ataque

### 2.1 Reconnaissance (Reconocimiento)

Recopilación de información sobre la víctima.

- **Actividad:** Escaneo de puertos, OSINT.
    
- **Hunting:** Análisis de logs de firewall y anomalías en tráfico externo.
    

### 2.2 Weaponization (Armar el ataque)

Preparación del payload malicioso.

- **Nota:** Fase externa; se utiliza para entender el contexto de la amenaza.
    

### 2.3 Delivery (Entrega)

Transmisión del arma al entorno.

- **Actividad:** Phishing, Drive-by download.
    
- **Hunting:** Logs de correo, reputación de URLs en Proxy.
    

### 2.4 Exploitation (Explotación)

Ejecución del código aprovechando vulnerabilidades.

- **Hunting:** Eventos 4688, ejecución anómala de procesos y alertas de EDR.
    

### 2.5 Installation (Instalación)

Establecimiento de persistencia en el sistema.

- **Hunting:** **Sysmon Event 1** (procesos), **Event 13** (registro) y **Event 7045** (servicios).
    

### 2.6 Command & Control (C2)

Comunicación externa con la infraestructura del atacante.

- **Hunting:** Análisis de NetFlow, DNS tunneling y detección de beaconing.
    

### 2.7 Actions on Objectives (Acciones sobre objetivos)

Ejecución del objetivo final (exfiltración, cifrado).

- **Hunting:** Transferencias masivas de datos y conexiones RDP internas inusuales.
    

## 3. Análisis de Ventajas y Limitaciones

- **Ventajas:** Estructura clara para análisis estratégico y mapeo de incidentes.
    
- **Limitaciones:** Modelo lineal que no considera ataques _fileless_ complejos o movimientos internos no secuenciales.
    

## 4. Implementación en el Proceso de Hunting

### 4.1 Definición de Escenario

- **Fase elegida:** Command & Control (C2).
    
- **Hipótesis:** "Si un atacante está en fase de C2, identificaremos conexiones periódicas (beaconing) hacia dominios no categorizados".
    

### 4.2 Query de Hunting (KQL)

Ejecución de consulta para detectar alta frecuencia de conexión en intervalos cortos:

Fragmento de código

```kql
DeviceNetworkEvents
| where Timestamp > ago(24h)
| summarize ConnectionCount = count() by RemoteUrl, bin(Timestamp, 1m)
| where ConnectionCount > 10
| order by ConnectionCount desc
```

## 5. Sinergia: Kill Chain + MITRE ATT&CK

- **Cyber Kill Chain:** Define la **fase operativa** (flujo estratégico).
    
- **MITRE ATT&CK:** Define la **técnica específica** (detección táctica).
    

---

### Referencias Externas

- [Lockheed Martin: The Cyber Kill Chain Framework](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)
    
- [SANS Institute: Applying the Cyber Kill Chain to Threat Hunting](https://www.google.com/search?q=https://www.sans.org/white-papers/36082/)
    
- [NIST: Guide to Cyber Threat Information Sharing](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-150.pdf)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]
[[MITRE ATT&CK como guía de CTH]]
[[Modelo Diamante como guía de CTH]]