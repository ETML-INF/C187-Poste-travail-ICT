---
marp: true
theme: default
paginate: true
footer: "ETML - Module 187 - Boot"
---

<!-- header: "Module 187 - Démarrage" -->
# 2 - Démarrage

ID du module 187 : OO1 et OO7

Ce chapitre traite les différentes parties du démarrage d'un PC comme l'UEFI ou le POST.

---

## Amorcage

Que se passe-t-il entre le moment où l'on appuie sur le bouton ON et l'affichage de l'écran de login ?

Plusieurs étapes vont se succéder, selon sur le slide suivant :

---

![bg fit](./img/Capt-seq-dem-pc.PNG)

---

## Bouton ON, alimentation et processeur

C'est le "réveil" : juste la mise sous tension des composants essentiels...

---

## Puce BIOS

La puce BIOS contient le code permettant le démarrage du PC. Elle est fixée sur la carte mère ou intégrée dans le processeur et est complètement liée au matériel.

C'est le lien entre le matériel et le logiciel (Hardware/Software).
Elle permet le lancement des routines de démarrage, la première étant le *POST*, en chargeant son code en mémoire.

Il est possible de mettre à jour le BIOS ("flasher le BIOS").
- Intervention délicate : bien se renseigner, suivre la marche à suivre, faire des backups
- En cas d'échec, le PC peut ne plus booter

---

## POST (Power On Self Test)

**POST** = *Power On Self Test*

Cette phase, aussi appelée **pré-boot**, teste et initialise tous les composants matériels du PC ainsi que les compatibilités.

Des bips sonores ou des messages peuvent être entendus/affichés. Selon la gravité du problème, le boot peut être interrompu.

Exemple : RAM mal insérée = bips et boot interrompu.

---

## BIOS

**BIOS** = **Basic Input Output System**

Au début des années 80, le BIOS est un code écrit en assembleur sur une puce fixée sur la carte mère (toujours le cas maintenant).

Il exécute les routines permettant le démarrage.

Limitations :
- Sensibilité aux attaques
- Limitations matérielles
- Interface ancienne (pas de souris, navigation avec les flèches)

---

## UEFI

C'est l'évolution du BIOS, pour les raisons décrites ci-dessus. Il est possible de l'émuler en choisissant l'option "Legacy". **UEFI** = **Unified Extensible Firmware Interface**
- Codé en C, plus souple
- Meilleures performances
- Rapidité
- Sécurité renforcée
- Prise en charge graphique
- Disques jusqu'à 9,4Zo
- Gestion de multiples OS
- Évolutif
- Prise en charge du réseau

---

![bg fit](./img/Capt-uefi-main.PNG)

---

## Accès au BIOS/UEFI

Pour accéder au BIOS/UEFI (ou Setup), on presse au démarrage sur une touche (souvent F2 ou Delete, selon le fabricant).

- Onglet SECURITY : mots de passe
- Onglet ADVANCED-BOOT : informations pour le boot

**Attention :**
- Ne pas modifier le BIOS/UEFI sans connaissance
- Sauvegarder/noter tous les paramètres
- Se renseigner sur le site du constructeur
- Ne changer qu'un paramètre à la fois

---

## MBR vs GPT

En résumé pour le MBR-GPT :

![height:400px](./img/Capt-resume-mbr-gpt.PNG)

---

## MBR vs GPT

- Pour le **BIOS** : **MBR** = Master Boot Record
- Pour l'**UEFI** : **GPT** = GUID Partition Table

**GRUB** et **LILO** sont les bootloaders les plus connus sous Linux.

---

## Chargement de l'OS

Lorsque tous les tests matériels sont faits, on cherche un endroit pour lancer le système d'exploitation. 
C'est une zone du disque qui contient des informations comme le nombre et les tailles des partitions ainsi que le fait qu'elle soit "bootable".

---

## Chargement de Windows (UEFI)

1. Firmware UEFI, ordre de boot, EFI Boot Loader
2. Windows Boot Manager (BCD)
3. Windows Boot Loader (winload.efi)
4. Chargement en mémoire du kernel et de SMSS.exe
5. Chargement des services et processus
6. winlogon.exe pour fenêtre de login, puis shell explorer.exe pour bureau

[Malekal - Processus démarrage UEFI Windows](https://www.malekal.com/processus-demarrage-uefi-windows/)

---

## Chargement de Linux

1. Recherche du MBR, chargement du GRUB
2. Charge le noyau et monte le système de fichiers
3. Le programme init ou systemd lance toutes les autres tâches

[Goffinet - Démarrage Linux](https://linux.goffinet.org/administration/processus-et-demarrage/demarrage-du-systeme-linux/)

---

## Pour aller plus loin

- [Boot PC (NeoSmart)](https://neosmart.net/wiki/mbr-boot-process/)
