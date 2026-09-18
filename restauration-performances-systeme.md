# RAPPORT D'INTERVENTION TECHNIQUE — RÉPARATION DES PERFORMANCES SYSTÈME

## 1. Contexte et Symptômes
* **Problématique :** Utilisation anormale du processeur (CPU) et de la mémoire vive (RAM) à 100 %.
* **Objectif :** Diagnostiquer la source de la surcharge matérielle, nettoyer l'image système, éliminer les processus parasites et neutraliser les points de persistance au démarrage.

---

## 2. Chronologie des Opérations et Résolution

### Étape 1 : Réparation et maintenance des composants Windows (DISM & SFC)
Exécution des commandes de maintenance de l'image système et des fichiers :
- Vérification et réparation de l'intégrité :
  `dism /online /cleanup-image /checkhealth`
  `dism /online /cleanup-image /restorehealth`
  `dism /online /cleanup-image /startcomponentcleanup`
- Vérification globale des fichiers système via l'invite de commandes :
  `sfc /scannow`

### Étape 2 : Investigation avancée et neutralisation des processus parasites (RAM)
* **Investigation détaillée :** Utilisation du raccourci `Win + R` pour lancer le Moniteur de ressources (`resmon`) afin d'analyser en profondeur l'activité de la mémoire.
* **Constat critique :** Présence d'environ **500 instances** du processus `PING.EXE` s'exécutant en arrière-plan sous forme de scripts.
* **Action corrective :** Arrêt forcé et massif des processus récurrents via l'invite de commandes :
  `taskkill /f /im PING.EXE`

### Étape 3 : Analyse des services et des programmes au démarrage (Persistance)
* **Vérification des services :** Contrôle des services Windows (aucun dysfonctionnement majeur identifié).
* **Analyse des programmes au démarrage :** Inspection des éléments lancés au démarrage du système, révélant plusieurs incohérences (exécutions automatiques de navigateurs et de scripts).
* **Découverte majeure :** Dans la ligne de commande associée à une tâche de démarrage **PowerShell**, présence d'un script masqué programmé pour lancer une boucle de pings automatiques et infinis vers Google en arrière-plan à chaque démarrage.
* **Résolution :** Désactivation des entrées incohérentes dans les programmes au démarrage et neutralisation de la persistance PowerShell.

---

## 3. Bilan et Résultat
* **Statut de l'intervention :** Résolu avec succès.
* **État final :** Le processeur et la RAM ont retrouvé des performances nominales grâce à la maintenance du système, l'éradication des 500 processus `PING.EXE` et le nettoyage des programmes mal configurés au démarrage.
