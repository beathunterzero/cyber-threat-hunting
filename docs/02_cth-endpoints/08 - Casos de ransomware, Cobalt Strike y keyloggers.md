## 1. Definición y Enfoque Operativo

Esta sección aplica la metodología de caza a tres de las amenazas más críticas y frecuentes en el panorama actual de la ciberseguridad. El objetivo es traducir el comportamiento de cada amenaza en anomalías detectables en la telemetría del EDR o SIEM, alejándose de la dependencia de firmas tradicionales (Hashes/IPs) y enfocándose en TTPs (Tácticas, Técnicas y Procedimientos).

## 2. Estrategias de Hunting por Amenaza

Con base en los escenarios operativos, la búsqueda debe estructurarse de la siguiente manera para cada tipo de amenaza:

### **1. Ransomware (Impacto y Cifrado)**

El ransomware no intenta ser sigiloso en su fase final; su característica principal es la destrucción o secuestro masivo de datos.

- **Comportamiento Objetivo:** Comportamientos inusuales en los archivos del sistema y procesos masivos de cifrado.
    
- **Estrategia de Caza (Hunting):** La búsqueda más eficaz debe formularse para identificar un **alto número de escrituras (writes) o modificaciones de archivos en un corto período de tiempo** originadas por un único proceso.
    
- **Indicadores Adicionales:** Eliminación de _Shadow Copies_ (`vssadmin`, `wmic shadowcopy delete`), modificación masiva de extensiones de archivos y creación de notas de rescate (archivos `.txt` o `.html` repetidos en múltiples directorios).
    

### **2. Cobalt Strike (Comando y Control / Post-explotación)**

Cobalt Strike es una herramienta comercial de emulación de adversarios (C2) ampliamente abusada por actores de amenazas avanzadas (APTs) y operadores de ransomware.

- **Comportamiento Objetivo:** Comunicación sigilosa con la infraestructura del atacante y movimiento lateral.
    
- **Estrategia de Caza (Hunting):** La búsqueda debe enfocarse en dos frentes:
    
    1. **Red:** Identificar la comunicación con sus _beacons_ (balizas), buscando patrones de _jitter_ y _sleep_ en conexiones HTTP/HTTPS o DNS hacia dominios desconocidos.
        
    2. **Endpoint:** Identificar comportamientos asociados a la **inyección de procesos** (Process Injection), como procesos legítimos (ej. `rundll32.exe`, `svchost.exe`) abriendo conexiones de red anómalas o asignando memoria de forma sospechosa.
        

### **3. Keyloggers (Robo de Credenciales y Espionaje)**

Los keyloggers, ya sean independientes o módulos de un troyano (RAT), buscan capturar información sensible directamente de la interacción del usuario.

- **Comportamiento Objetivo:** Interceptación continua de dispositivos de entrada de datos (teclado).
    
- **Estrategia de Caza (Hunting):** La búsqueda se orienta a identificar actividades sospechosas relacionadas con la captura de pulsaciones del teclado o la creación de archivos ocultos donde se almacenan esas pulsaciones para su posterior exfiltración.
    
- **APIs Críticas a Monitorear:** El Hunter debe enfocarse en el uso inusual de APIs nativas de Windows diseñadas para esta interceptación, tales como:
    
    - `SetWindowsHookEx` (Instala un "gancho" para monitorear el tráfico de mensajes del sistema).
        
    - `GetAsyncKeyState` (Determina si una tecla específica está siendo presionada en ese momento).
        

---

## 3. Matriz de Detección Rápida

|**Tipo de Amenaza**|**Foco Principal de Telemetría**|**Eventos / APIs Críticas para Correlación**|
|---|---|---|
|**Ransomware**|File System (I/O) / Procesos|Picos de `FileWrite`, borrado de backups, Sysmon Event ID 11 (FileCreate).|
|**Cobalt Strike**|Red (C2) / Memoria|Conexiones de red intermitentes, Sysmon Event ID 8 (CreateRemoteThread).|
|**Keyloggers**|Llamadas a API / File System|`SetWindowsHookEx`, `GetAsyncKeyState`, archivos `.log` o `.dat` ocultos en `AppData`.|

---

### Referencias Externas

- [MITRE ATT&CK: Data Encrypted for Impact (T1486)](https://attack.mitre.org/techniques/T1486/)
    
- [MITRE ATT&CK: Input Capture / Keylogging (T1056.001)](https://attack.mitre.org/techniques/T1056/001/)
    
- [SANS Institute: Cobalt Strike Threat Hunting Guide](https://www.sans.org/white-papers/)
    

### Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]