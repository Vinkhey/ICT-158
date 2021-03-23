# Environnement
## Nom de domaine

Comme dans la capture ci-dessous de nom de domaine est "Scuolapro.local"

![alt text](images/Autres/DNS.png)

Le FQDN ou Fully Qualified Domain Controller est "ict158-srv03-1.scuolapro.local"

![alt text](images/Autres/FQDN.png)

## IP

L'adresse du server est 10.1.1.20 avec comme passerelle par défaut 10.1.1.1 et le serveur DNS pointe sur lui même.

![alt text](images/Autres/IPServer.png)

L'adresse du client est 10.1.1.41, on peut constater également que l'adresse IP a bien été attibué par le serveur DHCP est pas rentrer manuellement, la passerelle par défaut est 10.1.1.1 et le serveur DHCP et DNS pointe bien sur l'adresse du serveur windows 2003.

![alt text](images/Autres/IPClient.png)

## Réseau

L'adresse du réseau est 10.1.1.0, le masque de sous réseau est 255.255.255.0 ou /24

![alt text](images/Autres/IPServer.png)

La pool d'adresse IP sont entre 10.1.1.40 et 10.1.1.199

![alt text](images/DHCP/PoolAdresse.png)

Ici on peut voir que l'adresse du routeur est 10.1.1.1, l'adresse du DNS est 10.1.1.20 lui même et le nom de domaine est "ScuolaPro.local".

![alt text](images/DHCP/OptionEtendue.png)

Voici un état des lieux du réseau actuelle.

![alt text](images/Autres/Shema.png)

Il y a actuellement 6 imprimantes connectés au serveur puis à un routeur ainsi qu'une machine cliente également connectée au serveur.


## Déploiement auto *wim

Sur le bureau du windows server 2003 il y a un raccourci qui mène au déployement d'os qui est visiblement situé dans le fichier download du disque D:

![alt text](images/OSDeployement/OsDeployement.png)

Dans le dossier images il y a l'image windows 7 qu'utilise la machine cliente.

![alt text](images/OSDeployement/images.png)

En revenant sur le dossier on peut y trouver un fichier texte à lire

![alt text](images/OSDeployement/ALire.png)

Egalement un autre fichier texte qui semble contenir un code comme un script mais il est en fichier texte, il semble qu'il sert à créer deux partitions différentes.

![alt text](images/OSDeployement/Dispartrans.png)

Sinon il ne reste que deux script en .bat, "DeployImage", qui j'imagine sert à déployer l'image windows du client.

![alt text](images/OSDeployement/DeployImage.png)

et "ExtractImage" qui sert à enlever l'image de la machine

![alt text](images/OSDeployement/ExtractImage.png)

## Imprimantes

Il y a un total de 7 imprimantes connecté sur le même réseau, une pour chaque département.

![alt text](images/Autres/Imprimantes.png)

Les printers sont tous des HP LaserJet 4250 PCL 5e, pour l'instant seulement une seule imprimante est utilisée, la HP_IT.

Dans cette capture nous pouvons voir les quelles adresses IP correspond à quelle imprimante ainsi que le port utilisé TCP/IP.

![alt text](images/Autres/IPImprimante.png)

![alt text](images/Autres/IPImprimante2.png)

Toutes les imprimantes utilisent le même pilote, le "HP Laserjet 4350 PCL 5e".

![alt text](images/Autres/PiloteImprimante.png)

Il y a trois pilote d'impression différent d'installé sur le serveur d'impression, celui qu'utilisent les imprimantes ont la version 64 bits et 32 bits.

![alt text](images/Autres/PiloteServeurImpression.png)

# Serveurs
## Hardware

Checker la documentation dans ce repository, ce document repertorie tout le type d'hardware disponible pour ce type de serveur, difficile de dire les vrais composants du serveur puisqu'il d'agit d'une machine virtuel, les composants ne sont pas les mêmes :

https://github.com/Vinkhey/ICT-158/blob/main/Doc%20Machines/doc_HPServer.pdf

D'après la capture ci-dessous l'os installé est "Microsoft windows server 2003 Standard Edition", la version du système est "5.2.3790 Service Pack 2 version 3790"

![alt text](images/Autres/Hardware-2.png)

## Services
### DHCP

Comme indiqué plus haut dans le document, il y a une étendue "SculoaPro_DHCP" sur l'adresse 10.1.1.0, le serveur DHCP est le serveur lui-même en 10.1.1.20

![alt text](images/DHCP/DHCP.png)

La Pool d'adresse distribuable est entre les adresses 10.1.1.40 et 10.1.1.199

![alt text](images/DHCP/PoolAdresse.png)

On peut constater qu'une adresse IP à déjà été attribuée à la machine cliente avec pour adresse 10.1.1.40 est la fin du bail d'une durée de 8 jours.

![alt text](images/DHCP/BauxAdresse.png)

Aucune réservation d'adresse IP n'a été effectuée.

![alt text](images/DHCP/ReservationAdresse.png)

Ici on peut constater les options d'étendues, le routeur avec l'adresse 10.1.1.1 et le serveur DNS en 10.1.1.20 avec comme nom de domaine ScuolaPro.local

![alt text](images/DHCP/OptionEtendue.png)

Aucune option de serveur n'a été effectuée

![alt text](images/DHCP/OptionServeur.png)

### AD

Comme mentionné au début de ce document le nom de domaine est "ScuolaPro.local" et le FQDN est "ict158-srv03-1.scuolapro.local", le controleur de domaine est "ScuolaPro.local", il n'y a pas de sous-domaine.

Le niveau fonctionnel est windows 2000 mixte et le niveau de la foret est windows 2000.

![alt text](images/Autres/foret.png)

Ici on peut retrouver les groupes utilisateurs créer par défaut par l'os.

![alt text](images/AD/Builtin.png)

Ici on retrouve les machines du réseau.

![alt text](images/AD/Computers.png)

Ici on retrouve le controlleur de domaine qui est le serveur lui-même.

![alt text](images/AD/DomainController.png)

Aucun principe de sécurité étrangère

![alt text](images/AD/ForeignSecurityPrincipals.png)

### Unité d'organisation

Dans l'unité d'organisation "ScuolaPro-Ste-Croix", on peut retrouver un groupe pour chaque département contenant les utilisateurs concernés.

Dans Back-office, le groupe Back-Office et L'utilisatrice Mélanie-Alonso, le groupe Back-Office ne possède actuellement aucun membre et Mélanie ne fait partit d'aucun autre groupe

![alt text](images/AD/DepartementAD/Back-Office.png)

Dans Comptabilité, le groupe Comptabilite et L'utilisatrice Dana Schipper, le groupe Comptabilite ne possède actuellement aucun membre et Dana ne fait partit d'aucun autre groupe

![alt text](images/AD/DepartementAD/Comptabilite.png)

Dans Direction, le groupe Direction et L'utilisateur Marc Mueller, le groupe Direction ne possède actuellement aucun membre et Marc ne fait partit d'aucun autre groupe

![alt text](images/AD/DepartementAD/Direction.png)

Dans IT, le groupe IT et L'utilisateur Tim Brown, il fait bien partit du groupe IT et aucun d'autre.
![alt text](images/AD/DepartementAD/IT.png)

Dans Logistique, le groupe Logistique et L'utilisateur Jean-Michel Blaser, il fait bien partit du groupe Logistique et aucun autre.

![alt text](images/AD/DepartementAD/Logistique.png)

Dans marketing, le groupe Marketing et L'utilisateur André Dupré, le groupe Marketing ne possède actuellement aucun membre et André ne fait partit d'aucun autre groupe

![alt text](images/AD/DepartementAD/Marketing.png)

Dans Production, le groupe Production et L'utilisateur Juerg Haefeli, le groupe Comptabilite ne possède actuellement aucun membre et Dana ne fait partit d'aucun autre groupes.

![alt text](images/AD/DepartementAD/Production.png)

Ici on peut retrouver les différents autres groupes.

![alt text](images/AD/Users.png)

### DNS

Les options du serveurs DNS :

![alt text](images/DNS/DNS.png)

Dans la zone de recherche directe, le domaine ScuolaPro.local

![alt text](images/DNS/ZoneDirecte.png)

Aucune zone de recherche inversée

![alt text](images/DNS/ZoneInverse.png)

Ici on peut notamment retrouver le FQDN du domaine, il y a également un alias CNAME "5e514734-7b39-4d21-aff5-270ee42d3261._msdcs.Scuolapro.local"

![alt text](images/DNS/Msdcs.png)

Ici on peut retrouver tout les hotes du domaine.

![alt text](images/DNS/ScuolaPro.png)

### File Server

Les partages local, il y un total de 12 partages différents, un partage caché pour le disque C avec droits de lecture et exécution pour tout les utilisateurs, tout les partages ont tout les droits pour le groupe administrateurs.

Un partage caché pour le disque D: sans droits particuliers.  

Un partage sur le dossier Downloads, les créateurs de fichiers et dossiers n'ont aucun droits.

Un partage sur le dossier Echange, les créateurs de fichiers et dossiers n'ont aucun droits.

Un partage caché IPC aucune idée de quoi il s'agit.

Un partage NETLOGON, avec comme droits de lecture et exécution pour le groupe utilisateurs authentifiés et opérateurs de serveurs, aucun droits pour les créateur propriétaire.

Un partage caché pour le dossier print qui contient les spools d'impression, createur propriétaire aucun droit, opérateur de serveur Modification, opérateur d'impression tout les droits, tout le monde droits de lecture et exécution et utilisateurs authentifiés également droit de lecture et exécution.

Un partage caché profil, créateur propriétaire aucun droit, utilisateur du domaine droit de modification.

Un partage Services, créateur propriétaire aucun droits.

Un partage SYSVOL, créatuer propriétaire aucun droit, opérateur de serveur et utilisateurs authentifiés droits de lecture et exécution.

Un partage caché utilisateur, créateur propriétaire aucun droits.

![alt text](images/FileServer/PartageLocal.png)

Aucune Session locale :

![alt text](images/FileServer/SessionLocal.png)

aucun fichiers d'ouverts :

![alt text](images/FileServer/FichierOuvertLocal.png)

Pour défragmenter les disques :

![alt text](images/FileServer/DefragmenterDisque.png)

Les options de partitions de disques :

![alt text](images/FileServer/GestionDisques.png)

## Raid5

Le raid 5 est partagée en plusieurs partitions nommée Data avec comme lettre d: entre les disques 1 à 3 avec une capacité totale de 80 Go ainsi que de type NTFS et le disque c: de 40Go également de type NTFS.

![alt text](images/FileServer/GestionDisques.png)

Le disque D: possède 74.1 Go de disponible mais seulement 5.87 Go sont utilisés pour un total de 80 Go de base.

![alt text](images/Autres/EspaceDisponible.png)

Le dossier Download contient un dossier image qui contient l'image du client windows 7.

Le dossier Echange contient un dossier Images et Vidéos qui sont vide les deux.

Le dossier Profils contient uniquement le dossier de Tim Brown, qui contient lui même un dossier Administration vide et un dossier Perso également vide.

![alt text](images/Autres/FichierTimBrown.png)

Le dossier Services contient tout les services de l'entreprise, seul le dossier IT contient un dossier Administration vide.

Le dossier Utilisateur contient tout les dossiers des utilisateurs de l'entreprise, seul le dossier de Tim Brown contient comme mentionné auparavant un dossier administration et Perso qui sont les deux vides.

![alt text](images/Autres/fichiers.png)

Le disque C: qui possède 35.8 Go de libre et 4.15 Go d'utilisés pour un total de 40Go de base.

![alt text](images/Autres/EspaceDisponibleC.png)

Il contient tout les fichiers systèmes destinés au focntionnement du serveur.

Il y a également un lecteur disquette(A:) ainsi qu'un lecteur de disque DVD (E:).

# Client
## Hardware :

- 35 machines clientes de type [Dell Latitude E6510](https://i.dell.com/sites/csdocuments/Shared-Content_data-Sheets_Documents/en/latitude-e6410-e6510-specsheet.pdf) cliquez sur le nom pour afficher la documentation Dell. Le Dell latitude E6510 est incompatible avec Windows 10.

- 10 machines clientes de type [Dell Latitude E6530](https://www.notebooksforstudents.org/Descriptions/dell-e6530.pdf) cliquez sur le nom pour afficher la documentation Dell. Le Dell latitude E6530 est compatible avec Windows 10.

- 5 machines clientes de type [Dell Optiplex 990](https://www.dell.com/downloads/global/products/optix/en/optiplex-990-tech-guide.pdf) cliquez sur le nom pour afficher la documentation Dell. Le Dell Optiplex 990 n'est pas compatible avec Windows 10. `Car Dell n'a pas mis à disposition des pilotes qui supportent Windows 10 sur ces PC.`

## OS de la machine client :

Windows 7 Entreprise 64 bits `Service Pack 1`

## Réseau :

Nom de l'hôte : ICT158-CLI7-1

Suffixe DNS Principal : Scuolapro.local

Adresse physique :  00-0C-29-D6-17-2F

Adresse IPv4 : 10.1.1.41

Masque de sous-réseau : 255.255.255.0

Passerelle par défaut : 10.1.1.1

Serveur DHCP : 10.1.1.20

Serveur DNS : 10.1.1.20

## Logiciels :

### Office :

![](P:\4ème\ICT-158\Office.PNG)

`Version Office : 11.5604.5606`

`Office 2003 est compatible avec Windows 10.`

### Antivirus :

Nom : Avira Antivirus

Version du produit : 15.0.20.59 -> Date : 25.08.2016

License : `Version gratuite`

### Bureau à distance :

 ![](P:\4ème\ICT-158\Bureau à distance.PNG)

### Adobe reader :

![](P:\4ème\ICT-158\Adobe.PNG)

`FireFox :`

`Version : 49.0.1`

`XMind :`

`Version : 7.5 Update 1 (R3.6.51.201607142338)`

`License : Pas de license`

`UltraVNC :`

`Version : 1.2.1.1`

## Script Logon

Il y a un script différent pour chaque utlisateur selon son affiliation aux départements, pour l'instant le seul profil de créer et celui de Tim Brown, aucun autre profil ne figure dans le dossier Profils.

Le chemin où sont stocker tout les scripts :

![alt text](images/Autres/ScriptLogonChemin.png)

Le contenu du script Back, servant à créer la session pour l'utilsatrice Melanie Alonso comme il s'agit de l'unique membre du Back Office. On peut voir que le script mappe un lecteur E: avec le contenu du dossier Back-Offfice et le script ajoute également l'imprimante HP_Back, chaque script fait les mêmes actions mais en changeant à chaque fois d'utilisateurs et d'imprimantes en fonction des affilations.

![alt text](images/Autres/ScriptBack.png)


## Profils itinérants

Dans cette capture ont peut voir le chemin du profil de l'utilisateur, ils ont tous le même chemin mais en changeant juste le chemin selon leur prénom et nom, comme mentionné auparavant seul le profil de Tim Brown a été créé, il contient aucun octet de données.

![alt text](images/Autres/ScriptLogon.png)

## Dossier personnel

Chaque dossier perso des utilisateurs est monté sur un lecteur U:, changeant également nom en fonction de leur prénom et nom, seul le dossier de Tim Brown contient des dossiers, les dossiers Administration et Perso qui sont les deux vides, tout les dossiers possèdent 0 octets de données.

![alt text](images/Autres/DossierBase.png)
