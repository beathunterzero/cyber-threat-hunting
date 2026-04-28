## 1. Introducción

Este glosario está diseñado con enfoque **operativo para Threat Hunting (CTH)**.  
Los términos están organizados por **categorías funcionales** y ordenados **alfabéticamente dentro de cada categoría**, priorizando claridad, uso práctico y detección.

---

# 2. Conceptos Fundamentales

- **Activo:** Recurso crítico (host, usuario, servidor, datos) que debe protegerse.
- **Amenaza:** Cualquier entidad o acción con capacidad de causar daño.
- **Análisis:** Proceso de interpretar datos para generar inteligencia accionable.
- **Anomalía:** Desviación del comportamiento normal (baseline).
- **Assume Breach:** Enfoque que asume que el atacante ya está dentro.
- **Baseline:** Comportamiento normal esperado de un sistema.
- **Brecha:** Compromiso de seguridad confirmado.
- **Campaña:** Conjunto de actividades coordinadas por un adversario.
- **Comportamiento:** Acciones observables de procesos, usuarios o red.
- **Dwell Time:** Tiempo que un atacante permanece sin ser detectado.
- **Entorno:** Contexto donde ocurre la actividad (cloud, endpoint, red).
- **Evento:** Registro individual generado por un sistema.
- **Finding:** Hallazgo relevante derivado de hunting.
- **Falso positivo (FPR):** Evento detectado como malicioso pero legítimo.
- **Gap:** Falta de visibilidad o cobertura de detección.
- **Hipótesis:** Suposición estructurada que guía la caza.
- **Infraestructura:** Recursos usados por atacante (IPs, dominios, C2).
- **Indicador (IoC):** Evidencia puntual de compromiso (IP, hash, dominio).
- **Indicador de Ataque (IOA):** Comportamiento que sugiere actividad maliciosa.
- **Patrones:** Secuencias repetitivas detectables en datos.
- **Pivoting:** Cambio de enfoque investigativo basado en hallazgos.
- **Telemetría:** Datos recolectados de sistemas para análisis.
- **TTPs:** Tácticas, Técnicas y Procedimientos del atacante.
- **Vector:** Método de entrada del ataque.

---

# 3. Frameworks y Modelos

- **MITRE ATT&CK:** Framework de TTPs estructurado por tácticas.
- **ATT&CK Navigator:** Herramienta para mapear cobertura de técnicas.
- **Pirámide del Dolor:** Modelo que clasifica valor de indicadores.
- **Cyber Threat Hunting (CTH):** Búsqueda proactiva de amenazas.
- **CTI (Cyber Threat Intelligence):** Inteligencia sobre amenazas.
- **DFIR:** Respuesta e investigación forense de incidentes.
- **CSIRT:** Equipo de respuesta a incidentes.
- **CJA (Crown Jewels Analysis):** Identificación de activos críticos.

---

# 4. Herramientas y Plataformas

- **EDR:** Detección y respuesta en endpoints.
- **SIEM:** Centralización y correlación de logs.
- **SOAR:** Automatización de respuesta.
- **Elastic Security:** SIEM basado en Elastic Stack.
- **Kibana:** Interfaz de visualización de Elastic.
- **Filebeat:** Forwarder de logs hacia Elastic.
- **Velociraptor:** EDR orientado a forense y hunting.
- **Splunk:** Plataforma SIEM comercial.
- **Microsoft Sentinel:** SIEM cloud de Microsoft.
- **CrowdStrike:** Plataforma EDR comercial.
- **BloodHound:** Análisis de relaciones en Active Directory.
- **Sandbox:** Entorno aislado para ejecutar malware.

---

# 5. Telemetría y Logs

- **Sysmon:** Telemetría avanzada de Windows.
- **Windows Event Logs:** Logs nativos del sistema.
- **Security Log:** Registro de eventos de seguridad.
- **OS Log:** Logs del sistema operativo.
- **Network Logs:** Registros de tráfico de red.
- **DNS:** Resolución de nombres.
- **Netflow:** Flujo de tráfico de red.
- **Proxy:** Intermediario de tráfico web.
- **TLS/SSL:** Protocolos de cifrado.
- **SSH:** Protocolo de acceso remoto seguro.
- **GeoIP:** Geolocalización de IPs.
- **ASN:** Sistema autónomo de red.
- **ECS:** Elastic Common Schema.
- **ASIM:** Normalización de logs en Microsoft.

---

# 6. Red y Comunicación

- **C2 (Command and Control):** Canal de control del atacante.
- **Beaconing:** Comunicación periódica hacia C2.
- **DNS Tunneling:** Uso de DNS para exfiltración/C2.
- **DGA:** Generación automática de dominios.
- **Fast Flux:** Rotación rápida de IPs en DNS.
- **ICMP:** Protocolo usado en tunneling.
- **FTP:** Protocolo de transferencia.
- **CDN:** Red de distribución de contenido.
- **Cloud:** Infraestructura en la nube.
- **Redirectores:** Proxies que ocultan C2.
- **Team Server:** Servidor central del atacante.
- **Nodo Tor:** Nodo de red Tor.
- **User-Agent:** Identificador en tráfico HTTP.
- **Headers:** Cabeceras HTTP.
- **TLDs:** Dominios de nivel superior.

---

# 7. Técnicas de Ataque

- **Persistencia:** Mantener acceso tras reinicio.
- **Movimiento lateral:** Expansión dentro de la red.
- **Evasión de firmas:** Evitar detección tradicional.
- **Exfiltración:** Extracción de datos.
- **Phishing:** Ingeniería social.
- **Payload:** Código malicioso ejecutado.
- **Fileless:** Ataques sin archivos en disco.
- **LOLBins / LOLBAS:** Uso de binarios legítimos.
- **DLL Injection:** Inyección de librerías en memoria.
- **Beacon:** Payload que se comunica con C2.
- **Keylogger:** Captura de teclado.
- **Ransomware:** Cifrado de archivos.
- **RAT:** Control remoto del sistema.
- **Dropper:** Descarga de malware.
- **Esteganografía:** Ocultación en archivos.
- **Pass-the-Hash (NTLM):** Uso de hashes para autenticación.

---

# 8. Sistema y Endpoint

- **Endpoint:** Dispositivo final (host).
- **Host:** Sistema dentro de la red.
- **AppData / Temp:** Rutas comunes de malware.
- **Run Keys:** Persistencia en registro.
- **Scheduled Tasks:** Persistencia mediante tareas.
- **WMI:** Administración y persistencia fileless.
- **svchost:** Proceso crítico de Windows.
- **winword:** Vector común de ataque.
- **regsvr32:** Ejecución de DLLs.
- **wscript / cscript:** Ejecución de scripts.
- **PowerShell:** Shell potente y abusado.
- **Command Line:** Línea de comandos ejecutada.
- **Parent/Child:** Relación entre procesos.

---

# 9. Comandos y Artefactos

- **whoami /all:** Enumeración de usuario.
- **net user /domain:** Enumeración de cuentas.
- **nltest:** Enumeración de dominio.
- **arp -a:** Tabla ARP.
- **ipconfig:** Configuración de red.
- **psexec:** Ejecución remota.
- **vssadmin:** Gestión de shadow copies.
- **wmic:** Interacción WMI.
- **mimikatz:** Extracción de credenciales.
- **lsass.exe:** Proceso de autenticación.

---

# 10. Criptografía y Codificación

- **Hash:** Firma única de archivo.
- **Base64 / Base32:** Codificación de datos.
- **3DES / RSA:** Algoritmos criptográficos.
- **Certificado:** Identidad digital.
- **TLS:** Cifrado de tráfico.

---

# 11. Privilegios y Seguridad

- **Usuarios privilegiados:** Cuentas con altos permisos.
- **SeDebugPrivilege:** Acceso a procesos.
- **SeImpersonatePrivilege:** Suplantación de identidad.
- **ACLs:** Control de acceso.
- **GenericAll / WriteDacl:** Permisos abusables.

---

# 12. Consultas y Lenguajes

- **KQL:** Lenguaje de consultas en Microsoft/Elastic.
- **EQL:** Lenguaje de correlación en Elastic.
- **VQL:** Lenguaje de Velociraptor.
- **Query:** Consulta técnica.
- **Dataset:** Conjunto de datos.
- **Scope:** Alcance de búsqueda.

---

# 13. Métricas y Operación

- **MTTD:** Tiempo medio de detección.
- **MTTR / MTTC:** Tiempo de respuesta/contención.
- **KPI:** Indicador de desempeño.
- **TTRU:** Time to Rule.
- **Detection Yield:** Efectividad del hunting.
- **Time to Production:** Tiempo para desplegar detección.

---

# 14. Inteligencia y OSINT

- **OSINT:** Inteligencia de fuentes abiertas.
- **Reputación:** Evaluación de IP/dominio.
- **Actor:** Grupo atacante.
- **Insider:** Amenaza interna.
- **Lazarus:** Grupo APT.
- **APT41:** Actor avanzado.

---

# 15. DevSecOps y Automatización

- **CI/CD:** Integración y despliegue continuo.
- **Pipeline:** Flujo automatizado.
- **Trigger:** Evento que dispara acción.
- **Forwarders:** Agentes de envío de logs.
- **Vendors:** Proveedores de seguridad.

---

### Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[06 - Queries y hunting en EDR]]  
[[07 - Cómo formular búsquedas efectivas]]  
[[10 - Convertir inteligencia en hipótesis de hunting]]  
[[01 - Madurez y métricas de hunting]]