# 🌐 Laboratorio 01: Auditoría Básica de Red y Diagnóstico de Conectividad

## 1. Objetivo
Verificar la configuración de red, analizar el enrutamiento de paquetes, inspeccionar registros DNS y auditar puertos activos en entornos híbridos (**Windows 10** y **Kali Linux**).

## 2. Entorno utilizado
* **Host:** Windows 10 (CMD / PowerShell)
* **Virtualización:** Oracle VirtualBox (Kali Linux)

## 3. Desarrollo técnico y hallazgos

### A. Configuración de red e interfaces (`ipconfig /all` e `ip a`)
* Identificación de direccionamiento IPv4 privado (`192.168.1.0/24`), puerta de enlace predeterminada (`192.168.1.1`) y servidores DNS del proveedor.
* Validación de concesiones DHCP (*leases*) y adaptadores virtuales de red.

### B. Diagnóstico de conectividad y detección de SO mediante TTL (`ping`)
* Ejecución de pruebas ICMP contra servidores públicos (`1.1.1.1`).
* **Análisis:** La respuesta con `TTL=56` confirma que el servidor de destino opera sobre un núcleo Linux/Unix (valor inicial de 64 menos 8 saltos de enrutamiento).

### C. Trazado de rutas y filtrado de firewalls (`tracert` / `traceroute`)
* Comparativa entre el comportamiento de Windows (ICMP) y Linux (UDP).
* Identificación de routers intermedios con filtrado de paquetes ICMP (`* * * Tiempo de espera agotado`) sin pérdida de conectividad final.

### D. Resolución de nombres y auditoría de conexiones (`nslookup`, `dig` y `netstat -an`)
* Verificación de registros DNS tipo `A` y valores de caché (`TTL` de 300 segundos).
* Revisión de sockets locales en estado `LISTENING` (puertos de servicio como SMB `445`) y conexiones salientes `ESTABLISHED` (tráfico HTTPS `443` y consultas DNS `53`).

## 4. Conclusión de seguridad
El dominio de las herramientas nativas de diagnóstico permite detectar rápidamente interfaces no autorizadas, conexiones salientes sospechosas y comportamientos de filtrado perimetral sin depender de software externo.
