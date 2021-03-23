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

Ce serveur est puissant, petit et a un faible coût. Il est parfait pour les petites entreprises. Nous avons choisi celui-ci, car il remplit les critères pour l'entreprise. Étant donné qu'il possède 4 disques dur, il n'y aura pas de soucis avec le RAID 5. 



# Migration des données
## Méthode 1

La première méthode consisterai à migrer le server de 2003 à 2008 puis 2012, 2016 et enfin 2019 en utilisant l'outil de micorsoft "Storage Migration Service"

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
## Méthode 2
## Justification de la méthode choisie
## description
