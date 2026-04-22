## 1. Definición y Enfoque Operativo

Este documento se centra en las técnicas avanzadas que utilizan los adversarios para ocultar su ejecución y evadir detecciones basadas en firmas. El enfoque del Hunter debe cambiar de buscar "archivos maliciosos" a analizar el **comportamiento de procesos legítimos**, monitorear la manipulación de memoria y vigilar el abuso de herramientas nativas del sistema operativo.

## 2. Ejemplos Comunes de Procesos Sospechosos

La telemetría de endpoint (Sysmon ID 1 o Evento 4688) debe ser auditada buscando anomalías en los siguientes procesos principales:

- **`powershell.exe`:** Ejecutando comandos en formato codificado mediante el argumento `-EncodedCommand` (u ofuscaciones similares).
    
- **`rundll32.exe`:** Cargando bibliotecas DLL desde ubicaciones no confiables o temporales (ej. `\Temp`, `\AppData`).
    
- **`wscript.exe`** o **`cscript.exe`:** Ejecutando scripts directamente descargados de Internet sin interacción del usuario.
    
- **`svchost.exe`:** Lanzando procesos hijos que no están relacionados con servicios legítimos del sistema o ejecutándose desde rutas que no son `System32`.
    
- **`explorer.exe`:** Iniciando conexiones de red inusuales o abriendo shells ocultos (ej. `cmd.exe` como hijo directo).
    

## 3. Técnicas de Inyección de Código

La inyección de código permite a un atacante ejecutar código malicioso bajo el contexto de un proceso legítimo y firmado.

|**Tipo de Inyección**|**Descripción Técnica**|
|---|---|
|**Process Hollowing**|Reemplazar el contenido de la memoria de un proceso legítimo suspendido (ej. `svchost.exe` o `notepad.exe`) con código malicioso antes de reanudar su ejecución.|
|**DLL Injection**|Forzar a un proceso legítimo en ejecución a cargar una biblioteca dinámica maliciosa desde el disco.|
|**Reflective DLL Injection**|Inyección directa de una DLL en la memoria de un proceso sin necesidad de escribir archivos en el disco (Fileless).|
|**Thread Execution Hijacking**|Secuestro de hilos de ejecución existentes dentro de un proceso legítimo para desviarlos hacia código malicioso.|

> [!TIP]
> 
> **Ejemplo de detección forense:** Para identificar manipulación de memoria inter-procesos, el Hunter debe buscar el uso inusual de APIs de Windows específicas como `WriteProcessMemory`, `CreateRemoteThread` o `NtUnmapViewOfSection` _(Sysmon Event ID 8 y 10)._

## 4. LOLBAS (Living Off the Land Binaries and Scripts)

Los atacantes utilizan herramientas legítimas del sistema operativo porque ya están firmadas por el fabricante (Microsoft), lo que reduce drásticamente la probabilidad de detección por antivirus tradicionales.

|**Binario / Script**|**Uso Legítimo Originial**|**Uso Malicioso Posible**|
|---|---|---|
|**`powershell.exe`**|Administración avanzada de sistemas.|Descarga y ejecución de payloads remotos en memoria.|
|**`mshta.exe`**|Ejecución de archivos HTML Applications (HTA).|Ejecución de scripts remotos maliciosos (ej. VBScript, JScript).|
|**`rundll32.exe`**|Cargar bibliotecas DLL legítimas.|Cargar DLL maliciosas en memoria.|
|**`regsvr32.exe`**|Registrar componentes COM (DLL).|Ejecutar scripts u objetos COM directamente desde Internet (`/s /u /i:http://...`).|
|**`certutil.exe`**|Gestión de certificados digitales.|Descargar archivos maliciosos (ej. `certutil.exe -urlcache -split -f http://...`).|
|**`wmic.exe`**|Administración remota y local (WMI).|Ejecutar comandos en la red o crear persistencia fileless.|

## 5. Los 6 Usos Maliciosos de PowerShell (Análisis Específico)

Debido a su integración profunda con el sistema, PowerShell requiere atención especial. Al cazar anomalías en `powershell.exe`, se deben buscar patrones que coincidan con estos 6 usos tácticos comunes:

1. **Bypass de Políticas de Ejecución:** Uso de argumentos como `-ExecutionPolicy Bypass` o `-ep bypass` para ignorar las restricciones de seguridad locales y forzar la ejecución de un script.
    
2. **Ejecución de Comandos Codificados:** Uso de `-EncodedCommand`, `-e`, o `-enc` para pasar instrucciones en Base64, ofuscando el código para evadir herramientas de seguridad basadas en cadenas de texto.
    
3. **Ocultamiento de Consola:** Uso de `-WindowStyle Hidden` o `-w hidden` para que la ejecución ocurra en segundo plano sin mostrar ninguna ventana emergente al usuario.
    
4. **Descarga de Payloads (Download Cradles):** Uso de comandos integrados como `Net.WebClient.DownloadString` o `Invoke-WebRequest` para descargar malware directamente desde el C2 del atacante.
    
5. **Ejecución Fileless (en Memoria):** Uso de `Invoke-Expression` (o su alias `IEX`) para tomar el código descargado en el punto anterior y ejecutarlo directamente en la memoria RAM, sin dejar artefactos en el disco.
    
6. **Evasión de AMSI (Bypass):** Ejecución de fragmentos de código diseñados para cegar o desactivar el _Antimalware Scan Interface_ (AMSI) antes de ejecutar el payload principal.
    

---

### Referencias Externas

- [MITRE ATT&CK: Living off the Land (T1218)](https://attack.mitre.org/techniques/T1218/)
    
- [MITRE ATT&CK: Command and Scripting Interpreter: PowerShell (T1059.001)](https://attack.mitre.org/techniques/T1059/001/)
    
- [The LOLBAS Project: Living Off The Land Binaries and Scripts](https://www.google.com/search?q=https://lolbas-project.github.com/)
    

### Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]