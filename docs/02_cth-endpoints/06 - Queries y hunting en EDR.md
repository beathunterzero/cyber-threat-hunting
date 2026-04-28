## 1. ¿Qué es el hunting en EDR?

Proceso **proactivo** para buscar amenazas directamente en endpoints.

Permite:

- Analizar procesos, red, archivos y autenticaciones
    
- Detectar TTPs no cubiertos por reglas
    
- Ejecutar acciones de respuesta
    

---

## 2. Ciclo del hunt

### 2.1 Preparación

- Definir fuentes: procesos, red, archivos, registro
    
- Establecer retención de datos
    
- Normalizar campos
    
- Validar cobertura de agentes
    

---

### 2.2 Hipótesis

- Basada en TTPs, IoCs o alertas
    
- Debe ser clara y accionable
    

Ejemplo:

- PowerShell con comandos codificados
    

---

### 2.3 Diseño de queries

- Tipo:
    
    - IoC
        
    - comportamiento
        
    - anomalía
        
- Optimización:
    
    - filtros por tiempo
        
    - uso de campos indexados
        
    - pruebas en subconjuntos
        

---

### 2.4 Ejecución

- Lanzar query
    
- Definir alcance (hosts, tiempo)
    
- Evaluar volumen de resultados
    

---

### Ejemplo (KQL)

```kql
DeviceProcessEvents
| where FileName == "powershell.exe"
| where ProcessCommandLine contains "EncodedCommand"
| where Timestamp > ago(7d)
| project Timestamp, DeviceId, InitiatingProcessFileName, ProcessCommandLine
```

---

### 2.5 Triage

- Validar resultados
    
- Enriquecer con contexto (IP, hash, procesos)
    
- Filtrar falsos positivos
    

---

### 2.6 Investigación y respuesta

- Recolectar evidencias
    
- Analizar comportamiento
    
- Ejecutar acciones:
    
    - aislar host
        
    - eliminar procesos
        
    - bloquear cuentas
        

---

### 2.7 Detección

- Convertir queries en reglas
    
- Ajustar umbrales
    
- Reducir ruido
    

---

### 2.8 Mejora continua

- Medir:
    
    - MTTD
        
    - MTTC
        
    - dwell time
        
- Mantener repositorio de queries
    
- Repetir ciclo
    

---

## 3. Buenas prácticas

- Pensar en comportamiento, no solo IoCs
    
- Correlacionar múltiples fuentes
    
- Documentar cada hunt
    
- Reutilizar queries
    

---

## Referencias Externas

- [https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-query-language](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-query-language)
    
- [https://attack.mitre.org/datasources/](https://attack.mitre.org/datasources/)
    
- [https://www.sans.org/white-papers/36422/](https://www.sans.org/white-papers/36422/)
    

---

## Documentación Relacionada

[[01 - Técnicas de persistencia y ejecución en endpoints]]