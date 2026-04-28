## 1. ¿Qué es la preparación del entorno?

Es la fase previa al hunting donde se garantiza:

- **Visibilidad suficiente**
    
- **Datos confiables**
    
- **Herramientas operativas**
    

Sin telemetría → no hay hunting.

---

## 2. Componentes del entorno

Tres capas básicas:

- **Fuentes de datos:**
    
    - Endpoints, red, cloud
        
- **Agentes de recolección:**
    
    - EDR, forwarders
        
- **Plataforma de análisis (SIEM):**
    
    - Centralización y consultas
        

---

## 3. Telemetría mínima requerida

|Fuente|Datos|Uso|
|---|---|---|
|Windows Logs|Autenticación, servicios|Accesos, privilegios|
|Sysmon|Procesos, red, archivos|Actividad técnica|
|EDR|Artefactos, memoria|Persistencia, comportamiento|
|Network|DNS, HTTP, NetFlow|C2, exfiltración|

---

## 4. Cobertura del Diamond Model

La telemetría debe permitir cubrir:

- **Víctima:** host, usuario
    
- **Infraestructura:** IPs, dominios
    
- **Capacidad:** procesos, malware
    
- **Adversario:** correlación con CTI
    

---

## 5. Configuración básica

1. **Auditoría**
    
    - Activar logs avanzados
        
    - Instalar Sysmon
        
2. **Agentes**
    
    - EDR / recolección
        
3. **Ingesta**
    
    - Datos en SIEM
        
4. **Validación**
    
    - Ejecutar prueba y verificar logs
        

---

## 6. Calidad del dato

- **Consistencia:** normalización (ECS u otro)
    
- **Latencia baja:** datos en tiempo útil
    
- **Contexto:** metadata del activo
    

---

## 7. Herramientas y enfoque

|Fuente|Tipo|Visibilidad|Esfuerzo|
|---|---|---|---|
|SIEM|Correlación|Media/Alta|Bajo|
|EDR|Comportamiento|Alta|Alto|
|Network|Tráfico|Alta|Medio|
|CTI|Contexto|N/A|Bajo|

---

## 8. Pilares operativos

Antes de hacer hunting:

- **Objetivos claros**
    
- **Centralización de datos**
    
- **Herramientas listas**
    
- **Accesos adecuados**
    
- **Datos validados**
    
- **Entorno controlado (lab/sandbox)**
    

---

## Referencias Externas

- [https://www.elastic.co/guide/en/ecs/current/index.html](https://www.elastic.co/guide/en/ecs/current/index.html)
    
- [https://docs.velociraptor.app/](https://docs.velociraptor.app/)
    
- [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    
- [https://www.sans.org/white-papers/36302/](https://www.sans.org/white-papers/36302/)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[01 - Creación de elastic-security-lab]]