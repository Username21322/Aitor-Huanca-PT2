# Manual d'instalació

## Configuració del sistema de virtualització (IsardVDI)

- Entra a la interfície web d’IsardVDI mitjançant el navegador.

![Cap1](captura.md/Cap1)
- Inicia sessió amb un usuari amb permisos d’administrador.
  
![captura](https://github.com/user-attachments/assets/806aa7fc-d6b6-4f3c-b722-e50d21853dd0)

- Crea una maquina virtual a la secció de "Escriptori Nou" a la part superior a la dreta.

![captura](https://github.com/user-attachments/assets/0a3f93e7-a217-42ae-8f52-036a693fcf98)

- Introdueix les dades bàsiques:
    - Nom de la màquina (ex: owncloud-server)
    - Sistema operatiu "Ubuntu-24.04-desktop"
![captura](https://github.com/user-attachments/assets/c0f3327f-8de2-4968-b554-d11687371246)

- Configura la màquina a la part de "HARDWARE":
    - Recursos: 
        - CPU=2,
        - Memòria RAM=8 GB
![captura]<img width="625" height="120" alt="image" src="https://github.com/user-attachments/assets/0bc89a35-aace-4c6f-8050-924408841672" />

- Assigna la màquina a la xarxa virtual "puigcastellar1".
![captura]<img width="666" height="408" alt="image" src="https://github.com/user-attachments/assets/05975c79-0be3-4fa0-b786-31d333de5fad" />

- Habilita accés remot (RDP, SPICE o VNC), preferiblement "SPICE".
![captura]<img width="1192" height="232" alt="image" src="https://github.com/user-attachments/assets/447b1fd0-44a5-44a3-8884-e8d4d9eb2d42" />

- Crea la màquina
![captura]<img width="283" height="118" alt="image" src="https://github.com/user-attachments/assets/ac68aa4e-e0a3-4b5f-996b-dfe9e1172755" />

## Procés de configuració del sistema operatiu del sistema

- Inicia la máquina
![captura]<img width="299" height="307" alt="image" src="https://github.com/user-attachments/assets/3490b91a-2907-4d10-8da8-15ef3e10c446" />

- Selecciona "SPICE"
![captura]<img width="299" height="307" alt="image" src="https://github.com/user-attachments/assets/1d668d91-dc10-4669-96f1-205b9cf40b2d" />



## Procés d'instalació de gestor d'arxius "NextCloud"
### Configuració del sistema operatiu (LAMP)
Abans de tot es selecciona a la part de configuració de l'usuari "Ubuntu" en comptes de Ubuntu en Xorg

<img width="605" height="182" alt="image" src="https://github.com/user-attachments/assets/eda46062-ff80-4aae-9cff-320defcbcf59" />

La contraseña es "usuario"

Una vez dentro de la máquina busca "CMD" o "Terminal" y abrelo para hacer la configuración.

<img width="592" height="279" alt="image" src="https://github.com/user-attachments/assets/9776c71a-c55d-4536-923b-df2676020f8e" />

#### 1. Actualiza el Sistema con el comando siguiente:

```bash
sudo apt update && sudo apt upgrade -y
```
#### 2. Instala Apache

```bash
sudo apt install apache2 -y
```

#### 3. Habilita/Inicia el servicio

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

#### 4. Verifica el esatado

```bash
sudo systemctl status apache2
```
Para ver la pagina predeterminada de Apache escribe en google el enlaze EN LA MÁQUINA VIRTUAL. Enlace: `http://localhost`

#### 5. Instala MySQL

```bash
sudo apt install mysql-server mysql-client -y
```

#### 6. Habilita/Inicia el servicio de MySQL

```bash
sudo systemctl enable mysql
sudo systemctl start mysql
```
#### 7. Accede a la consola de MySQL

```bash
sudo mysql
```
#### 8. Crea la base de datos

```sql
CREATE DATABASE bbdd;
```
#### 9. Creación del usuario local

```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL PRIVILEGES ON bbdd.* TO 'usuario'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
#### 10. Instala PHP y sus extensiones comunes

```bash
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-zip php-json php-cli -y
```
#### 11. Reinicia APACHE para cargar PHP

```bash
sudo systemctl restart apache2
```

#### 12. Verifica la versión de PHP

```bash
php -v
```

#### 13. Crea un fitxero de prueba 

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```
##### Visita `http://localhost/info.php` para ver la información de PHP

#### 13.1 Después de comprobar que este bien, elimina el archivo

```bash
 sudo rm /var/www/html/info.php
```
### Configuració de VirtualHost

#### 1. Ponemos un ejemplo

```bash
sudo mkdir -p /var/www/domini.local
```
#### 2. Definimosw VirtualHost

```bash
sudo nano /etc/apache2/sites-available/domini.local.conf
```

##### Pon la configuración siguiente:

```apache
<VirtualHost *:80>
    ServerAdmin admin@domini.local
    ServerName www.domini.local
    ServerAlias domini.local
    DocumentRoot /var/www/domini.local
    ErrorLog ${APACHE_LOG_DIR}/domini.local_error.log
    CustomLog ${APACHE_LOG_DIR}/domini.local_access.log combined
</VirtualHost>
```
