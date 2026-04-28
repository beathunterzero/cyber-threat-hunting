## 1. ¿Qué se busca?

Detectar cómo el atacante:

- Mantiene comunicación (**C2**)
    
- Extrae información (**exfiltración**)
    

Clave:

- El tráfico sale desde el endpoint comprometido
    

---

## 2. Arquitectura C2

Componentes típicos:

- **Servidor C2 (Team Server)**
    
- **Redirectores** (ocultan origen real)
    
- **Beacons** (malware que inicia conexión)
    

---

## 3. Técnicas de C2

|Técnica|Descripción|
|---|---|
|Beaconing|Conexiones periódicas|
|DGA|Dominios generados automáticamente|
|Fast Flux|IPs cambiantes|
|TLS/HTTPS|Tráfico cifrado|
|Esteganografía|Datos ocultos|

---

## 4. Técnicas de exfiltración

|Técnica|Descripción|
|---|---|
|Compresión + cifrado|Reduce y oculta datos|
|Protocolos alternativos|DNS, ICMP, FTP|
|Cloud legítimo|Drive, Dropbox|
|Programación|Horarios de bajo tráfico|
|Fragmentación|Envío en pequeñas partes|

---

## 5. Detección en DNS

Indicadores:

- TLDs inusuales
    
- Alto volumen de consultas
    
- Dominios nuevos
    

### Ejemplo (KQL)

```kql
DeviceNetworkEvents
| where ActionType == "DnsConnection"
| where RemoteUrl has_any (".xyz", ".top", ".club")
| summarize count() by RemoteUrl, DeviceId
| where count_ > 100
```

---

## 6. Indicadores clave

- Conexiones periódicas (beaconing)
    
- Tráfico cifrado hacia dominios desconocidos
    
- Uso de DNS fuera de patrón
    
- Transferencias pequeñas repetidas
    

---

## 7. Ejemplo real (ADVSTORESHELL)

Patrones observables:

- Uso de HTTP (POST) para C2
    
- Datos comprimidos y cifrados
    
- Persistencia en Run Keys
    
- Archivos temporales `.dat`
    
- Codificación Base64
    
- Cifrado (3DES / RSA)
    

---

## 8. Enfoque de hunting

- Analizar frecuencia de conexiones
    
- Correlacionar red + endpoint
    
- Detectar anomalías en DNS
    
- Validar contra baseline
    

---

## 9. Objetivo

- Detectar C2 temprano
    
- Identificar exfiltración
    
- Cortar comunicación del atacante
    

---

## Referencias Externas

- [https://attack.mitre.org/techniques/T1041/](https://attack.mitre.org/techniques/T1041/)
    
- [https://attack.mitre.org/software/S0045/](https://attack.mitre.org/software/S0045/)
    
- [https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-devicenetworkevents-table](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-devicenetworkevents-table)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]