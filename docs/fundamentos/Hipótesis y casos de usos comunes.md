## 1. Definición de Hipótesis en Threat Hunting

Una **hipótesis** es una suposición fundamentada sobre la presencia de una amenaza en la red. No es una adivinanza; es una declaración analítica que guía la cacería y define qué datos buscar. Según la metodología de SANS y Lenin Ramírez, una hipótesis bien estructurada debe ser **específica, medible y orientada a la acción**.

## 2. Fuentes para la Generación de Hipótesis

Para no "cazar a ciegas", utilizamos el **Diamond Model** (Modelo Diamante) para conectar los puntos entre los elementos de una intrusión:

- **Adversario (Adversary):** ¿Qué grupos de APT suelen atacar a mi sector?
    
- **Capacidad (Capability):** ¿Qué herramientas o malware utilizan? (Ej. Mimikatz, AnyDesk).
    
- **Infraestructura (Infrastructure):** ¿Cómo se comunican con sus víctimas? (C2, IPs, Dominios).
    
- **Víctima (Victim):** ¿Qué activos críticos de mi red son los más atractivos?
    

## 3. Casos de Uso Comunes (Escenarios de Caza)

Estos son los escenarios prioritarios que todo Hunter debe documentar y ejecutar:

|**Táctica (MITRE)**|**Escenario de Hipótesis**|**Atributos de Telemetría (Logs)**|
|---|---|---|
|**Persistencia**|"Un atacante ha creado un servicio o tarea programada para sobrevivir a un reinicio".|Sysmon Event ID 1 (Process Creation), Event ID 13 (Registry Modification).|
|**Escalado de Privilegios**|"Se están realizando ataques de _Password Spraying_ o _Brute Force_ contra el AD".|Windows Event Logs 4625 (Logon Failure), 4624 (Success).|
|**Acceso a Credenciales**|"Se está intentando volcar la memoria de `lsass.exe` para extraer hashes".|Sysmon Event ID 10 (Process Access), herramientas como Mimikatz.|
|**Movimiento Lateral**|"El atacante está usando RDP o SMB de forma anómala entre estaciones de trabajo".|Logs de red, autenticaciones entre hosts (no de server a host).|
|**Comando y Control**|"Existe tráfico de balizamiento (_beacons_) hacia una IP no categorizada".|Logs de Firewall, DNS (consultas frecuentes a un mismo dominio).|

## 4. Estructura de un Caso de Uso (Template)

Para que tus cacerías en el lab sean ordenadas, cada hipótesis debe seguir este formato:

1. **Título:** Descripción breve del ataque (ej. Abuso de LOLBins).
    
2. **Técnica MITRE:** Identificador oficial (ej. T1059.001 - PowerShell).
    
3. **Hipótesis:** _"Si un atacante ha ganado acceso, usará PowerShell para descargar un script ofuscado desde internet"_.
    
4. **Consulta de Validación (KQL/VQL):** La query específica para Elastic o Velociraptor.
    
5. **Resultado Esperado:** Visualización de procesos hijos sospechosos de `powershell.exe`.
    

## 5. El Modelo Diamante en la Operativa

El uso del Diamond Model permite al Hunter realizar el "Pivoting":

- Si descubrimos una **Capacidad** (ej. un script de PowerShell raro), pivotamos hacia la **Infraestructura** (¿a qué IP se conecta?) para identificar el alcance total del ataque.
    

---

### Referencias Externas

- [The Diamond Model for Intrusion Analysis](https://www.google.com/search?q=http://www.activeresponse.org/wp-content/uploads/2013/07/diamond_model.pdf)
    
- [MITRE ATT&CK: Enterprise Techniques](https://attack.mitre.org/techniques/enterprise/)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]
[[Modelo Diamante como guía de CTH]]
[[Dataset de ataque simulado (logs y malware samples controlados)]]