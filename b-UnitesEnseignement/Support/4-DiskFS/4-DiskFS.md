---
marp: true
theme: default
paginate: true
footer: "ETML - Module 187 - Disques et systèmes de fichiers"
---

<!-- header: "Module 187 - Disques et systèmes de fichiers" -->
# 4 - Disques et système de fichiers

ID du module 187 : OO7

Ce chapitre traite des systèmes de fichiers et des gestionnaires de disques.

---

## Systèmes de fichiers : Disques durs

- **HDD** (Hard Disk Drive) : mécanique, 3,5" ou 2,5", bon marché, éviter de déplacer en fonctionnement
- **SSD** (Solid State Drive) : électronique, 2,5", plus cher, meilleure résistance, plus rapide, écritures limitées, faible consommation, pas de bruit

Le connecteur le plus répandu : SATA. Pour SSD interne : aussi M.2.

On privilégie un SSD pour l'OS et les applications, un HDD pour les données.

Tous les supports (disques internes/externes, clés USB, cartes SD, DVD/BlueRay) sont des mémoires de masse.

---

## Fragmentation

- HDD : défragmentation parfois nécessaire pour regrouper les morceaux de fichiers
- SSD : jamais défragmenter (nombre d'écritures limité)
- Certains systèmes de fichiers sont plus sensibles à la fragmentation (FAT, NTFS)

[Wiki-disque dur](https://fr.wikipedia.org/wiki/Disque_dur)

---

## Système de partitionnement

Une partition d'un disque dur est l'attribution d'une partie de l'espace pour en faire un disque virtuel. Il peut y avoir plusieurs partitions sur un disque physique.

La première partition pour le démarrage s'appelle **partition d'amorçage** (boot partition).

---

## MBR/BIOS

Le MBR (zone d'amorçage) est le premier secteur adressable du disque dur.
- Taille : 512 octets
- Contient les données de partitionnement et de démarrage
- Maximum 4 partitions principales ou 3 principales + 1 étendue
- Capacité jusqu'à 2,2To

---

![height:500px](./img/Capt-PART-BIOS.PNG)

---

## GPT/UEFI

Le GPT contient les informations pour les partitions du disque.
- Taille : 16384 octets
- Jusqu'à 128 partitions, chacune avec un identifiant unique (GUID)
- Plus de notion de principales/étendues/logiques
- Taille max d'une partition : 256To
- Capacité jusqu'à 9,4Zo
- Informations de partitionnement et démarrage stockées plusieurs fois + CRC
- Robustesse et intégrité des données

---

![height:500px](./img/Capt-GPT-STRUC.PNG)

---

## Exemple de partition GPT sous Windows

![height:500px](./img/Capt-PART-UEFI.PNG)

---

## Gestion des partitions

- Windows : gestionnaire de disque
- Linux : GParted (ou fdisk en console)

Avantages du partitionnement :
- Plusieurs OS/systèmes de fichiers sur le même disque
- Accès aux mêmes données depuis 2 OS
- Reconstruction/formatage d'une seule partition

[MS MBR-GPT](https://www.tech2tech.fr/quelle-est-la-difference-entre-le-format-gpt-et-mbr-pour-un-disque/)

---

## Systèmes de fichiers

Il existe plus de 100 systèmes de fichiers (FS). Chaque FS définit sa façon de stocker et organiser l'information (journalisation, droits d'accès, métadonnées, ...).

[Wiki - système de fichiers](https://fr.wikipedia.org/wiki/Syst%C3%A8me_de_fichiers)

---

![height:500px](./img/Capt-FS-Win-App-Lin.PNG)

---

## Gestionnaire de disques

Un gestionnaire de disques sert à gérer les disques et les partitions : ajouter, modifier, formater, supprimer une partition.

Attention : l'information peut être définitivement perdue. **Ne pas toucher au disque C: sauf si vous êtes sûr !**

---

## Windows : gestionnaire de disques

![height:500px](./img/Capt-gest-disques-Windows.PNG)

---

## GParted

GParted (Gnome PARTition EDitor) : logiciel gratuit pour la gestion graphique des disques/partitions (par défaut dans Linux).
- Version Live (DVD ou clé USB) pour accéder aux disques éteints
- Beaucoup de FS supportés
- Création, suppression, modification de taille
- Contrôles, étiquettes, copier-coller
- Modification du UUID

[Site GParted](https://gparted.org/)

---

## Exemple GParted : Windows

![height:500px](./img/Capt-gparted-uuid-W10.PNG)

---

## Exemple GParted : Linux

![height:500px](./img/Capt-gparted-uuid-linux.PNG)

---

## IMPORTANT

Quand on touche au système :
- Toujours faire des backups
- Se renseigner
- Savoir ce que l'on fait
- Ne faire qu'une modification à la fois

---

![bg fit](./img/Capt-tab-byte.PNG)
