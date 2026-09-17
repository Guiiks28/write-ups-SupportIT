# RAPPORT D'INTERVENTION TECHNIQUE — GESTION DES DISQUES ET RESTAURATION DE FICHIERS

## 1. Contexte et Problématique
* **Problématique :** Disques durs invisibles ou hors ligne dans le système, et nécessité de récupérer des données personnelles spécifiques (dossier "York") pour les replacer dans le répertoire images de l'utilisatrice (Mme Michu).
* **Objectifs :** Réactiver un disque hors ligne, restaurer l'accès à un second disque via les commandes `diskpart`, et extraire/restaurer les fichiers cibles.

---

## 2. Chronologie des Opérations et Résolution

### Étape 1 : Diagnostic des disques via la Gestion des disques
* **Action :** Utilisation du raccourci `Win + R`, puis saisie de la commande `diskmgmt.msc` pour ouvrir l'interface de gestion des disques.
* **Constat :** Identification d'un disque marqué comme "Hors ligne". 
* **Résolution :** Réactivation manuelle du disque pour le rendre de nouveau opérationnel sous l'explorateur Windows.

### Étape 2 : Récupération et restauration des fichiers ciblés (Dossier "York")
* **Constat :** Le dossier de données recherché ("York") était stocké sur un lecteur `F:` initialement situé sur le disque hors ligne.
* **Action :** Extraction des fichiers nécessaires depuis le disque cible (`E:` / `F:`) et réintégration de ceux-ci directement dans le dossier "Images" de l'utilisatrice.
* **Vérification :** Intégrité et emplacement des dossiers validés.

### Étape 3 : Restauration et gestion du second disque via Diskpart
Pour le second disque présentant des anomalies d'accès, utilisation de l'interpréteur de commandes `diskpart` :
- Affichage de la liste des disques connectés :
  `list disk`
- Sélection du disque concerné :
  `select disk X` *(remplacé par le numéro du disque)*
- Sélection de la partition cible :
  `select partition Y`
- Activation / remise en état de la structure pour restaurer l'accès complet aux volumes.
* **Vérification :** Les deux disques sont de nouveau reconnus, montés et accessibles sans erreur sous le système.

---

## 3. Bilan et Résultat
* **Statut de l'intervention :** Résolu avec succès.
* **État final :** Les deux disques durs ont été entièrement récupérés et réactivés (via l'interface graphique et `diskpart`), et les fichiers de l'utilisatrice ont été replacés au bon endroit dans son arborescence de dossiers.
