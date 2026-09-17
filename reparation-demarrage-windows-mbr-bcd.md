# RAPPORT D'INTERVENTION TECHNIQUE — RÉPARATION DE DÉMARRAGE WINDOWS

## 1. Contexte et Cartographie des Volumes
- **Problématique :** Échec au démarrage du système d'exploitation Windows.
- **Identification des disques :**
  - `C:` : Disque principal de données / ancien emplacement du gestionnaire de démarrage.
  - `E:` : Partition cible contenant le système Windows (cible de boot).
  - `X:` : Partition de récupération (Recovery) Windows / Environnement de secours (WinPE).
  - `D:` : Volume vide / inutilisé.
  - `G:` : Disque virtuel Windows ISO.

---

## 2. Chronologie des Opérations et Diagnostic

### Étape 1 : Boot sur l'outil de réparation (Préparation)
Insertion d'un support d'installation (ISO Windows 10) et démarrage dans l'environnement de récupération de Windows (WinRE / Invite de commandes).

### Étape 2 : Tentative de réparation classique du secteur de démarrage (Échec partiel)
Exécution de la commande de réparation du MBR :
`bootrec /fixmbr`
- **Résultat :** Succès pour le MBR. 
- **Tentative de la commande `/fixboot` :** Refus d'accès.
- **Solution de contournement :** Utilisation de l'outil `bootsect` pour réécrire le secteur de démarrage système :
`bootsect /nt60 SYS`
- **Vérification :** Nouvelle exécution de `/fixboot` validée avec succès (Fixboot ok).

### Étape 3 : Analyse approfondie et reconstruction de la base BCD
Lenteur ou échec persistant de la commande `/rebuildbcd`. 
- **Investigation (Notepad & BCDedit) :** En ouvrant le Bloc-notes depuis l'invite de commandes, identification que l'OS se trouve sur la partition `E:`. À l'inverse, l'analyse `bcdedit` montre que le gestionnaire cherche à lancer le système depuis le lecteur `C:`.

### Étape 4 : Correction de la cible et recréation du BCD (Commandes BCDBOOT)
Forçage du démarrage sur le lecteur `E:` à l'aide des commandes de configuration :
`bcdboot E:\Windows /s E: /f BIOS /l fr-fr`
Puis configuration explicite du chargeur de démarrage (`bootmgr`) :
`bcdedit /set {bootmgr} device partition=E:`

### Étape 5 : Activation de la partition système (Diskpart)
Vérification et activation de la partition `E:` pour qu'elle soit reconnue comme active et bootable :
`diskpart` -> `select volume E` -> `active` -> `exit`

### Étape 6 : Remplacement du fichier Winload corrompu (Finition)
Au lancement de la machine, une erreur liée à `winload.exe` apparaît. Récupération d'un fichier de démarrage sain depuis la partition Recovery (`X:`) vers la partition système (`E:`).
`copy /y X:\Windows\System32\winload.exe E:\Windows\System32\winload.exe`
- **Vérification :** Le fichier est copié et validé, permettant le chargement correct du noyau Windows.

---

## 3. Bilan et Résultat
- **Statut de l'intervention :** Résolu avec succès.
- **État final :** Le système Windows amorce désormais correctement depuis la partition `E:`, le chargeur de démarrage (`bootmgr`) et le fichier `winload.exe` étant opérationnels et synchronisés.
