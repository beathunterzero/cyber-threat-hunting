## 1. Definición y Enfoque Operativo

El análisis de logs de red y de sistema es la piedra angular del Threat Hunting moderno. Este proceso consiste en inspeccionar registros de tráfico y acceso para identificar comportamientos que se desvían de los patrones normales (baselines), permitiendo detectar intrusiones, movimientos laterales o canales de comando y control (C2) que las herramientas automatizadas podrían omitir.

---

## 2. Matrices de Caza por Fuente de Datos

### **I. Logs de Firewall: C2 y Puertos Inusuales**

Se centra en la telemetría de red a nivel de capa de transporte para identificar comunicaciones salientes no autorizadas.

|**Pilar**|**Detalle Operativo**|
|---|---|
|**Objetivo**|Identificar conexiones salientes sospechosas hacia direcciones IP externas desconocidas o mediante puertos no estándar.|
|**Procedimiento**|Filtrar tráfico saliente hacia países fuera del ámbito operativo, puertos altos (8080-65535) o protocolos inusuales (ICMP para datos). Cruzar IPs con feeds de inteligencia de amenazas.|
|**Ejemplo de Hallazgo**|Un host interno mantiene conexiones periódicas al puerto 8082 de una IP desconocida, indicando un posible **beaconing de C2**.|

---

### **II. Logs de Proxy: Tráfico Web (HTTP/HTTPS) Anómalo**

Analiza el tráfico de capa de aplicación para detectar el uso de la web como vector de exfiltración o túnel.

|**Pilar**|**Detalle Operativo**|
|---|---|
|**Objetivo**|Detectar exfiltración de datos o el uso de túneles encubiertos dentro del tráfico web legítimo.|
|**Procedimiento**|Revisar URLs con patrones sintácticos extraños, dominios de reciente creación (DGA) o User-Agents inusuales. Analizar picos en peticiones POST y grandes volúmenes de salida.|
|**Ejemplo de Hallazgo**|Un equipo realiza múltiples peticiones HTTPS a un dominio con subdominios aleatorios y alto volumen de salida, evidenciando un **túnel HTTP**.|

---

### **III. Logs de Autenticación: Movimiento Lateral y Fuerza Bruta**

Enfocado en el abuso de identidad y la expansión del atacante dentro del perímetro.

|**Pilar**|**Detalle Operativo**|
|---|---|
|**Objetivo**|Detectar accesos no autorizados, compromiso de cuentas o desplazamientos entre sistemas.|
|**Procedimiento**|Buscar ráfagas de intentos fallidos seguidos de un éxito (Brute Force/Password Spraying). Analizar logins desde IPs inusuales o en horarios fuera de la jornada laboral.|
|**Ejemplo de Hallazgo**|Un usuario administrativo se autentica en un servidor de base de datos crítico al que nunca había accedido, sugiriendo **movimiento lateral**.|

---

### **IV. Logs de Endpoint y Sistema: Malware y LOLBins**

Monitoreo directo del comportamiento del sistema operativo y la ejecución de procesos.

|**Pilar**|**Detalle Operativo**|
|---|---|
|**Objetivo**|Identificar la ejecución de malware, binarios legítimos usados para fines maliciosos (LOLBins) o scripts ofuscados.|
|**Procedimiento**|Analizar registros de procesos (Sysmon/EDR) buscando `powershell.exe`, `wscript.exe` o `cmd.exe` con parámetros en Base64. Monitorear cambios en el registro y persistencia.|
|**Ejemplo de Hallazgo**|Ejecución de PowerShell desde un directorio temporal (`%TEMP%`) con argumentos ofuscados y conexión posterior a una IP externa (fase de **post-explotación**).|

---

## 3. Correlación de Hallazgos (Use Cases)

Para aumentar la fidelidad de las alertas, el Hunter debe buscar la intersección de estos logs:

1. **Firewall + Endpoint:** Un proceso inusual (Endpoint) genera una conexión a un puerto alto (Firewall).
    
2. **Proxy + Autenticación:** Un login exitoso desde una IP externa (Autenticación) es seguido por la descarga de un script desde un dominio nuevo (Proxy).
    

---

### Referencias Externas

- [MITRE ATT&CK: Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008/)
    
- [SANS Institute: Log Management and Analysis Guide](https://www.sans.org/white-papers/33314/)
    
- [OWASP: Logging and Monitoring Guide](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]
