# Manual d'instal·lació d’ownCloud amb virtualització mitjançant IsardVDI

# Demostració del funcionament

## Pujar un Arxiu
#### Primerament hem d'anar a la part de "Arxius" de NextCloud, que en anglés seria "Files"

![hola](Imagenes/imagen1.png)

#### Seguidament li donem al boto on diu "Nou" o en anglés que seria "New"

![hola](Imagenes/imagen3.png)

#### Després fem click a "Penjar Fitxer" o "Upload Files"

![hola](Imagenes/imagen2.png)

## Crear una carpeta
#### Al mateix apartat  on pujem un fitxer, li donem a "New Folder" o "Nova Carpeta"

![hola](Imagenes/imagen4.png)

## Compartició de continguts
Per poder compartir els continguts hen de trobar l'icone blau de compartir que seria el de la imatge seguent:

![hola](Imagenes/imagen5.png)

Quan li donem a aquest botó, ens sortira dues maneres de compartir el contingut:
- "internal Shares": Seria per compartir amb persones que ja tinguin acces a aqust contingut.
- "External Shares": Seria per donar acces al contingut, ja sigui amb email o per un link.

![hola](Imagenes/imagen6.png)

## Creació d'usuaris
#### Per começar a crear altres usuaris, hem de donar-li al nostre perfil

![hola](Imagenes/imagen7.png)

#### Seguidament hen de fer click en "Accounts" o "Comptes"

![hola](Imagenes/imagen8.png)

## Configuració d’usuaris
1. Accedeix a la interfície d’administració amb el compte principal.  
2. Ves a **Configuració → Administració → Usuaris**.  
3. Crea tres usuaris:  
   - **Administrador** → assignat al grup *admin*.  
   - **Editor** → assignat al grup *Editors*.  
   - **Visualitzador** → assignat al grup *Visualitzadors*.  


## Assignació de rols i permisos
- **Administrador**: pot crear, editar, eliminar i compartir fitxers.  
- **Editor**: pot crear i modificar fitxers, però no eliminar carpetes compartides ni gestionar usuaris.  
- **Visualitzador**: només pot obrir i llegir fitxers, sense editar ni eliminar.  

### Demostració
- Iniciant sessió com *Visualitzador*, no apareixen opcions d’edició.  
- Iniciant sessió com *Editor*, es poden modificar documents però no eliminar-los si no són propis.  



## Administració d’arxius
### Jerarquia de carpetes
- `Documents_Personals` → privats per cada usuari.  
- `Treballs_Compartits` → Editors i Administradors.  
- `Recursos` → tots els usuaris, inclosos Visualitzadors.  

### Polítiques de seguretat
- Caducitat d’enllaços compartits (ex. 7 dies).  
- Contrasenya obligatòria per a enllaços externs.  
- Bloqueig de descàrregues per a Visualitzadors.  



## Accés des d’una màquina de la xarxa
1. Configura la màquina virtual amb una IP fixa.  
2. Des d’un altre dispositiu de la mateixa xarxa, accedeix via navegador:  

```bash
http://IP_de_la_VM/nextcloud


