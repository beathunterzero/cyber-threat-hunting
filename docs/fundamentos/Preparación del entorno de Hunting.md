## 1. Definición y Propósito

La **preparación del entorno** es el primer paso operativo y la fase fundamental para garantizar que el analista cuente con las herramientas, datos y accesos necesarios antes de iniciar cualquier búsqueda de amenazas. Sin una visibilidad adecuada (telemetría), el Threat Hunting se vuelve imposible. El objetivo es configurar una infraestructura capaz de recolectar, centralizar y analizar eventos en tiempo real e histórico.

## 2. Componentes de la Infraestructura de Hunting

Un entorno robusto se compone de tres capas principales:

- **Fuentes de Datos (Endpoints y Red):** Generan los eventos crudos (Logs de Windows, Sysmon, tráfico de red).
    
- **Agentes de Recolección (EDR/Forwarders):** Herramientas como **Velociraptor** y **Elastic Agent** que extraen y envían la telemetría.
    
- **Plataforma de Análisis (SIEM):** El stack de **Elastic Security** donde se normalizan, indexan y consultan los datos mediante KQL.
    

## 3. Fuentes de Datos Críticas (Telemetría)

|**Fuente**|**Tipo de Datos**|**Utilidad en el Hunting**|
|---|---|---|
|**Windows Event Logs**|Seguridad, Sistema, Aplicación.|Autenticaciones (4624/4625), creación de servicios.|
|**Sysmon**|Telemetría profunda de procesos.|Identificación de inyección de código, conexiones de red por proceso.|
|**EDR (Velociraptor)**|Artefactos forenses (MFT, Registro).|Análisis de persistencia y recolección de evidencias en "caliente".|
|**Logs de Red**|DNS, TLS, HTTP, Netflow.|Detección de balizamiento (Beacons) y exfiltración.|

## 4. El Modelo Diamante en la Recolección

Al preparar el entorno, debemos asegurar que la telemetría recolectada nos permita completar los cuatro vértices del **Diamond Model**:

1. **Víctima:** Logs que identifiquen el host, usuario o activo afectado.
    
2. **Infraestructura:** Logs de red que muestren IPs, dominios y certificados.
    
3. **Capacidad:** Telemetría de endpoint que capture el malware o herramientas.
    
4. **Adversario:** Datos que permitan atribuir el ataque mediante el cruce con CTI.
    

## 5. Configuración Técnica del Laboratorio (Elastic + Velociraptor)

- **Paso 1: Configuración de Auditoría:** Habilitar logs detallados (GPO) e instalar **Sysmon**.
    
- **Paso 2: Despliegue de Agentes:** Instalación de Elastic Agent y Velociraptor.
    
- **Paso 3: Ingesta en SIEM:** Verificación de que los datos llegan correctamente a Elastic.
    
- **Paso 4: Validación de Visibilidad:** Realizar una acción conocida y verificar su registro completo.
    

## 6. Calidad del Dato (Data Quality)

- **Consistentes:** Uso del **Elastic Common Schema (ECS)**.
    
- **Oportunos:** Mínima latencia de ingesta.
    
- **Contextualizados:** Inclusión de metadatos del activo.
    

## 7. Comparativa de Enfoques de Datos y Herramientas

|**Herramienta / Enfoque**|**Tipo de Detección**|**Nivel de Visibilidad**|**Carga de Análisis**|
|---|---|---|---|
|**SIEM (Elastic)**|Reglas y firmas (IoCs/TTPs).|Media/Alta.|Baja/Media.|
|**EDR (Velociraptor)**|Comportamiento y forense.|Máxima.|Alta.|
|**Network (Zeek)**|Protocolos y flujos.|Alta.|Media.|
|**Threat Intelligence**|Contexto externo.|N/A.|Baja.|

## 8. Pilares Operativos de la Preparación

Antes de iniciar la búsqueda, se deben garantizar estos seis pilares estratégicos:

1. **Objetivos:** Asegurar visibilidad total, integridad de la información y eficiencia en el análisis de datos.
    
2. **Centralización:** Acceso centralizado a logs de endpoints, tráfico de red, DNS, autenticación y sistemas en la nube.
    
3. **Herramientas:** Implementar EDR, SIEM, SOAR y utilidades forenses para análisis de memoria, tráfico y malware.
    
4. **Accesos y permisos:** Otorgar al equipo de hunting accesos controlados pero suficientes para consultas profundas.
    
5. **Validación:** Comprobar que los logs estén completos, sincronizados en tiempo y libres de errores de recolección.
    
6. **Entorno seguro:** Utilizar laboratorios aislados (**sandboxes**) para ejecutar muestras sospechosas sin riesgo.
    

---

### Referencias Externas

- [SANS Institute: Blue Team Handbook](https://www.google.com/search?q=https://www.sans.org/white-papers/36302/)
    
- [Elastic Common Schema (ECS) Documentation](https://www.elastic.co/guide/en/ecs/current/index.html)
    
- [Velociraptor Documentation & Artifact Reference](https://docs.velociraptor.app/)
    
- [Microsoft: Sysmon Documentation](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
    

### Documentación Relacionada

[[Filosofía y estrategia del Threat Hunting]]