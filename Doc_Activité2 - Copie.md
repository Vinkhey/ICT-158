# Pratique

# Changement du Hardware

Selon Microsoft le système minimale pour installer Windows server 2019 est :

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

### Minimum:

    Carte réseau Ethernet capable d’au moins un débit en gigabits
    Conforme à la spécification de l’architecture PCI Express.

Une carte réseau qui prend en charge le débogage réseau (KDNet) est utile, mais ne constitue pas une condition minimale requise.

Une carte réseau qui prend en charge l’environnement PXE (Pre-boot Execution Environment) est utile, mais ne constitue pas une condition minimale requise.

## Choix du matériel

[HPE ProLiant MicroServer Gen10 Plus](https://buy.hpe.com/ch/fr/servers/proliant-microserver/proliant-microserver/proliant-microserver/hpe-proliant-microserver-gen10-plus/p/1012241014)

Processeur : Intel Xeon E-2224
Vitesse : 3.40GHz
RAM : 16Go
Type : DDR4
Vitesse de RAM : 2666 MHz
Capacité de stokage : 4 x 1Tb 

Prix : 820.-

## Justification financière

Ce serveur est puissant, petit et est très peu couteux. Il est parfait pour une petite entreprise tel scuaolapro. Nous avons choisi celui-ci, car il remplit les critères pour l'entreprise. Il possède 4 emplacements de disque. Donc suivant les besoins du client, il peut rajouter des disques en cas de besoin. Dans notre cas, nous avons pris 4 disques dur de 1Tb. Ce qui peut faire beaucoup pour l'utilité qu'il en aurait. Si le client désire moi de disque, et du coup, ne plus utiliser le raid 5 le prix du serveur baisserait. 

# Migration des données

Avant de commencer une migration de données, il faut savoir ce que le client vaudrait migrer et est-ce que toutes les données sont migrables ou non. Ensuite, on doit bien s'assurer qu'il  y a une sauvegarde de tous les fichiers à migrer. Comme ça, s'il y a un problème, il nous reste un backup. 

## Méthode 1

La première méthode consisterai à migrer le server de 2003 à 2008 puis 2012, 2016 et enfin 2019 en utilisant l'outil de micorsoft "Storage Migration Service"

![alt text](C:\Git\ICT-158\images\Autres\upgrade-paths.png)

Il est apparament impossible de transférer directement les données d'un server 2003 à 2019, en suivant le shéma ci-desssus, nous devrions d'abord upgrade de 2003 à 2008 puis 2012, 2016 et enfin seulement nous pourrons atteindre la version 2019.

Cette outil peut migrer le file server d'un serveur à un autre, donc toutes les datas du serveur et les partages, il ne permet pas de migrer le reste des services ni les logiciels installés. Par contre il permet de transférer les groupes et utilisateurs ainsi que les droits ntfs et de partage, il ne peut migrer les controlleur de domaine.



La première méthode consisterai à prendre un logiciel de migrations des données.

## Méthode 2

La deuxième méthode consisterai à transférer les données manuellement par clé usb et recréer les partages sur le nouveau serveur. Par contre, nous perdrons les droits et devrons les recrées également.

## Méthode 3

Nous pourrions utiliser la commande powershell robocopy qui permet de copier les files entre les deux serveurs ainsi que les droits ntfs, par contre il faudra recréer les partages manuellement mais au moins les droits seront conservés. Il faut également transférer les options de partage car sinon les partages ne seront pas vu par le serveur.

## Justification de la méthode choisie

La méthode 3 semble être non seulement la plus rapide mais également la plus facile des méthodes car elle ne prend pas en compte l'upgrade des serveurs fastidieuse et permet de limiter la perte de temps de la méthode 2.

# Migration des Services

## Méthode 1

La première méthode consisterai à migrer l'AD sur Windows Server 2012 en premier lieu. Car il est impossible de le faire directement de Windows Server 2003 à 2019.  Ensuite, il faudrait faire la migration de 2012 à 2019.  Car sous Windows 2000 server et 2003, la réplication de SYSVOL ce faisait à l'aide FRS (NTFRS) alors que depuis Windows Server 2012 il se fait avec DFSR. D'où le besoin de faire une première migrations de 2003 à 2012 et ensuite de faire celle de 2012 à 2019. <br/>

Tout d'abord, il faut voir l'état de son active directory à l'aide de la commande suivante: 

**<u>dcdiag /e /test:sysvolcheck /test:advertising</u> #permet faire un check de sysvol et du domaine controller**

**<u>dfsrmig /setglobalstate 1</u>  #La migration va passé en mode préparation et va faire une copie de SYSVOL avec le nom SYSVOL_DFSR**

**<u>dfsrmig /getmigrationstate</u> #Permet de voir l'avancement de la commande que l'on vient de faire. Jusqu'a ce que ça nous mette le fait qu'on a réussi.**

**<u>dfsrmig /setglobalstate 2</u> #La copie SYSVOL_DFSR sera montée sur le partage SYSVOL à la place de l'ancienne. Il faut patienter un certain temps.** 

**<u>dfsrmig /getmigrationstate</u> #Comme pour la précendente opération, il faut faire cette commande pour voir l'avancement.** 

**<u>dfsrmig /setglobalstate 3</u> #Cette commande va retirer complètement FRS et son SYSVOL pour passer entièrement à DFSR. Il faudra patienter encore un certain temps le temps que FRS soit retiré sur le DC (ou les DC) et que DFSR soit fonctionnel. Il faut refaire la commande "dfsrmig /getmigrationstate" pour voir l'avancement de temps en temps.** 

S'il y a des soucis avec l'antivirus. Il faut penser à changer le chemin d'exclusion SYSVOL en SYSVOL_DFSR. <br/>

Après cette étape on pourrait faire la migration entre Windows Server 2012 et Windows Server 2019.

Pour désactiver l'AD de l'ancien serveur, il faut faire un DCpromo, ensuite une boîte de dialogue s'ouvre et il va proposé de supprimer l'AD ce contrôleur de domaine. 

Ensuite nous pourrions recréer le serveur DNS à partir de cela. Il serait recréé automatiquement grâce au données de l'AD. 

### Pour le DHCP :

Il faut migrer le rôle DHCP afin de pouvoir retirer (physiquement) notre Windows Server 2003.

- Sur le Windows Server 2003, changer son IP.
- Sur le Windows Server 2016, installez le rôle DHCP.
- Sur le Windows Server 2016, changer son IP pour q’elle soit celle de l’ancien DHCP

Sur le Windows Server 2003, sauvegardez le DHCP avec la commande netsh.

On peut sauvegarder toutes les étendues (s'il y en a plusieurs) :

**netsh dhcp server export c:\ScuolaPro_DHCP.dat all**

ou seulement une :

**netsh dhcp server export c:\ScuolaPro_DHCP.dat 10.1.1.0**

Sur le Windows Server 2016, il faut récupérer le fichier ScuolaPro_DHCP.dat et il faut limporter avec la commande

 **netsh dhcp server import c:\ScuolaPro_DHCP.dat 10.1.1.0**

Si la commande ne fonctionne pas, il faudra recommencer l’exportation en procédant étendues par étendues et les importer unes à unes.

Stoppez le service DHCP Serveur puis démarrez le à nouveau.

###  Pour le serveur d'impression : 

à faire...



## Méthode 2

La méthode 2 consisterait à partir de zéro et recommencer tout le travail. Donc, ce serait le faite de d'utiliser notre nouveau serveur et avoir, cette fois-ci, Windows Server 2019. Il faudrait refaire un serveur DHCP le reconfigurer comme il est sur le server 2003. Donc, configurer l'adresse IP du server en 10.1.1.20 et l'étendu serait : 10.1.1.40 à 10.1.1.199. Ensuite, créer l'AD avec une nouvelle forêt 2019 et pas une forêt de 2000 comme l'ancienne. Avoir le même nom de domaine  que l'ancien server. Ensuite il faudra le promouvoir en contrôleur de domaine. 

## Justification de la méthode choisie

La première méthode semble être la plus complète et la plus pertinente, car elle permet de faire de faire une migration sans avoir trop de perte. Mais elle est complexe dans la compréhension. Donc il faudra faire des testes avant de se lancer dans la réalisation. Car sinon, cela risque de prendre beaucoup temps. Et le coup de travail sera élevé pour le client. 