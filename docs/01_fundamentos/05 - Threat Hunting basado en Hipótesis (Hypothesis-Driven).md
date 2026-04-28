## 1. ¿Qué es el Hypothesis-Driven Hunting?

El **Threat Hunting basado en hipótesis** es el enfoque más **proactivo**.

- No depende de IoCs externos
    
- Parte del conocimiento de **TTPs**
    
- Asume que el atacante ya está presente
    
- Busca **comportamientos**, no artefactos
    

Opera en la **cúspide de la Pirámide del Dolor**.

---

## 2. ¿De dónde salen las hipótesis?

Una hipótesis válida se basa en:

- **MITRE ATT&CK:**
    
    - Técnicas de persistencia, ejecución, movimiento lateral
        
- **CTI (Threat Intelligence):**
    
    - Adaptación de TTPs de actores reales al entorno propio
        
- **Contexto interno:**
    
    - Conocimiento de lo normal vs anómalo
        

Ejemplo:

> Si un atacante usa tareas programadas para persistencia, ¿cómo se vería en mis sistemas?

---

## 3. Tipos de hunting por hipótesis

- **Persistencia:**
    
    - Run keys, servicios, WMI subscriptions
        
- **Movimiento lateral:**
    
    - Uso anómalo de RDP, SMB, autenticaciones
        
- **Exfiltración:**
    
    - Tráfico hacia cloud o protocolos no comunes
        
- **LOLBins:**
    
    - Uso sospechoso de `powershell.exe`, `certutil.exe`, `mshta.exe`
        

---

## 4. Flujo de trabajo

1. **Formulación**
    
    - Definir una hipótesis clara
        
2. **Datos requeridos**
    
    - Identificar logs necesarios (Sysmon, red, OS)
        
3. **Ejecución**
    
    - Consultas en SIEM / EDR
        
4. **Validación**
    
    - Confirmar o descartar la hipótesis
        

---

## 5. IoC vs Hypothesis Hunting

|IoC-Driven|Hypothesis-Driven|
|---|---|
|Reactivo|Proactivo|
|Basado en artefactos|Basado en comportamiento|
|Fácil de automatizar|Requiere análisis|
|Baja durabilidad|Alta durabilidad|
|Bajo valor estratégico|Alto valor estratégico|

---

## 6. Telemetría necesaria

Para que este enfoque funcione, se requiere visibilidad completa:

- **Procesos:**
    
    - Parent/Child
        
    - Command line
        
    - DLLs cargadas
        
- **Red:**
    
    - Conexiones persistentes
        
    - TLS sospechoso
        
- **Sistema:**
    
    - Registro, usuarios, logs
        
- **Archivos:**
    
    - Ejecución en `AppData`, `Temp`
        

---

## Referencias Externas

- [https://attack.mitre.org/](https://attack.mitre.org/)
    
- [https://www.threathunting.net/hunts/](https://www.threathunting.net/hunts/)
    
- [https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[04 - Threat Hunting basado en IoCs (IoC-Driven)]]  
[[06 - Threat Hunting basado en Analítica (Analytics-Driven)]]