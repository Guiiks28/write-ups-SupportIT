# RAPPORT D'INTERVENTION TECHNIQUE — GESTION DES DISQUES ET RESTAURATION DE FICHIERS

## 1. Contexte et Problématique
* **Problématique :** Disques durs invisibles ou hors ligne, erreurs système détectées sur le disque principal (`C:`), et nécessité de récupérer des données personnelles spécifiques (dossier "York") pour les replacer dans le répertoire images de l'utilisatrice.
* **Objectifs :** Diagnostiquer et réparer les erreurs du disque `C:`, réactiver un disque hors ligne, restaurer l'accès à un second disque via `diskpart`, et extraire les fichiers cibles.

---

## 2. Chronologie des Opérations et Résolution

### Étape 1 : Diagnostic et réparation du disque principal (CHKDSK)
* **Constat :** Suspicion d'erreurs logiques ou physiques sur le système de fichiers du disque principal suite à un diagnostic préalable.
* **Action :** Lancement d'une analyse des erreurs avec la commande de vérification :
  `chkdsk C: /r`
* **Planification de la réparation :** Comme le disque système est verrouillé au démarrage, validation de la planification de la réparation au prochain redémarrage avec la commande globale :
  `chkdsk /f /r`
* **Vérification :** Correction automatique des secteurs défectueux et des erreurs du système de fichiers par Windows lors du reboot.

### Étape 2 : Diagnostic des disques via la Gestion des disques
* **Action :** Utilisation du raccourci `Win + R`, puis saisie de la commande `diskmgmt.msc` pour ouvrir l'interface de gestion des disques.
* **Constat :** Identification d'un disque marqué comme "Hors ligne". 
* **Résolution :** Réactivation manuelle du disque pour le rendre de nouveau opérationnel sous l'explorateur Windows.

### Étape 3 : Récupération et restauration des fichiers ciblés (Dossier "York")
* **Constat :** Le dossier de données recherché ("York") était stocké sur le lecteur initialement situé sur le disque hors ligne.
* **Action :** Extraction des fichiers nécessaires et réintégration de ceux-ci directement dans le dossier "Images" de l'utilisatrice.
* **Vérification :** Intégrité et emplacement des dossiers validés.

### Étape 4 : Restauration et gestion du second disque via Diskpart
Pour le second disque présentant des anomalies d'accès, utilisation de l'interpréteur de commandes `diskpart` :
- Affichage de la liste des disques connectés : `list disk`
- Sélection du disque concerné : `select disk X`
- Sélection de la partition cible : `select partition Y`
- Activation / remise en état de la structure pour restaurer l'accès complet aux volumes.
* **Vérification :** Les disques sont de nouveau reconnus, montés et accessibles sans erreur sous le système.

---

## 3. Bilan et Résultat
* **Statut de l'intervention :** Résolu avec succès.
* **État final :** Le disque système `C:` a été analysé et réparé en profondeur via `chkdsk`, les disques hors ligne ont été réactivés (via l'interface graphique et `diskpart`), et les fichiers de l'utilisatrice ont été replacés au bon endroit.
