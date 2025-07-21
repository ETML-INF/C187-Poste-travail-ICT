---
marp: true
theme: default
paginate: true
footer: "ETML - Module 187 - Installation du système d'exploitation"
---

<!-- header: "Module 187 - Installation du système d'exploitation" -->
# 5 - Installation du système d'exploitation

ID du module 187 : OO2

Ce chapitre traite de l'installation d'un système d'exploitation avec les contraintes et les prérequis.

---

## Installation de Windows 10 et 11

L'installation d'un OS peut se faire avec différents supports :
- DVD
- clé USB
- disque externe
- réseau

Il n'est pas nécessaire de modifier l'ordre de boot dans le BIOS. Au démarrage, appuyez sur F8/F10/F12 pour obtenir le menu de démarrage (boot menu).

---

## Compatibilité et spécifications

Avant de commencer l'installation, assurez-vous de la disponibilité et de la compatibilité entre le matériel et le logiciel.

**Spécifications minimum**
- Windows 10 : CPU 1GHz, 2Go RAM, 20Go HD libre, Internet
- Windows 11 : CPU 1GHz (2 coeurs), 4Go RAM, 64Go disque, UEFI non Legacy, Internet

---

## Partitionnement lors de l'installation

Lors de l'installation, 3 partitions seront créées :
- Partition de démarrage (Boot Loader)
- Partition OS
- Partition de récupération

Il est possible de modifier la taille du disque système à la fin de l'installation avec le gestionnaire de disque, mais l'espace "récupérable" sera limité.

---

## Backup et installation sur système existant

Dans le cas d'un système existant, il faut toujours faire un backup avant de lancer l'installation.

---

## Ajout de programmes/applications

Une fois l'OS installé, il est possible d'ajouter des programmes/applications. Selon le fabricant, il y aura plusieurs modes d'installation.

---

## Gestion des programmes

Dans **Programmes et fonctionnalités** (Windows), on peut voir, désinstaller ou modifier une application.

Pour Linux, on parle de **gestionnaire de paquets**.
