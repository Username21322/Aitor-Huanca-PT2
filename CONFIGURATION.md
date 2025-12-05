# Manual d'instal·lació d’ownCloud amb virtualització mitjançant IsardVDI

# Demostració del funcionament

## Pujar un Arxiu
#### Primerament hem d'anar a la part de "Arxius" de NextCloud, que en anglés seria "Files"

![Captura](Imagenes/imagen1.png)

#### Seguidament li donem al boto on diu "Nou" o en anglés que seria "New"

![Captura](Imagenes/imagen3.png)

#### Després fem click a "Penjar Fitxer" o "Upload Files"

![Captura](Imagenes/imagen2.png)
## Crear una carpeta
#### Al mateix apartat  on pujem un fitxer, li donem a "New Folder" o "Nova Carpeta"

![Captura](Imagenes/imagen4.png)

## Compartició de continguts
Per poder compartir els continguts hen de trobar l'icone blau de compartir que seria el de la imatge seguent:

![Captura](Imagenes/imagen5.png)

Quan li donem a aquest botó, ens sortira dues maneres de compartir el contingut:
- "internal Shares": Seria per compartir amb persones que ja tinguin acces a aqust contingut.
- "External Shares": Seria per donar acces al contingut, ja sigui amb email o per un link.

![Captura](Imagenes/imagen6.png)

## Creació d'usuaris
#### Per começar a crear altres usuaris, hem de donar-li al nostre perfil

![Captura](Imagenes/imagen7.png)

#### Seguidament hen de fer click en "Accounts" o "Comptes"

![Captura](Imagenes/imagen8.png)

## Configuració d’usuaris
### Per crear els usuaris ves a la part d'adalt on diu "Nova Compta" o "New account":

<img width="279" height="101" alt="image" src="https://github.com/user-attachments/assets/023007a6-d603-49af-b4a2-29c4b129d0f1" />

### Per crear els grups has d'anara a la part on diu "Groups" o "Grups" i donar-li al botó "+"

<img width="289" height="81" alt="image" src="https://github.com/user-attachments/assets/57d9ad58-c309-4d2d-b692-241416ee5a1e" />

### Crea els 3 usuaris necesaris:
#### - **Primer crea els Grups: "Admin" "Editor" "Visualitzadors"**

<img width="184" height="117" alt="image" src="https://github.com/user-attachments/assets/a941d12b-97a0-4a50-ae75-4bddfdb2f5d7" />

   - Usuari: **Administrador** → assignat al **grup Admin**.

<img width="410" height="616" alt="image" src="https://github.com/user-attachments/assets/15553023-3fa3-4bef-a0d7-e4a2f66461fe" />

   - Usuari: **Editor** → assignat al **grup Editors**.

<img width="405" height="587" alt="image" src="https://github.com/user-attachments/assets/4e4b796b-9d64-4488-8d14-8907dc75272b" />

   - Usuari: **Visualitzador** → assignat al **grup Visualitzadors**.  

<img width="407" height="588" alt="image" src="https://github.com/user-attachments/assets/e3d4e720-57b8-4b73-807d-6f8f3c525750" />

## Assignació de rols i permisos
### En aquest punt, com ja hem fet els grups i hem posat les comptes a cada grup, llavors cada compta ja te els seus propis rols.

- **Administrador**: pot crear, editar, eliminar i compartir fitxers.  
- **Editor**: pot crear i modificar fitxers, però no eliminar carpetes compartides ni gestionar usuaris.  
- **Visualitzador**: només pot obrir i llegir fitxers, sense editar ni eliminar.  

### Demostració
- Des de la compta principal, crea una carpeta per fer la prova, seguidament comparteix la carpeta amb les 3 comptes que vam crear.
  
- Seguidament crea un arxiu on pots posar el que vulguis ja que és una prova.

<img width="855" height="364" alt="image" src="https://github.com/user-attachments/assets/72186c16-176f-4aa5-9cc1-31e598a335b6" />

#### Administrador
- Primerament la farem amb la compta Admin, on posarem "Custom permisions" i posem totes les opcions que posen a la part de "Custom permissions"

<img width="858" height="737" alt="image" src="https://github.com/user-attachments/assets/660a5896-c25e-488f-8b2d-6d3ca9cd33f8" />

- Seguidament veiem a la part de "Files", la carpeta que vam compartir i veuras que pots fer tot.

<img width="863" height="289" alt="image" src="https://github.com/user-attachments/assets/68b81948-f3c3-4356-835c-8ac2d89a2638" />

#### Visualitzador 
- Primerament la farem amb la compta visualitzador, on posarem "View Only"

<img width="857" height="442" alt="image" src="https://github.com/user-attachments/assets/86ad1baa-d99b-4ddf-9a9a-f323d74cda3f" />

- Seguidament iniciem sessió com *Visualitzador*
- Seguidament veiem a la part de "Files", la carpeta que vam compartir i veuras que només la pots veure
  
<img width="856" height="266" alt="image" src="https://github.com/user-attachments/assets/9a5654d3-798d-4e8b-88a5-37cb8c751ee0" />

#### Editor
- Primerament la farem amb la compta Editor, on posarem "Allow editing"

<img width="857" height="446" alt="image" src="https://github.com/user-attachments/assets/0bafb86b-e693-4cd2-acfe-b4899377a3b6" />

- Seguidament iniciem sessió com *Editor*, on es poden modificar documents però no eliminar-los si no són propis.  
- Seguidament veiem a la part de "Files", la carpeta que vam compartir i veuras que podem modificar documents però no eliminar-los si no són propis.

<img width="861" height="261" alt="image" src="https://github.com/user-attachments/assets/d5121b44-bab8-4322-a829-f91bb7c8ae03" />

# Administració d’arxius a Nextcloud

## Organització de carpetes i fitxers

### Objectiu
Crear una jerarquia lògica de carpetes per mantenir els documents ordenats.

### Crear l’estructura de carpetes
**Instruccions (en anglès):**
1. Log in to your Nextcloud account.  
2. Go to **Files**.  
3. Click **+ New folder**.  
4. Create the following folders:  
   - **Documents Personals**  
   - **Treball Compartit**  
   - **Recursos**  
5. Open **Treball Compartit** and create subfolders:  
   - **Equip A**  
   - **Equip B**
   
## Polítiques de seguretat

### Objectiu
Activar opcions de seguretat com la caducitat dels enllaços compartits i l’obligació de contrasenya.

### Activar polítiques de seguretat
**Instruccions (en anglès):**
1. Log in as **admin**.  
2. Go to **Settings → Administration → Sharing**.  
3. Enable:  
   - **"Enforce expiration date for public links"**  
   - **"Enforce password protection for public links"**  
   - Optional: **"Allow users to share via link"**


### 2.2 Crear un enllaç compartit amb restriccions
**Instruccions (en anglès):**
1. Go to **Files**.  
2. Select a folder and click **Share**.  
3. Enable **Share link**.  
4. Set:  
   - An expiration date  
   - A password  
5. Test the link in another browser.

---

## 3. Accés des de qualsevol màquina de la xarxa

### 3.1 Obtenir la IP de la màquina virtual
- A Linux VM: `ip a`
- A Windows VM: `ipconfig`
  
### 3.2 Accedir a Nextcloud des d’una altra màquina

**Instruccions (en anglès):**
1. Open a browser on another device connected to the same network.  
2. Enter: `http://<IP-de-la-MV>/nextcloud`
3. Inicia sesió amb les teves credencials

### 3.3 Permetre accés al firewall (si és necessari)

**Instruccions (en anglès):**
- `sudo ufw allow 80/tcp`
- `sudo ufw allow 443/tcp`
## 4. (Extra) Accés a clouds de companys

### Objectiu
Afegir comptes externs de Nextcloud i navegar-hi.

### Afegir comptes externs
**Instruccions (en anglès):**
1. Log in to your Nextcloud.  
2. Go to **Settings → Connected Accounts**.  
3. Click **Add Nextcloud account**.  
4. Enter the server URL, username and app password.  
5. Save.

### Navegar pels comptes externs
**Instruccions (en anglès):**
1. Go to **Files**.  
2. Look for the new external folder.  
3. Open it to browse shared files.
