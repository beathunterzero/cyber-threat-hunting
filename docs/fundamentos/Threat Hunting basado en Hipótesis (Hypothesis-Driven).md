## 1. Definición y Concepto

El **Threat Hunting basado en Hipótesis** es el enfoque más proactivo y avanzado de la disciplina. A diferencia del modelo basado en IoCs, aquí el cazador no espera a recibir un indicador externo; en su lugar, utiliza el conocimiento profundo de las **TTPs** (Tácticas, Técnicas y Procedimientos) de los atacantes para suponer que una actividad maliciosa está ocurriendo en el entorno.

Este enfoque se sitúa en la **cúspide de la Pirámide del Dolor**, ya que busca identificar comportamientos que son difíciles de modificar para el adversario.

## 2. Origen de las Hipótesis

Según la metodología, una hipótesis sólida no surge del azar, sino de tres fuentes principales de conocimiento:

- **Tácticas y Técnicas (MITRE ATT&CK):** Análisis de cómo los atacantes logran persistencia, escalado de privilegios o exfiltración.
    
- **Inteligencia de Amenazas (CTI):** Adaptar el comportamiento de un grupo de APT conocido a la infraestructura propia (ej. _"Si el grupo Lazarus usa tareas programadas para persistencia, ¿cómo se vería eso en mis servidores Windows?"_).
    
- **Experiencia y Contexto:** Conocimiento del analista sobre qué es "normal" y qué es "anómalo" dentro de su red específica.
    

## 3. Tipos de Hunting por Hipótesis

Las cacerías se clasifican según el tipo de comportamiento que intentan descubrir:

- **Hunting de Persistencia:** Búsqueda de mecanismos que permitan al atacante mantener el acceso (registros `Run`, servicios nuevos, WMI Event Subscriptions).
    
- **Hunting de Movimiento Lateral:** Detección de uso inusual de RDP, SMB o autenticaciones sospechosas en controladores de dominio.
    
- **Hunting de Exfiltración:** Identificación de flujos de datos anómalos hacia nubes públicas o protocolos no estándar (DNS, ICMP).
    
- **Hunting de LOLBins:** Vigilancia sobre el uso de binarios legítimos (`mshta.exe`, `certutil.exe`, `powershell.exe`) con argumentos sospechosos.
    

## 4. El Flujo de Trabajo (Workflow Táctico)

Este modelo sigue un proceso riguroso para evitar "pescar en el vacío":

1. **Formulación:** Redactar una pregunta clara. _"¿Existe algún proceso legítimo inyectado con código malicioso en mi red?"_.
    
2. **Identificación de Datos:** Determinar qué logs necesito (ej. Sysmon Event ID 10 para inyección de procesos).
    
3. **Ejecución:** Realizar consultas avanzadas en **Kibana** o **Velociraptor**.
    
4. **Confirmación/Refutación:** Analizar los resultados para validar si la hipótesis era correcta.
    

## 5. Cuadro Comparativo: Niveles de Caza

Es fundamental entender dónde se sitúa este enfoque dentro de las capacidades del Hunter:

|**Característica**|**Basado en IoCs (Reactivo)**|**Basado en Hipótesis (Proactivo)**|
|---|---|---|
|**Dificultad**|Baja (Automatizable con feeds)|Alta (Requiere analista experto)|
|**Durabilidad**|Muy Baja (Los IPs/Hashes mueren rápido)|Muy Alta (Los TTPs son duraderos)|
|**Valor Estratégico**|Operativo / Limpieza|Estratégico / Maduración del SOC|
|**Enfoque**|Artefactos estáticos|Comportamientos dinámicos|

## 6. Fuentes de Datos Críticas (Telemetría Requerida)

Para que el hunting basado en hipótesis sea viable, el laboratorio debe contar con visibilidad total sobre los siguientes objetos, tal como indica la taxonomía técnica del curso:

|**Objeto de Investigación**|**Atributos Críticos a Analizar**|
|---|---|
|**Procesos (Endpoint)**|Parent/Child relationship, Command Line arguments, DLLs cargadas.|
|**Red (Network)**|Conexiones persistentes de bajo ancho de banda (Beacons), certificados TLS inusuales.|
|**Sistema Operativo**|Modificaciones en claves de registro críticas, creación de usuarios locales, limpieza de logs.|
|**Archivos**|Creación de ejecutables en directorios temporales (`AppData`, `Temp`).|

---

### Referencias Externas

- [MITRE ATT&CK Framework](https://www.google.com/url?sa=E&source=gmail&q=https://attack.mitre.org/)
    
- [The Threat Hunting Project: Hypothesis Generation](https://www.google.com/search?q=https://www.threathunting.net/hunts)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]
[[Threat Hunting basado en IoCs (IoC-Driven)]]
[[Threat Hunting basado en Analítica (Analytics-Driven)]]