## 1. ¿Qué se busca?

Detectar amenazas reales mediante **comportamiento (TTPs)**.

Enfoque:

- No depender de IoCs
    
- Traducir actividad en patrones detectables
    
- Usar telemetría de endpoint y red
    

---

## 2. Estrategias por amenaza

### 2.1 Ransomware

**Objetivo:**

- Cifrado masivo de archivos
    

**Qué buscar:**

- Alto volumen de escritura en poco tiempo
    
- Un solo proceso modificando muchos archivos
    

**Indicadores:**

- Eliminación de shadow copies (`vssadmin`, `wmic`)
    
- Cambios masivos de extensiones
    
- Archivos de rescate repetidos
    

---

### 2.2 Cobalt Strike

**Objetivo:**

- Control remoto (C2)
    
- Post-explotación
    

**Qué buscar:**

**Red:**

- Beaconing (intervalos regulares)
    
- Conexiones a dominios desconocidos
    

**Endpoint:**

- Procesos legítimos con actividad anómala
    
- Inyección de procesos
    

Ejemplos:

- `rundll32.exe` con tráfico de red
    
- `svchost.exe` fuera de patrón
    

---

### 2.3 Keyloggers

**Objetivo:**

- Captura de credenciales
    

**Qué buscar:**

- Interacción con teclado
    
- Archivos ocultos de registro
    

**APIs críticas:**

- `SetWindowsHookEx`
    
- `GetAsyncKeyState`
    

Indicadores:

- Archivos `.log` o `.dat` en `AppData`
    
- Procesos accediendo input sin contexto
    

---

## 3. Matriz rápida

|Amenaza|Foco|Indicadores|
|---|---|---|
|Ransomware|File system|Escrituras masivas|
|Cobalt Strike|Red + memoria|Beaconing + inyección|
|Keylogger|API + archivos|Hooks + logs ocultos|

---

## 4. Enfoque de hunting

- Priorizar comportamiento
    
- Correlacionar endpoint + red
    
- Detectar patrones repetitivos
    
- Validar contra baseline
    

---

## 5. Objetivo final

- Detectar antes del impacto
    
- Reducir dwell time
    
- Convertir hallazgos en detecciones
    

---

## Referencias Externas

- [https://attack.mitre.org/techniques/T1486/](https://attack.mitre.org/techniques/T1486/)
    
- [https://attack.mitre.org/techniques/T1056/001/](https://attack.mitre.org/techniques/T1056/001/)
    
- [https://www.sans.org/white-papers/](https://www.sans.org/white-papers/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]