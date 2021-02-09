# Environnement
## Nom de domaine
Comme dans la capture ci-dessous de nom de domaine est "Scuolapro.local"

![alt text](/images/Autres/DNS.png)

Le FQDN ou Fully Qualified Domain Controller est "ict158-srv03-1.scuolapro.local"

![alt text](/images/Autres/FQDN.png)
## IP

L'adresse du server est 10.1.1.20 avec comme passerelle par défaut 10.1.1.1 et le serveur DNS pointe sur lui même.

![alt text](/images/Autres/IPServer.png)

L'adresse du client est 10.1.1.41, on peut constater également que l'adresse IP a bien été attibué par le serveur DHCP est pas rentrer manuellement, la passerelle par défaut est 10.1.1.1 et le serveur DHCP et DNS pointe bien sur l'adresse du serveur windows 2003.

![alt text](/images/Autres/IPClient.png)

Chose bizarre lorqu'on regarde les adresses réservé, la machine cliente windows 7 semble avoir deux adresses IP qui lui ont été attribué et active au même moment, mais si on tente de pinger la machine 10.1.1.40 sur le serveur et le client elle ne répond pas mais la 10.1.1.41 fonctionne.

![alt text](/images/Autres/AdresseDonne.png)

Le serveur ne semble pas pouvoir pinger la machine 10.1.1.41, mais le client lui arrive à le pinger, il semble y avoir un problème avec le pare-feu.

## Réseau

Dans la capture ci-dessous nous pouvons voir que l'adresse du réseau est 10.1.1.0

![alt text](/images/DHCP/DHCP.png)

le masque de sous réseau est 255.255.255.0 ou /24

![alt text](/images/Autres/IPServer.png)

La pool d'adresse IP sont entre 10.1.1.40 et 10.1.1.199

![alt text](/images/DHCP/PoolAdresse.png)

Ici on peut voir que l'adresse du routeur est 10.1.1.1, l'adresse du DNS est 10.1.1.20 lui même et le nom de domaine est ScuolaPro.local.

![alt text](/images/DHCP/OptionEtendue.png)

## Déploiement auto *wim

Sur le bureau du windows server 2003 il y a un raccourci qui mène au déployement d'os qui est visiblement situé dans le fichier download du disque D:

![alt text](/images/OSDeployement/OsDeployement.png)

Dans le dossier images il y a l'image windows 7 qu'utilise la machine cliente.

![alt text](/images/OSDeployement/Images.png)

## Imprimantes
Il y a un total de 7 imprimantes connecté sur le même réseau :

![alt text](/images/Autres/Imprimantes.png)
# Serveurs
## Hardware
Checker la documentation dans ce repository :

https://github.com/Vinkhey/ICT-158/blob/main/doc_HPServer.pdf

Dans ce document on peut retrouver le supposé hardware si la machine était réel, mais comme elle ne l'ai pas, son hadware est réellement :

![alt text](/images/Autres/Hardware.png)

Elle prend ces ressources de la machine utilisé hôte.
## OS
Capture d'écran de l'os installé sur le serveur :

![alt text](/images/Autres/OSVersion.png)

Nous pouvons donc constater que l'os installé est "Microsoft Windows Server 2003" la version standard.
## Services
### DHCP
![alt text](/images/DHCP/DHCP.png)

![alt text](/images/DHCP/PoolAdresse.png)

![alt text](/images/DHCP/BauxAdresse.png)

![alt text](/images/DHCP/ReservationAdresse.png)

![alt text](/images/DHCP/OptionEtendue.png)

![alt text](/images/DHCP/OptionServeur.png)
### AD
![alt text](/images/AD/AD.png)

![alt text](/images/AD/Builtin.png)

![alt text](/images/AD/Computers.png)

![alt text](/images/AD/DomainController.png)

![alt text](/images/AD/ForeignSecurityPrincipals.png)

### Unité d'organisation

![alt text](/images/AD/GroupeAD/Back-Office.png)

![alt text](/images/AD/GroupeAD/Comptabilite.png)

![alt text](/images/AD/GroupeAD/Direction.png)

![alt text](/images/AD/GroupeAD/IT.png)

![alt text](/images/AD/GroupeAD/Logistique.png)

![alt text](/images/AD/GroupeAD/Marketing.png)

![alt text](/images/AD/GroupeAD/Production.png)

![alt text](/images/AD/Users.png)
### DNS
![alt text](/images/DNS/DNS.png)

![alt text](/images/DNS/ZoneDirecte.png)

![alt text](/images/DNS/ZoneInverse.png)

![alt text](/images/DNS/Msdcs.png)

![alt text](/images/DNS/ScuolaPro.png)

### File Server
![alt text](/images/FileServer/PartageLocal.png)

![alt text](/images/FileServer/SessionLocal.png)

![alt text](/images/FileServer/FichierOuvertLocal.png)

![alt text](/images/FileServer/DefragmenterDisque.png)

![alt text](/images/FileServer/GestionDisques.png)
## Raid5

![alt text](/images/FileServer/GestionDisques.png)
