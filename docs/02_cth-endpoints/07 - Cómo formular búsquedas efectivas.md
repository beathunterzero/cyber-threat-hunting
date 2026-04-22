## 1. Definición y Metodología Base

La formulación de búsquedas efectivas en Threat Hunting no es un proceso de prueba y error, sino una **secuencia lógica que combina pensamiento analítico, conocimiento técnico y una metodología estructurada**. El objetivo es traducir una hipótesis de caza abstracta en una consulta técnica precisa y procesable dentro del SIEM o EDR.

## 2. Secuencia Lógica de Búsqueda (Fases Core)

El proceso de formulación sigue 5 pasos estrictos y secuenciales:

### **Paso 1: Definir el objetivo de la búsqueda**

Antes de escribir cualquier línea de código (KQL, VQL, Splunk SPL), el Hunter debe tener clara su meta.

- **Implicación:** Establecer claramente qué tipo de amenaza o comportamiento anómalo se desea identificar en la infraestructura. Sin un objetivo delimitado (ej. "Encontrar persistencia mediante tareas programadas"), la caza carecerá de rumbo.
    

### **Paso 2: Seleccionar las fuentes de datos adecuadas**

El éxito de la búsqueda depende directamente de la calidad y variedad de los datos analizados.

- **Fuentes Críticas Incluyen:** * Logs de endpoints (ej. Sysmon, Eventos de Windows).
    
    - Tráfico de red (Netflow, DNS, Proxy).
        
    - Registros del SIEM.
        
    - Eventos de autenticaciones (AD, Entra ID).
        
    - Telemetría del sistema operativo.
        

### **Paso 3: Diseñar la consulta o query de búsqueda**

Es la traducción técnica del objetivo a la sintaxis de la herramienta.

- **El Equilibrio Clave:** Una búsqueda demasiado amplia genera "ruido blanco" y una avalancha de falsos positivos (fatiga de alertas), mientras que una búsqueda demasiado restrictiva o específica puede omitir eventos críticos y dejar pasar al adversario.
    

### **Paso 4: Analizar los resultados obtenidos y correlacionarlos con el contexto**

Los datos crudos obtenidos de la consulta deben transformarse en inteligencia accionable.

- **Correlación:** Se utilizan conocimientos avanzados sobre tácticas, técnicas y procedimientos (TTPs) del adversario para dar sentido a los resultados.
    
- **Framework Estándar:** Esta correlación generalmente se organiza y mapea bajo marcos de la industria como **MITRE ATT&CK**.
    

### **Paso 5: Documentar los hallazgos y refinar la búsqueda**

El Threat Hunting es un proceso iterativo de mejora continua.

- **Retroalimentación:** Cada búsqueda ofrece lecciones operativas que permiten ajustar los parámetros, mejorar la eficiencia de las consultas y optimizar futuras investigaciones. Los hallazgos positivos confirmados deben transicionar a reglas de detección automatizadas.
    

---

### Referencias Externas

- [MITRE ATT&CK: Design and Evaluate Threat Hunting](https://www.google.com/url?sa=E&source=gmail&q=https://mitre-attack.github.io/attack-navigator/)
    
- [SANS Institute: Threat Hunting Methodology](https://www.google.com/search?q=https://www.sans.org/white-papers/36422/)
    

### Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]