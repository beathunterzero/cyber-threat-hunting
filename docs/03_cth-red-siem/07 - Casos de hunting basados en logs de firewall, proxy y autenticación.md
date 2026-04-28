## 1. ¿Qué se busca?

Detectar anomalías usando logs de:

- Red
    
- Web
    
- Autenticación
    
- Endpoint
    

Clave:

- Comparar contra baseline
    
- Identificar desviaciones
    

---

## 2. Casos por fuente

### 2.1 Firewall (red)

**Objetivo:**

- Detectar C2 y tráfico anómalo
    

**Qué buscar:**

- Conexiones a IPs desconocidas
    
- Puertos altos o no estándar
    
- Tráfico a países inusuales
    

**Ejemplo:**

- Conexiones periódicas a puerto 8082 → posible beaconing
    

---

### 2.2 Proxy (web)

**Objetivo:**

- Detectar exfiltración o túneles
    

**Qué buscar:**

- Dominios nuevos o DGA
    
- URLs anómalas
    
- User-Agents inusuales
    
- Alto volumen en POST
    

**Ejemplo:**

- HTTPS con subdominios aleatorios → túnel HTTP
    

---

### 2.3 Autenticación

**Objetivo:**

- Detectar abuso de cuentas
    

**Qué buscar:**

- Intentos fallidos + éxito
    
- Logins fuera de horario
    
- Accesos desde IPs nuevas
    

**Ejemplo:**

- Usuario admin accede a sistema no habitual
    

---

### 2.4 Endpoint

**Objetivo:**

- Detectar ejecución maliciosa
    

**Qué buscar:**

- PowerShell, cmd, wscript
    
- Uso de Base64
    
- Ejecución desde `Temp`
    

**Ejemplo:**

- PowerShell ofuscado + conexión externa
    

---

## 3. Correlación clave

### Ejemplos:

- **Endpoint + Firewall**
    
    - Proceso sospechoso → conexión externa
        
- **Proxy + Autenticación**
    
    - Login anómalo → descarga de script
        

---

## 4. Enfoque de hunting

- No analizar fuentes aisladas
    
- Correlacionar eventos
    
- Priorizar anomalías consistentes
    
- Validar contra comportamiento normal
    

---

## 5. Objetivo

- Detectar actividad evasiva
    
- Aumentar fidelidad de detección
    
- Reducir falsos positivos
    

---

## Referencias Externas

- [https://attack.mitre.org/tactics/TA0008/](https://attack.mitre.org/tactics/TA0008/)
    
- [https://www.sans.org/white-papers/33314/](https://www.sans.org/white-papers/33314/)
    
- [https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]