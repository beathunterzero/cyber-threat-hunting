## 1. ¿Qué es una hipótesis en Threat Hunting?

Una **hipótesis** es una suposición basada en datos que busca validar la presencia de una amenaza.

- No es intuición → es análisis
    
- Define **qué buscar** y **dónde buscar**
    
- Debe ser:
    
    - Específica
        
    - Medible
        
    - Accionable
        

---

## 2. ¿Cómo generar hipótesis?

Se construyen a partir de contexto y modelos como **Diamond Model**:

- **Adversario:**
    
    - Qué actores atacan tu sector
        
- **Capacidad:**
    
    - Herramientas y técnicas utilizadas
        
- **Infraestructura:**
    
    - Cómo se comunican (C2, dominios, IPs)
        
- **Víctima:**
    
    - Qué activos son objetivo
        

---

## 3. Casos de uso comunes

|Táctica|Hipótesis|Telemetría|
|---|---|---|
|Persistencia|Creación de servicios o tareas|Sysmon 1, 13|
|Privilegios|Ataques de autenticación|Event 4625, 4624|
|Credenciales|Acceso a `lsass.exe`|Sysmon 10|
|Movimiento lateral|Uso anómalo de RDP/SMB|Logs de red, autenticación|
|C2|Beaconing hacia IP externa|DNS, firewall|

---

## 4. Template de hipótesis

Estructura estándar para documentar:

1. **Título**
    
    - Ej: abuso de PowerShell
        
2. **Técnica (MITRE)**
    
    - Ej: T1059.001
        
3. **Hipótesis**
    
    - Ej: uso de PowerShell para descarga remota
        
4. **Consulta**
    
    - Query en SIEM / EDR
        
5. **Resultado esperado**
    
    - Actividad sospechosa validada
        

---

## 5. Uso operativo del Diamond Model

Permite pivotear durante la investigación:

- Detectas una **capacidad** → buscas infraestructura
    
- Detectas infraestructura → identificas víctimas
    
- Detectas víctimas → amplías alcance
    

Objetivo:

- Pasar de un evento aislado a una **visión completa del ataque**
    

---

## Referencias Externas

- [https://apps.dtic.mil/sti/pdfs/ADA586960.pdf](https://apps.dtic.mil/sti/pdfs/ADA586960.pdf)
    
- [https://attack.mitre.org/techniques/enterprise/](https://attack.mitre.org/techniques/enterprise/)
    
- [https://www.sans.org/white-papers/35502/](https://www.sans.org/white-papers/35502/)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[09 - Modelo Diamante como guía de CTH]]