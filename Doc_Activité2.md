# Pratique
# Changement du Hardware

Selon Microsoft le système minimale pour installer Windows server 2019 est :

## Processeur

Selon microsoft le système minimale pour installer Windows server 2019 est :
## Processeur
### Minimum:

    Processeur 1,4 GHz 64 bits
    Compatible avec le jeu d’instructions x64
    Prend en charge NX et DEP
    Prend en charge CMPXCHG16b, LAHF/SAHF et PrefetchW
    Prend en charge la traduction d’adresse de second niveau (EPT ou NPT)

## RAM
### Minimum:

    512 Mo (2 Go pour l’option d’installation Serveur avec Expérience utilisateur)
    Type ECC (Error Correcting Code) ou technologie similaire pour les déploiements d’hôtes physiques

## Contrôleur de stockage et espace disque requis

Les ordinateurs qui exécutent Windows Server 2019 doivent inclure un adaptateur du stockage conforme à la spécification de l’architecture PCI Express. Les dispositifs de stockage persistant sur les serveurs classés en tant que lecteurs de disque dur ne doivent pas être PATA. Windows Server 2019 n’autorise pas ATA/PATA/IDE/EIDE pour les lecteurs de données, de démarrage ou de page.

L’espace disque requis **minimal** approximatif pour la partition système est le suivant.

**Minimum** : 32 Go

## Conditions requises pour les cartes réseau

Minimum : 32 Go
Conditions requises pour les cartes réseau
Minimum:

    Carte réseau Ethernet capable d’au moins un débit en gigabits
    Conforme à la spécification de l’architecture PCI Express.

Une carte réseau qui prend en charge le débogage réseau (KDNet) est utile, mais ne constitue pas une condition minimale requise.

Une carte réseau qui prend en charge l’environnement PXE (Pre-boot Execution Environment) est utile, mais ne constitue pas une condition minimale requise.

## Choix du matériel et justification

HPE ProLiant MicroServer Gen10 Plus

[HPE ProLiant MicroServer Gen10 Plus](https://buy.hpe.com/ch/fr/servers/proliant-microserver/proliant-microserver/proliant-microserver/hpe-proliant-microserver-gen10-plus/p/1012241014)

Processeur : Intel Xeon E-2224
Vitesse : 3.40GHz
RAM : 16Go
Type : DDR4
Vitesse de RAM : 2666 MHz
Capacité de stokage : 4 x 1Tb

Prix : 820.-

Ce serveur est puissant, compact et a un faible coût. Il est parfait pour les petites entreprises. Nous avons choisi celui-ci, car il remplit les critères pour l'entreprise.

Ce serveur est puissant, petit et a un faible coût. Il est parfait pour les petites entreprises. Nous avons choisi celui-ci, car il remplit les critères pour l'entreprise. Étant donné qu'il possède 4 disques dur, il n'y aura pas de soucis avec le RAID 5.



# Migration des données
## Méthode 1

La première méthode consisterai à migrer le server de 2003 à 2008 puis 2012, 2016 et enfin 2019 en utilisant l'outil de microsoft "Storage Migration Service".

![alt text](images/Autres/upgrade-paths.png)

Il est apparament impossible de transférer directement les données d'un server 2003 à 2019, en suivant le shéma ci-desssus, nous devrions d'abord upgrade de 2003 à 2008 puis 2012, 2016 et enfin seulement nous pourrons atteindre la version 2019.

Cette outil peut migrer le file server d'un serveur à un autre, donc toutes les datas du serveur et les partages, il ne permet pas de migrer le reste des services ni les logiciels installés. Par contre il permet de transférer les groupes et utilisateurs ainsi que les droits ntfs et de partage, il ne peut migrer les controlleur de domaine.

## Méthode 2

La deuxième méthode consisterai à transférer les données manuellement par clé usb et recréer les partages sur le nouveau serveur. par contre nous perdrons les droits et devrons les recrées également.

## Méthode 3

Nous pourrions utiliser la commande powershell robocopy qui permet de copier les files entre les deux serveurs ainsi que les droits ntfs, par contre il faudra recréer les partages manuellement mais au moins les droits seront conservés. Il faut également transférer les options de partage car sinon les partages ne seront pas vu par le serveur.

## Justification de la méthode choisie

La méthode 3 semble être non seulement la plus rapide mais également la plus facile des méthodes car elle ne prend pas en compte l'upgrade des serveurs fastidieuse et permet de limiter la perte de temps de la méthode 2.

# Migration des Services

## Méthode 1

La première méthode consisterai à migrer l'AD sur Windows Server 2012 en premier lieu. Car il est impossible de le faire directement de Windows Server 2003 à 2019.  Ensuite, il faudrait faire la migration de 2012 à 2019.  Car sous Windows 2000 server et 2003, la réplication de SYSVOL ce faisait à l'aide FRS (NTFRS) alors que depuis Windows Server 2012 il se fait avec DFSR. D'où le besoin de faire une première migrations de 2003 à 2012 et ensuite de faire celle de 2012 à 2019. <br/>

Tout d'abord, il faut voir l'état de son active directory à l'aide de la commande suivante: 

```cmd
dcdiag /e /test:sysvolcheck /test:advertising #permet faire un check de sysvol et du domaine controller
```

```cmd
dfsrmig /setglobalstate 1  #La migration va passé en mode préparation et va faire une copie de SYSVOL avec le nom SYSVOL_DFSR
```

```cmd
dfsrmig /getmigrationstate #Permet de voir l'avancement de la commande que l'on vient de faire. Jusqu'a ce que ça nous mette le fait qu'on a réussi.
```

```cmd
dfsrmig /setglobalstate 2 #La copie SYSVOL_DFSR sera montée sur le partage SYSVOL à la place de l'ancienne. Il faut patienter un certain temps. 
```

```cmd
dfsrmig /getmigrationstate #Comme pour la précendente opération, il faut faire cette commande pour voir l'avancement. 
```

```cmd
dfsrmig /setglobalstate 3 #Cette commande va retirer complètement FRS et son SYSVOL pour passer entièrement à DFSR. Il faudra patienter encore un certain temps le temps que FRS soit retiré sur le DC (ou les DC) et que DFSR soit fonctionnel. Il faut refaire la commande "dfsrmig /getmigrationstate" pour voir l'avancement de temps en temps. 
```

S'il y a des soucis avec l'antivirus. Il faut penser à changer le chemin d'exclusion SYSVOL en SYSVOL_DFSR. <br/>

Après cette étape on pourrait faire la migration entre Windows Server 2012 et Windows Server 2019.  

Pour le DHCP, il faut exécuter la commande suivante sur PowerShell: <br/>

```powershell
Export-DhcpServer -ComputerName "FQDN Serveur DHCP" -File 
"C:\Temp\dhcp172163.xml" -ScopeId 10.1.1.0 #cette commande va créer un fichier .xml qui pourra être utiliser sur le nouveau serveur. Le répertoire Temp dans être créer avant de faire la commande. 
```

 

## Méthode 2

La méthode 2 consisterait à partir de zéro et recommencer tout le travail. C'est-à-dire, recréer l'AD, le DNS et le DHCP, les groupes, les utilisateurs, etc... Ce qui pourrait poser pas mal de problèmes pour les utilisateurs. Car leur PCs ne recevrait pas d'adresse IP et il ne ferai pas parti du domaine. 

## Justification de la méthode choisie

Bien que la méthode 2 semble être plus rapide, nous prendrons la première méthode car elle permet d'enlever les erreurs humaines que nous pourrions faire en recréant manuellement les services. Et la première méthode semble être plus complète et pertinente que la deuxième.

# Pratique

En premier lieu il faut faire rejoindre le même network au deux serveurs 2003 et 2019, puis rajouter le serveur 2019 au domaine.

## Migration des données

Il faut commencer par ajouter le protocole smb1 car sinon on ne peut accéder aux partages depuis le serveur, vérifier que les files sont accessibles depuis le serveur 2019 et ensuite on peut commencer à exporter vers ce serveur.
