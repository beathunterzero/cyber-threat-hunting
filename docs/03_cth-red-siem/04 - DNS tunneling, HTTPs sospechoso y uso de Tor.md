## 1. ¿Qué se busca?

Detectar uso de canales encubiertos para:

- **C2**
    
- **Exfiltración**
    

Clave:

- El tráfico parece legítimo (DNS / HTTPS)
    

---

## 2. DNS Tunneling

Uso de DNS para transportar datos.

### Indicadores:

- Dominios largos o aleatorios
    
- Alta entropía en `qname`
    
- Muchas consultas a un mismo dominio
    
- Uso de registros `TXT`
    

---

## 3. HTTPS sospechoso

Uso de TLS para ocultar C2.

### Indicadores:

- Dominio consultado → luego sesión HTTPS persistente
    
- Conexiones largas o repetitivas
    
- Dominios con mala reputación
    
- Tráfico cifrado fuera de patrón
    

---

## 4. Uso de Tor

Oculta origen/destino del atacante.

### Indicadores:

- Resoluciones hacia nodos Tor
    
- IPs conocidas de exit nodes
    
- Actividad DNS asociada a anonimización
    

Acción:

- Bloqueo en resolver DNS
    
- Alertas por listas conocidas
    

---

## 5. Detección basada en comportamiento

### 5.1 Entropía

- Detectar datos codificados
    
- Subdominios no humanos
    

---

### 5.2 Frecuencia

- Muchas consultas en poco tiempo
    
- Patrones repetitivos
    

---

### 5.3 Volumen

- Tamaños de paquetes DNS inusuales
    
- Transferencias fragmentadas
    

---

## 6. Enfoque de hunting

- Analizar DNS + red
    
- Correlacionar con procesos
    
- Detectar desviaciones del baseline
    
- Priorizar dominios desconocidos
    

---

## 7. Objetivo

- Detectar canales ocultos
    
- Identificar exfiltración silenciosa
    
- Bloquear comunicación externa
    

---

## Referencias Externas

- [https://attack.mitre.org/techniques/T1071/004/](https://attack.mitre.org/techniques/T1071/004/)
    
- [https://attack.mitre.org/techniques/T1572/](https://attack.mitre.org/techniques/T1572/)
    
- [https://attack.mitre.org/techniques/T1090/003/](https://attack.mitre.org/techniques/T1090/003/)
    

---

## Documentación Relacionada

[[01 - Guía para la caza de amenazas]]  
[[03 - Detección de beaconing y tráfico anómalo]]