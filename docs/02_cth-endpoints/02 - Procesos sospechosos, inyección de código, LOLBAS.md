## 1. ¿Qué se busca?

Detectar **ejecución maliciosa oculta** en endpoints.

Enfoque:

- No buscar archivos → analizar **comportamiento**
    
- Revisar procesos legítimos usados de forma anómala
    
- Detectar manipulación de memoria
    

---

## 2. Procesos sospechosos

Analizar eventos de creación de procesos (Sysmon 1 / Event 4688):

- **`powershell.exe`**
    
    - Uso de `-enc`, `-ExecutionPolicy Bypass`
        
- **`rundll32.exe`**
    
    - DLLs en `Temp` o `AppData`
        
- **`wscript.exe` / `cscript.exe`**
    
    - Scripts descargados
        
- **`svchost.exe`**
    
    - Rutas no estándar
        
    - Procesos hijos anómalos
        
- **`explorer.exe`**
    
    - Lanza `cmd.exe`
        
    - Conexiones de red inusuales
        

---

## 3. Inyección de código

Ejecuta código malicioso dentro de procesos legítimos.

Tipos comunes:

|Técnica|Descripción|
|---|---|
|Process Hollowing|Reemplaza memoria de proceso legítimo|
|DLL Injection|Carga DLL maliciosa|
|Reflective DLL|Inyección en memoria (fileless)|
|Thread Hijacking|Uso de hilos existentes|

Indicadores:

- Acceso a memoria entre procesos
    
- APIs sospechosas:
    
    - `WriteProcessMemory`
        
    - `CreateRemoteThread`
        
    - `NtUnmapViewOfSection`
        

Eventos útiles:

- Sysmon 8
    
- Sysmon 10
    

---

## 4. LOLBAS

Uso malicioso de herramientas legítimas.

|Binario|Uso malicioso|
|---|---|
|`powershell.exe`|Ejecución remota|
|`mshta.exe`|Scripts desde web|
|`rundll32.exe`|DLL maliciosa|
|`regsvr32.exe`|Ejecución remota|
|`certutil.exe`|Descarga de archivos|
|`wmic.exe`|Ejecución remota|

Clave:

- No es el binario → es el **uso**
    

---

## 5. PowerShell: patrones críticos

Buscar:

1. **Bypass de políticas**
    
    - `-ExecutionPolicy Bypass`
        
2. **Comandos codificados**
    
    - `-enc`, `-EncodedCommand`
        
3. **Ejecución oculta**
    
    - `-WindowStyle Hidden`
        
4. **Descarga remota**
    
    - `DownloadString`, `Invoke-WebRequest`
        
5. **Ejecución en memoria**
    
    - `IEX` (Invoke-Expression)
        
6. **Bypass AMSI**
    
    - Código para evadir detección
        

---

## 6. Enfoque de hunting

- Analizar relaciones padre/hijo
    
- Revisar argumentos de ejecución
    
- Correlacionar con red
    
- Priorizar comportamiento sobre firmas
    

---

## Referencias Externas

- [https://attack.mitre.org/techniques/T1218/](https://attack.mitre.org/techniques/T1218/)
    
- [https://attack.mitre.org/techniques/T1059/001/](https://attack.mitre.org/techniques/T1059/001/)
    
- [https://lolbas-project.github.io/](https://lolbas-project.github.io/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]