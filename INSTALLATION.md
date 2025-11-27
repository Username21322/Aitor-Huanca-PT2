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
#### 3. Habilita VirtualHost

```bash
sudo a2ensite domini.local.conf
```

#### 4. Reinicia Apache2

```bash
sudo systemctl restart apache2
```

#### 5. Modificar `/etc/hosts` per resoldre el domini localment

Perquè el vostre sistema resolgui el nom de domini `www.domini.local` cap a la vostra màquina, editeu el fitxer `/etc/hosts`:

```bash
sudo nano /etc/hosts
```

Afegiu la línia següent:

```
127.0.0.1   www.domini.local domini.local
```

Això permet que el navegador trobi el vostre lloc web sense necessitat d’un servidor DNS extern.

### 6. Comprovar el funcionament

Obriu un navegador i accediu a:

```
http://www.domini.local
```

Si el directori `/var/www/domini.local` està buit, Apache pot mostrar un error 403 o una llista de directoris (segons la configuració). Per provar que funciona, creeu un fitxer de prova:

```bash
echo "<h1>Hola, benvingut domini.local</h1>" | sudo tee /var/www/domini.local/index.html
```

Torneu a carregar la pàgina i hauríeu de veure el missatge.

### 7. Solució de problemes: Registres d’Apache2

Si el lloc no funciona com s’espera, consulteu els registres d’Apache:

### Registre d’errors
Conté missatges sobre errors de configuració, permisos, fitxers no trobats, etc.

```bash
sudo tail -f /var/log/apache2/domini.local_error.log
```

### Registre d’accés
Mostra totes les peticions rebudes pel servidor.

```bash
sudo tail -f /var/log/apache2/domini.local_access.log
```

> **Consell:** Useu `tail -f` per veure les entrades en temps real mentre proveu el lloc.

### 8. Assignació de permisos

Apache2 s’executa normalment amb l’usuari `www-data`. Per evitar problemes de permisos, configureu el propietari i els permisos del directori del vostre lloc:

### Canviar el propietari
Permet que el vostre usuari pugui editar fitxers i que Apache els pugui llegir:

```bash
sudo chown -R $USER:www-data /var/www/domini.local
```

### Establir permisos adequats
Assegureu-vos que el propietari i el grup tinguin accés complet, i que altres usuaris només puguin llegir:

```bash
sudo chmod -R 775 /var/www/domini.local
```

### Guia d’instal·lació i configuració de plataformes cloud (Nextcloud / ownCloud)  
**Dins d’un virtual host preconfigurat (`/var/www/domini.local`)**

Aquesta guia explica com instal·lar **Nextcloud** o **ownCloud** en un entorn on ja tens un **virtual host actiu** apuntant a `/var/www/domini.local` (per exemple, `domini.local`). No cal configurar Apache ni el virtual host, ja que es considera ja operatiu.



## 1. Descàrrega i instal·lació de la plataforma cloud

### 1.1. Enllaços oficials

- **Nextcloud**: [https://www.nextcloud.com](https://www.nextcloud.com)  
  Descàrrega directa:  
  [https://download.nextcloud.com/server/releases/latest.zip](https://download.nextcloud.com/server/releases/latest.zip)

- **ownCloud**: [https://www.owncloud.org](https://www.owncloud.org)  
  Descàrrega directa (versió estable):  
  [https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip](https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip)

> **Nota**: Nextcloud és compatible amb PHP 8.1+, mentre que **ownCloud encara requereix PHP 7.4** en moltes versions estables. Assegura’t de tenir la versió de PHP adequada abans d’instal·lar.


### 1.2. Passos d’instal·lació

1. **Mou’t al directori del virtual host**:
   ```bash
   cd /var/www/domini.local
   ```
2. **Neteja el contingut actual** (si cal):
   > Assegura’t que no hi ha dades importants abans d’executar això.
   ```bash
   sudo rm -rf *
   ```
   
3. **Descarrega el fitxer `.zip`** de la plataforma triada (Nextcloud o ownCloud) al teu sistema.
    ```bash
    wget https://download.nextcloud.com/server/releases/latest.zip
   ```

4. **Descomprimeix l’arxiu directament al directori**:

   - **Heu descarregat l'arxiu a una ruta qualsevol**
   ```bash
   sudo unzip /ruta/al/arxiu.zip
   ```
   > Si l’arxiu crea una carpeta interna (ex: `nextcloud/` o `owncloud/`), assegura’t que el contingut es mogui **al nivell arrel** del virtual host:
   ```bash
   sudo mv nextcloud/* . && sudo rmdir nextcloud
   # o
   sudo mv owncloud/* . && sudo rmdir owncloud
   ```

   - **Podeu fer això directament si ho teniu descomprimit a `Descargas`:**
   ```bash
   cp -R ~/Descargas/nextcloud/. /var/www/domini.local/.
   ```
   Elimineu la carpeta `nextcloud` i l'arxiu `latest.zip`
    ```bash
    sudo rm -rf ~/Descargas/nextcloud && sudo rm -rf ~/Descargas/latest.zip
    ```

   - **Podeu fer això directament si ho teniu descomprimit a `/var/www/domini.local`:**
   ```bash
   cp -R /var/www/domini.local/nextcloud/. /var/www/domini.local/.
   ```
   Elimineu la carpeta `nextcloud` i l'arxiu `latest.zip`
    ```bash
    sudo rm -rf /var/www/domini.local/nextcloud && sudo rm -rf /var/www/domini.local/latest.zip
    ```
6. **Assegura els permisos correctes**:
   ```bash
   sudo chown -R www-data:www-data /var/www/domini.local
   sudo chmod -R 755 /var/www/domini.local
   ```

7. **Accedeix a la interfície web**:
   Obre el navegador i visita:
   ```
   http://domini.local
   ```
   Segueix les instruccions de configuració assistida:
   - Crea un usuari administrador.
   - Configura la base de dades (recomanat: MariaDB/MySQL).
   - Verifica que tots els requisits del sistema es compleixin.

## 2. Recomanacions addicionals

- **Directori de dades**: Durant la instal·lació, es recomana **no emmagatzemar les dades dins del directori web** (ex: `/var/www/domini.local/data`). Millor usa una ruta externa com `/var/ncdata` o `/opt/owncloud-data`.
- **Còpies de seguretat**: Fes *backups* regulars del directori de dades i de la base de dades.
- **Seguretat**: Desactiva l’accés a fitxers sensibles (`.htaccess`, `config.php`) i considera afegir regles de seguretat addicionals a Apache o Nginx.


## Apèndix: Instal·lació de PHP 7.4 a Ubuntu 24.04 (només per a ownCloud)

> **Aquest pas només és necessari si instal·les ownCloud**, ja que moltes versions estables encara no són compatibles amb PHP 8.3 (versió per defecte a Ubuntu 24.04). Nextcloud **no requereix aquest pas**.

### Passos:

1. **Actualitza el sistema**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Instal·la les dependències per afegir repositoris PPA**:
   ```bash
   sudo apt install software-properties-common -y
   ```

3. **Afegeix el repositori de PHP de Ondřej Surý**:
   ```bash
   LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
   ```

4. **Actualitza els repositoris**:
   ```bash
   sudo apt update
   ```

5. **Instal·la PHP 7.4 i les extensions requerides**:
   ```bash
   sudo apt install -y php7.4 \
       libapache2-mod-php7.4 \
       php7.4-fpm \
       php7.4-common \
       php7.4-mbstring \
       php7.4-xmlrpc \
       php7.4-soap \
       php7.4-gd \
       php7.4-xml \
       php7.4-intl \
       php7.4-mysql \
       php7.4-cli \
       php7.4-ldap \
       php7.4-zip \
       php7.4-curl
   ```

6. **(Opcional) Selecciona PHP 7.4 com a versió per defecte**:
   ```bash
   sudo update-alternatives --config php
   ```

7. **Activa els mòduls d’Apache necessaris**:
   ```bash
   sudo a2enmod proxy_fcgi setenvif
   sudo a2enconf php7.4-fpm
   ```

8. **Reinicia Apache**:
   ```bash
   sudo systemctl restart apache2
   ```

> **Verificació**: Pots comprovar la versió activa de PHP amb:
> ```bash
> php -v
> ```
