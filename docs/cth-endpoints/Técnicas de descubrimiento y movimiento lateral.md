## 1. Definición y Enfoque Operativo

Esta fase engloba las **acciones utilizadas por los atacantes dentro de una red comprometida para reconocer el entorno, identificar objetivos y expandir su acceso hacia otros sistemas o cuentas más privilegiadas.** El reto para el Threat Hunter es que en estas fases los atacantes se mezclan con la actividad normal de los administradores de red, por lo que la detección depende de identificar desviaciones en el comportamiento habitual.

## 2. Pirámide de Descubrimiento y Movimiento Lateral

De acuerdo con el modelo operativo del curso, las tácticas se estructuran en los siguientes niveles (de reconocimiento inicial a ejecución profunda), junto con sus huellas de detección:

|**Nivel de Táctica**|**Técnica / Acción**|**Huellas para Detección (Indicadores)**|
|---|---|---|
|**1**|**Escaneo y descubrimiento de red**|Picos inusuales de tráfico de descubrimiento, múltiples conexiones a puertos comunes (135/137/139/445) desde un mismo host.|
|**2**|**Enumeración de cuentas y recursos (Account/Service Discovery)**|Consultas repetitivas a APIs de directorio, enumeración de SMB/LDAP fuera del comportamiento normal, búsquedas masivas de cuentas.|
|**3**|**Robo de credenciales y uso de credenciales robadas (credential harvesting / reuse)**|Accesos remotos desde cuentas elevadas fuera de horario, uso de herramientas de dumping, autenticaciones con hashes en lugar de contraseñas.|
|**4**|**Abuso de servicios remotos: RDP, WinRM / PowerShell Remoting**|Nuevas sesiones RDP entre hosts donde no suelen existir, ejecución remota de PowerShell desde orígenes inesperados, muchos intentos de autenticación remota.|
|**5**|**Ejecución remota vía SMB, PsExec o creación de servicios remotos**|Creación/escalado de servicios remotos, procesos iniciados por cuentas de administración desde hosts no habituales, llamadas a PsExec identificables en logs.|
|**6**|**WMI / WMIC y Scheduled Tasks para ejecución remota y persistencia**|Creación de `CommandLineEventConsumer/filters`, tareas programadas nuevas o modificadas por usuarios no autorizados, actividad WMI fuera de patrones normales.|

## 3. Comandos Comunes (LOLBins de Reconocimiento)

Para ejecutar el Nivel 2 de la pirámide, los atacantes suelen utilizar herramientas nativas (_Living Off the Land_). Estos comandos deben vigilarse si se ejecutan en secuencias rápidas:

- `whoami /all`
    
- `net user /domain`
    
- `net group "Domain Admins" /domain`
    
- `nltest /dclist:`
    
- `ipconfig /all` y `arp -a`
    

## 4. Estrategia de Caza para el Threat Hunter

- **Contexto de la Línea de Comandos:** Comandos como `net user` son de uso diario por parte de TI, pero si son ejecutados como procesos hijos de aplicaciones inusuales (como `winword.exe` o procesos web como `w3wp.exe`), representan un indicador crítico.
    
- **Análisis de Grafos de Red:** Es fundamental establecer una línea base de las conexiones RDP y SMB. Las comunicaciones laterales entre estaciones de trabajo (Workstation a Workstation) suelen ser la firma clara de una infección propagándose.
    

---

### Referencias Externas

- [MITRE ATT&CK: Discovery (TA0007)](https://attack.mitre.org/tactics/TA0007/)
    
- [MITRE ATT&CK: Lateral Movement (TA0008)](https://attack.mitre.org/tactics/TA0008/)
    

### Documentación Relacionada

[[Procesos sospechosos, inyección de código, LOLBAS]]
[[Técnicas de persistencia y ejecución en endpoints]]