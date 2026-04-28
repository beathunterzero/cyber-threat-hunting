## 1. ¿Qué es el IoC-Driven Hunting?

El **Threat Hunting basado en IoCs** utiliza indicadores conocidos obtenidos de **Ciberinteligencia (CTI)** para buscar evidencia de actividad maliciosa en el entorno.

- Parte de datos ya conocidos
    
- Busca presencia **histórica o actual**
    
- Enfocado en artefactos específicos (no comportamiento)
    

---

## 2. Tipos de IoCs en red

Clasificación de indicadores según su uso en infraestructura atacante:

|Categoría|Indicadores|Valor|
|---|---|---|
|TLS/SSL|JA3/JA3S, SNI, certificados|Identifica herramientas y C2|
|SSH|Claves públicas, algoritmos|Relación entre campañas|
|Dominios|DGA, dominios nuevos, typosquatting|Infraestructura maliciosa|
|DNS|Queries largas, TXT inusuales, frecuencia alta|C2 encubierto / exfiltración|

---

## 3. Flujo de un IoC Hunt

1. **Ingesta CTI**
    
    - Recepción de indicadores (reportes, feeds)
        
2. **Extracción de IoCs**
    
    - Dominios, hashes, certificados, patrones
        
3. **Búsqueda en logs**
    
    - Consultas en SIEM (ej. Kibana)
        
4. **Validación**
    
    - Filtrar falsos positivos
        
    - Verificar contexto (servicios legítimos vs maliciosos)
        

---

## 4. Limitaciones del enfoque

El IoC Hunting opera en niveles bajos de la detección:

- **Alta rotación:** IPs, dominios y certificados cambian rápido
    
- **Fácil evasión:** uso de infraestructura legítima (CDN, cloud)
    
- **Poca durabilidad:** detección de corto plazo
    

---

## 5. Ejemplos prácticos (KQL)

- **SNI sospechoso**
    
    ```kql
    network.protocol: "tls" AND tls.server.name: /.*secure-update.*/
    ```
    
- **Dominios tipo DGA**
    
    ```kql
    dns.question.name: /.{25,}/
    ```
    
- **JA3 conocido**
    
    ```kql
    tls.client.ja3_hash: "7739105ed22b10..."
    ```
    

---

## 6. Prioridad de indicadores

Clasificación según valor operativo:

|Tipo|Obtención|Valor|
|---|---|---|
|IoCs públicos|Alta|Bajo|
|IoCs específicos|Media|Alto|
|IoCs propios|Baja|Muy alto|
|TTPs|Muy baja|Máximo|

---

## Referencias Externas

- [https://attack.mitre.org/](https://attack.mitre.org/)
    
- [https://www.sans.org/white-papers/35502/](https://www.sans.org/white-papers/35502/)
    
- [https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)
    

---

## Documentación Relacionada

[[01 - Filosofía y estrategia del Threat Hunting]]  
[[05 - Threat Hunting basado en Hipótesis (Hypothesis-Driven)]]  
[[06 - Threat Hunting basado en Analítica (Analytics-Driven)]]