# RAPPORT D'INTERVENTION TECHNIQUE — RÉPARATION DES PERFORMANCES SYSTÈME

## 1. Contexte et Symptômes
* **Problématique :** Utilisation anormale du processeur (CPU) et de la mémoire vive (RAM) à 100 %.
* **Objectif :** Diagnostiquer la source de la surcharge matérielle, nettoyer l'image système et stopper les processus parasites.

---

## 2. Chronologie des Opérations et Résolution

### Étape 1 : Optimisation et exclusion de l'antivirus (CPU)
* **Constat :** L'analyse de l'activité du processeur a révélé que l'antivirus surconsommait les ressources.
* **Action :** Ajout d'une règle d'exclusion sur le lecteur système `C:` (disque de travail).
* **Vérification :** Baisse immédiate et notable de la charge du processeur.

### Étape 2 : Réparation et maintenance des composants Windows (DISM)
Exécution des commandes de maintenance de l'image système :
- Vérification de l'état des composants :
  `dism /online /cleanup-image /checkhealth`
- Réparation des systèmes corrompus :
  `dism /online /cleanup-image /restorehealth`
- Nettoyage des composants corrompus/obsolètes :
  `dism /online /cleanup-image /startcomponentcleanup`
* **Vérification :** Restauration réussie du magasin de composants et nettoyage final du système.

### Étape 3 : Analyse approfondie et arrêt des processus gourmands (RAM)
* **Investigation détaillée :** Utilisation du raccourci `Win + R` pour lancer le Moniteur de ressources (`resmon`) afin d'identifier les processus consommant la mémoire vive.
* **Action sur les scripts parasites :** Détection de multiples instances de la commande `PING.EXE` s'exécutant sous forme de scripts en arrière-plan. Arrêt forcé de ces processus avec la commande :
  `taskkill /f /im PING.EXE`
* **Vérification :** Disparition des scripts bloquants.

### Étape 4 : Analyse des fichiers système (SFC)
* **Action :** Lancement d'une vérification globale de l'intégrité des fichiers système via l'invite de commandes (DOS) :
  `sfc /scannow`
* **Vérification :** Validation et correction des fichiers système pour stabiliser l'utilisation de la RAM.

---

## 3. Bilan et Résultat
* **Statut de l'intervention :** Résolu avec succès.
* **État final :** Le processeur et la RAM ont retrouvé des performances normales grâce à l'exclusion ciblée de l'antivirus, la maintenance DISM/SFC et l'élimination des scripts `PING.EXE` parasites.
