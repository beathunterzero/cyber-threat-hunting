## 1. Definición y Propósito

Una vez que un adversario compromete un host, necesita establecer un canal para enviarle instrucciones (**Comando y Control o C2**) y extraer la información robada hacia su infraestructura (**Exfiltración**). Dado que las redes modernas bloquean el tráfico entrante no solicitado, los atacantes diseñan su malware para que sea el endpoint comprometido quien inicie la conexión hacia afuera, evadiendo así los firewalls perimetrales.

## 2. Arquitectura de Comando y Control

Basado en el diagrama de infraestructura operativa, los atacantes modernos utilizan una arquitectura de múltiples capas:

- **Atacante (Team Server):** El servidor central desde donde los operadores manejan el malware.
    
- **Redireccionadores (Redirectors):** Servidores proxy intermedios que enmascaran la dirección IP real del servidor C2.
    
- **Balizas (Beacons):** El payload malicioso ejecutándose dentro de la red comprometida que "llama a casa" periódicamente.
    

## 3. Técnicas de Comunicación de C2

|**Técnica**|**Descripción**|
|---|---|
|**Beaconing (Balizamiento)**|El malware envía señales periódicas y constantes al servidor C2 para indicar que sigue comprometido y listo para recibir comandos. Se suele añadir _jitter_ (variación de tiempo) para evitar patrones predecibles.|
|**DGA (Domain Generation Algorithms)**|Generación automática y masiva de múltiples nombres de dominio aleatorios a los que el malware intenta conectarse, evadiendo listas negras estáticas.|
|**Fast Flux DNS**|Cambios rápidos y constantes en las direcciones IP asociadas con un único nombre de dominio para ocultar la ubicación real del C2.|
|**Canales Cifrados**|Uso de protocolos legítimos como HTTPS o TLS para encriptar las comunicaciones del C2, mezclándolas con el tráfico normal y cegando la inspección profunda (DPI).|
|**Esteganografía**|Ocultación de comandos o información dentro de archivos aparentemente inofensivos (como imágenes o documentos) en el tráfico de red.|

## 4. Técnicas de Exfiltración

|**Técnica**|**Descripción**|
|---|---|
|**Compresión y Cifrado de Datos**|Reducción del tamaño de los archivos robados y su posterior cifrado con contraseñas para evitar la lectura por parte de herramientas de Prevención de Pérdida de Datos (DLP).|
|**Protocolos Alternativos**|Uso de protocolos que generalmente no están tan monitoreados como HTTP/HTTPS, tales como consultas DNS, paquetes ICMP o túneles FTP.|
|**Servicios de Almacenamiento en la Nube**|Subida de los datos robados a servicios comerciales legítimos (Google Drive, Dropbox, Mega) para que el tráfico saliente parezca actividad habitual.|
|**Transferencia Programada**|Exfiltración de datos programada durante horas de menor actividad (madrugadas o fines de semana) para evitar picos de tráfico sospechosos.|
|**Chunking (Fragmentación)**|División de volúmenes masivos de datos en fragmentos muy pequeños que se envían lentamente para evadir límites de tamaño de archivo y alertas de volumen.|

## 5. Caza Operativa: Detectando Exfiltración/C2 por DNS (KQL)

Las extensiones de dominio inusuales (TLDs) o el volumen excesivo de consultas DNS hacia dominios sospechosos pueden indicar el uso de DGA o exfiltración vía DNS.

**Consulta de Detección (Hunting Query):**

Fragmento de código

```kql
DeviceNetworkEvents
| where ActionType == 'DnsConnection'
| where RemoteUrl has_any ('.xyz', '.top', '.club')
| summarize count() by RemoteUrl, DeviceId
| where count_ > 100
```

## 6. Ejemplos de Procedimientos (Exfiltración sobre C2)

El siguiente cuadro muestra ejemplos reales documentados de cómo diferentes actores de amenazas y familias de malware ejecutan la exfiltración de datos utilizando sus canales de C2 ya establecidos.

|**Nombre**|**ID**|**Descripción del Procedimiento Operativo**|
|---|---|---|
|**ADVSTORESHELL**|S0045|ADVSTORESHELL exfiltra datos a través del mismo canal utilizado para el C2.|
|**Agrius**|G1030|Agrius exfiltró datos preparados utilizando herramientas como Putty y WinSCP, comunicándose con servidores de comando y control.|
|**Amadey**|S1025|Amadey ha enviado datos de víctimas a sus servidores C2.|
|**AppleJeus**|S0584|AppleJeus ha exfiltrado información recopilada del host a un servidor C2.|
|**AppleSeed**|S0622|AppleSeed puede exfiltrar archivos a través del canal C2.|
|**APT3**|G0022|APT3 tiene una herramienta que exfiltra datos a través del canal C2.|
|**APT32**|G0050|El _backdoor_ de APT32 ha exfiltrado datos utilizando el canal ya abierto con su servidor C&C.|
|**APT39**|G0087|APT39 ha exfiltrado datos robados de víctimas a través de comunicaciones C2.|
|**ArcaneDoor**|C0046|ArcaneDoor incluyó el uso de canales de comando y control existentes para la exfiltración de datos.|

## 7. Análisis de Caso Práctico: TTPs de ADVSTORESHELL

Para comprender cómo un malware orquesta todo el ciclo (desde la persistencia hasta la exfiltración), el siguiente cuadro desglosa las técnicas específicas utilizadas por **ADVSTORESHELL**, mapeadas al framework MITRE ATT&CK.

|**Dominio**|**ID de Técnica**|**Nombre de la Técnica**|**Uso Práctico / Implementación del Malware**|
|---|---|---|---|
|Enterprise|**T1071.001**|Protocolo de Capa de Aplicación: Protocolos Web|ADVSTORESHELL se conecta al puerto 80 de un servidor C2 usando la API Wininet. Los datos se intercambian a través de HTTP POSTs.|
|Enterprise|**T1560.003**|Archivar Datos Recopilados: Método Personalizado|ADVSTORESHELL comprime los datos de salida generados por la ejecución de comandos con una implementación personalizada del algoritmo Lempel-Ziv-Welch (LZW).|
|Enterprise|**T1547.001**|Ejecución de Inicio Automático: Claves de Registro (Run Keys)|ADVSTORESHELL logra persistencia agregándose a la clave de registro `HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`.|
|Enterprise|**T1059.003**|Intérprete de Comandos y Scripts: Windows Command Shell|ADVSTORESHELL puede crear un shell remoto y ejecutar un comando dado.|
|Enterprise|**T1132.001**|Codificación de Datos: Codificación Estándar|El tráfico C2 de ADVSTORESHELL se cifra y luego se codifica con Base64.|
|Enterprise|**T1074.001**|Datos Preparados (Staged): Datos Locales|ADVSTORESHELL almacena la salida de la ejecución de comandos en un archivo `.dat` en el directorio `%TEMP%`.|
|Enterprise|**T1573.001**|Canal Cifrado: Criptografía Simétrica|ADVSTORESHELL cifra con el algoritmo 3DES y una clave codificada internamente (_hardcoded_) antes de la exfiltración.|
|Enterprise|**T1573.002**|Canal Cifrado: Criptografía Asimétrica|Una variante de ADVSTORESHELL cifra parte de su comunicación C2 utilizando RSA.|

---

### Referencias Externas

- [MITRE ATT&CK: Exfiltration Over C2 Channel (T1041)](https://attack.mitre.org/techniques/T1041/)
    
- [MITRE ATT&CK: Software ADVSTORESHELL (S0045)](https://attack.mitre.org/software/S0045/)
    
- [Microsoft Defender: DeviceNetworkEvents table](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-devicenetworkevents-table)
    

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]