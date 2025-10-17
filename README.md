# Instalador de entorno LAMP

Este script sirve para instalar y configurar un entorno LAMP (Linux, Apache, MySQL, PHP) de forma automática en un sistema Ubuntu

---

## Script

```bash
#!/bin/bash
```
Indica que el script debe ejecutarse con Bash

---

```bash
set -ex
```
Activa dos opciones:
- -e: hace que el script se detenga si ocurre un error. 
- -x: muestra por pantalla cada comando que se ejecuta

---

```bash
apt update
```
Actualiza la lista de paquetes disponibles  

---

```bash
apt upgrade
```
Actualiza todos los paquetes instalados a las ultimas versiones disponibles

---

```bash
apt install apache2 -y
```
Instala el servidor web Apache2, que será el encargado de servir las páginas web.  
El parámetro `-y` responde automáticamente si a todas las confirmaciones durante la instalación.

---

```bash
apt install php libapache2-mod-php php-mysql -y
```
Instala **PHP** y los módulos necesarios para integrarlo con Apache y MySQL:
- `php`: el lenguaje de programación del lado del servidor.  
- `libapache2-mod-php`: módulo que permite que Apache ejecute archivos `.php`.  
- `php-mysql`: extensión que permite a PHP conectarse con bases de datos MySQL/MariaDB.  
El `-y` nuevamente evita que el sistema solicite confirmación manual.

---

```bash
cp ../conf/000-default.conf /etc/apache2/sites-available/000-default.conf
```
Copia el archivo de configuración del sitio web por defecto desde el directorio `../conf/` (carpeta superior) hacia la ruta real de configuración de Apache:  
`/etc/apache2/sites-available/000-default.conf`.

Esto permite aplicar una configuración personalizada al sitio web principal.

---

```bash
systemctl restart apache2
```
Reinicia el servicio **Apache2** para que se apliquen los cambios realizados en su configuración.  
`systemctl` es el comando de control de servicios en sistemas que usan *systemd*.

---

```bash
cp ../php/index.php /var/www/html
```
Copia el archivo `index.php` desde la carpeta `../php/` (una carpeta superior) hasta el directorio raíz del servidor web `/var/www/html`.  
De esta forma, Apache servirá este archivo cuando se acceda a `http://localhost/`.

---

## Resultado
