## 1. Definición y Propósito

El **Modelo de Madurez de Capacidad de Threat Hunting (Hunting Maturity Model)** es un marco estratégico diseñado para evaluar, estructurar y evolucionar las capacidades de detección proactiva de una organización. Permite trazar una hoja de ruta clara para pasar de una postura puramente reactiva a un enfoque continuo y optimizado.

El modelo se divide en tres pilares evaluados a lo largo de cinco niveles de madurez.

> [!INFO] Nota sobre Requisitos Previos
> 
> Los elementos marcados en _cursiva_ en las siguientes tablas no son estrictamente parte de una capacidad pura de Threat Hunting, pero se consideran **requisitos previos y facilitadores esenciales** para poder ejecutar las cacerías.

---

## 2. Los 3 Pilares del Modelo de Madurez

### Pilar 1: Personas (People)

Enfocado en el talento humano, la capacitación y la estructura del equipo de analistas.

|**Nivel de Madurez**|**Características del Equipo y Capacitación**|
|---|---|
|**Nivel 1: Inicial**|• Analistas de SOC existentes.<br><br>  <br><br>• Necesidades de recursos y capacitación desconocidas.<br><br>  <br><br>• Rendimiento no gestionado y falta de plan de desarrollo.<br><br>  <br><br>• _Comportamiento normal de sistemas insuficientemente comprendido._|
|**Nivel 2: Gestionado**|• Líder de Threat Hunting asignado.<br><br>  <br><br>• Visión informal de recursos y capacitación.<br><br>  <br><br>• El rendimiento se gestiona cualitativamente.<br><br>  <br><br>• _Comportamiento normal de sistemas moderadamente comprendido._|
|**Nivel 3: Definido**|• Hunters de amenazas dedicados.<br><br>  <br><br>• Planes formales de reclutamiento, capacitación y desarrollo profesional.<br><br>  <br><br>• Expectativas de rendimiento definidas con perfiles de rol.<br><br>  <br><br>• _Comportamiento normal de sistemas totalmente comprendido._|
|**Nivel 4: Cuantitativo**|• Analistas de SOC rotados para Aprendizaje y Desarrollo (L&D).<br><br>  <br><br>• Planes de sucesión implementados.<br><br>  <br><br>• Métricas utilizadas para evaluar el rendimiento del equipo.<br><br>  <br><br>• Sistemas críticos para la misión identificados.|
|**Nivel 5: Optimizado**|• Equipos integrados en todo el SOC.<br><br>  <br><br>• Necesidades de recursos y capacitación totalmente integradas.<br><br>  <br><br>• Planes de mejora para abordar el bajo rendimiento.<br><br>  <br><br>• Conciencia situacional plena.|

---

### Pilar 2: Procesos (Process)

Enfocado en cómo se generan las hipótesis, la recopilación de datos y el uso de inteligencia.

|**Nivel de Madurez**|**Características del Proceso Operativo**|
|---|---|
|**Nivel 1: Inicial**|• Generación de hipótesis no estructurada.<br><br>  <br><br>• Poca comprensión de anomalías indicativas de actividad maliciosa.<br><br>  <br><br>• _Las cazas ocurren ad-hoc (si ocurren) con poca/ninguna recopilación de datos._|
|**Nivel 2: Gestionado**|• La CTI y la experiencia se usan para generar hipótesis priorizadas.<br><br>  <br><br>• Se utilizan feeds de amenazas básicos. Búsqueda dirigida a IOCs (base de la Pirámide del Dolor).<br><br>  <br><br>• _Las cazas ocurren ocasionalmente con recopilación moderada de datos._|
|**Nivel 3: Definido**|• Proceso de caza formal.<br><br>  <br><br>• La CTI se usa para detectar actividad maliciosa; búsqueda dirigida a IOCs en el medio de la Pirámide.<br><br>  <br><br>• _Cazas regulares con alta recopilación de datos de áreas clave._|
|**Nivel 4: Cuantitativo**|• Puntuación de riesgo manual (evaluación de "Joyas de la Corona").<br><br>  <br><br>• CTI adaptada específicamente a la organización. Búsqueda dirigida a TTPs.<br><br>  <br><br>• _Cazas frecuentes con recopilación de datos de la mayor parte de la infraestructura._|
|**Nivel 5: Optimizado**|• Puntuación de riesgo automatizada (ej. Machine Learning).<br><br>  <br><br>• Seguimiento automatizado de TTPs y campañas. Analíticas compartidas con la comunidad.<br><br>  <br><br>• _Cazas continuas con alta recopilación de toda la infraestructura._|

---

### Pilar 3: Herramientas (Tools)

Enfocado en la tecnología utilizada para buscar, automatizar y documentar.

|**Nivel de Madurez**|**Características Tecnológicas y de Automatización**|
|---|---|
|**Nivel 1: Inicial**|• Poca o ninguna automatización.<br><br>  <br><br>• Poca o ninguna documentación producida.<br><br>  <br><br>• _Uso exclusivo de herramientas de SOC reactivas._|
|**Nivel 2: Gestionado**|• Búsquedas básicas mediante texto o consultas tipo SQL.<br><br>  <br><br>• Documentación utilizando suites ofimáticas básicas.<br><br>  <br><br>• _Coincidencia automática de IOCs._|
|**Nivel 3: Definido**|• Técnicas de análisis estadístico.<br><br>  <br><br>• Biblioteca de procedimientos de caza automatizada en horario regular.<br><br>  <br><br>• Flujo de trabajo central y herramientas de repositorio de conocimiento.<br><br>  <br><br>• _Uso de entornos de laboratorio para generación/prueba de hipótesis._|
|**Nivel 4: Cuantitativo**|• Uso de herramientas de visualización analítica probadas para su efectividad.<br><br>  <br><br>• Biblioteca de procedimientos de caza automatizada en un horario frecuente.<br><br>  <br><br>• Uso intensivo de Dashboards operativos.|
|**Nivel 5: Optimizado**|• Se aprovecha el Machine Learning (escaneo del horizonte prospectivo).<br><br>  <br><br>• Biblioteca de procedimientos de caza automatizada continuamente.<br><br>  <br><br>• Repositorio de conocimiento integrado y compartido globalmente.|

---

## 3. Aplicación Práctica en el Laboratorio

Para el entorno de laboratorio actual centrado en la respuesta a incidentes en la nube y endpoints (Fedora/Windows, Elastic, Velociraptor), el objetivo a corto plazo es consolidar el **Nivel 3 (Definido)**:

- **Personas:** Actuar como un Hunter dedicado, comprendiendo a fondo el "baseline" del entorno simulado.
    
- **Procesos:** Dejar de depender de simples IOCs (hashes, IPs) y enfocar las cacerías en comportamientos y anomalías (el medio de la Pirámide del Dolor).
    
- **Herramientas:** Utilizar la bóveda de Obsidian como el "Repositorio de conocimiento central" y mantener las _queries_ de KQL/VQL organizadas para ejecución regular.
    

---

### Referencias Externas

- [SANS Institute: The Threat Hunting Maturity Model](https://www.google.com/search?q=https://www.sans.org/white-papers/37702/)
    
- [Sqrrl: Threat Hunting Reference Architecture (Origin of the Model)](https://www.threathunting.net/)
    

### Documentación Relacionada

[[02 - Técnicas de comunicación de C2 y exfiltración]]
[[03 - Detección de beaconing y tráfico anómalo]]
[[04 - DNS tunneling, HTTPs sospechoso y uso de Tor]]
[[05 - Threat Hunting en SIEM]]
[[06 - Ejemplo de hipótesis en SIEM]]
[[07 - Casos de hunting basados en logs de firewall, proxy y autenticación]]
[[08 - Integración con CTI]]
[[09 - Uso de IoCs de fuentes abiertas]]
[[10 - Convertir inteligencia en hipótesis de hunting]]
[[01 - Filosofía y estrategia del Threat Hunting]]