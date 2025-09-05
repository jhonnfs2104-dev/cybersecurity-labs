# Análisis de Metasploitable 2

Este documento detalla los hallazgos durante la auditoría de seguridad de la máquina virtual Metasploitable 2.

## Fase 1: Reconocimiento y Escaneo

El objetivo de esta fase fue identificar los servicios y puertos abiertos en la máquina para determinar posibles vectores de ataque.

---

### Herramientas Utilizadas
* **Nmap:** Para el escaneo de puertos y descubrimiento de servicios.

### Comando Ejecutado
Se utilizó un escaneo TCP completo para enumerar todos los puertos, detectar versiones de servicios y ejecutar scripts básicos de reconocimiento.
```bash
nmap -p- -sV -sC -oN nmap_metasploitable 192.168.3.45

Resultados Clave y Análisis de Vulnerabilidades
El escaneo reveló múltiples servicios con vulnerabilidades conocidas y configuraciones inseguras. Los más críticos son:

Puerto 21/tcp (FTP): Se identificó la versión vsftpd 2.3.4, la cual es conocida por tener una vulnerabilidad de puerta trasera. Además, permite el inicio de sesión anónimo.

Puerto 23/tcp (Telnet): El servicio Telnet está expuesto, lo que representa un riesgo alto ya que transmite credenciales en texto plano.

Puerto 1524/tcp (bindshell): Se encontró un shell de root escuchando en este puerto, lo que permite acceso administrativo inmediato y sin autenticación a la máquina.

Conclusión Inicial
La superficie de ataque de la máquina es extremadamente grande. Basado en los hallazgos, el servicio de FTP (vsftpd 2.3.4) y el bindshell en el puerto 1524 son los puntos de entrada más prometedores para la siguiente fase: Explotación.
