## 1. ¿Qué es Cyber Kill Chain?

El **Cyber Kill Chain** es un modelo que describe las **fases de un ataque dirigido**.

En Threat Hunting se usa para:

- Entender **en qué etapa está el atacante**
    
- Definir **qué buscar en cada fase**
    
- Priorizar puntos de detección
    

---

## 2. Fases del ataque

### 2.1 Reconnaissance (Reconocimiento)

- **Actividad:** OSINT, escaneo de puertos
    
- **Hunting:**
    
    - Logs de firewall
        
    - Tráfico externo anómalo
        

---

### 2.2 Weaponization (Preparación)

- **Actividad:** creación de payload
    
- **Nota:**
    
    - No es visible directamente
        
    - Sirve como contexto
        

---

### 2.3 Delivery (Entrega)

- **Actividad:** phishing, descarga web
    
- **Hunting:**
    
    - Logs de correo
        
    - Proxy / URLs sospechosas
        

---

### 2.4 Exploitation (Explotación)

- **Actividad:** ejecución de código
    
- **Hunting:**
    
    - Creación de procesos (4688)
        
    - Actividad anómala en endpoint
        

---

### 2.5 Installation (Instalación)

- **Actividad:** persistencia
    
- **Hunting:**
    
    - Sysmon Event ID 1 (procesos)
        
    - Sysmon Event ID 13 (registro)
        
    - Event ID 7045 (servicios)
        

---

### 2.6 Command & Control (C2)

- **Actividad:** comunicación externa
    
- **Hunting:**
    
    - NetFlow
        
    - DNS tunneling
        
    - Beaconing
        

---

### 2.7 Actions on Objectives

- **Actividad:** exfiltración, cifrado
    
- **Hunting:**
    
    - Transferencias grandes
        
    - RDP interno anómalo
        

---

## 3. Uso en Threat Hunting

- Permite mapear el ataque por **etapas**
    
- Facilita detectar **actividad parcial**
    
- Ayuda a construir hipótesis por fase
    

---

## 4. Ejemplo práctico (C2)

**Hipótesis:**  
Conexiones periódicas hacia dominios no categorizados indican posible beaconing.

**Consulta (KQL):**

```kql
DeviceNetworkEvents
| where Timestamp > ago(24h)
| summarize ConnectionCount = count() by RemoteUrl, bin(Timestamp, 1m)
| where ConnectionCount > 10
| order by ConnectionCount desc
```

---

## 5. Limitaciones

- Modelo **lineal** (no refleja ataques modernos complejos)
    
- No cubre bien:
    
    - ataques fileless
        
    - movimientos internos no secuenciales
        

---

## 6. Kill Chain vs MITRE ATT&CK

- **Kill Chain:**
    
    - Fase del ataque (visión estratégica)
        
- **MITRE ATT&CK:**
    
    - Técnica específica (visión técnica)
        

Uso combinado:

- Kill Chain → dónde mirar
    
- MITRE → qué buscar
    

---

## Referencias Externas

- [https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)
    
- [https://www.sans.org/white-papers/36082/](https://www.sans.org/white-papers/36082/)
    
- [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-150.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-150.pdf)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[07 - MITRE ATT&CK como guía de CTH]]  
[[09 - Modelo Diamante como guía de CTH]]