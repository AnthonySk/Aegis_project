# Projet ARGUS v1.0
## Spécifications fonctionnelles

---

# 1. Description générale

Le projet **ARGUS v1.0** consiste à développer une plateforme drone autonome capable d'effectuer des missions d'observation et de collecte de données dans un environnement complexe.

Le système doit permettre au drone d'opérer avec un minimum d'intervention humaine, tout en assurant la transmission des informations collectées vers une station de contrôle.

L'objectif est de créer une plateforme robotique évolutive permettant l'intégration future de nouveaux capteurs et algorithmes.

---

# 2. Fonctions principales

| Identifiant                                                   | Fonction principale                               | Description                                                         |
|---------------------------------------------------------------|---------------------------------------------------|---------------------------------------------------------------------|
| [FP1](#fp1--planification-et-exécution-dune-mission-autonome) | Planification et exécution d'une mission autonome | Permettre au drone d'effectuer une mission définie par un opérateur |
| [FP2](#fp2--acquisition-et-collecte-de-données)               | Acquisition et collecte de données                | Permettre l'observation et l'enregistrement d'informations          |
| [FP3](#fp3--communication-avec-une-station-de-contrôle)       | Communication avec une station de contrôle        | Permettre l'échange d'informations entre le drone et l'opérateur    |
| [FP4](#fp4--gestion-de-la-sécurité-du-système)                | Gestion de la sécurité du système                 | Garantir un fonctionnement fiable et sécurisé                       |
| [FP5](#fp5--évolutivité-de-la-plateforme)                     | Évolutivité de la plateforme                      | Permettre l'ajout de nouvelles fonctionnalités                      |
| [FP6](#fp6--interaction-utilisateur)                          | Interaction utilisateur                           | Fournir une interface de contrôle et de supervision                 |

---

# FP1 — Planification et exécution d'une mission autonome

## Objectif

Permettre au drone d'effectuer une mission définie par un opérateur avec un minimum d'intervention humaine.

---

## FS1.1 — Création d'une mission

Le système doit permettre à un opérateur de :

- définir une zone d'opération ;
- définir des points de passage GPS (*waypoints*) ;
- définir une altitude de vol ;
- définir une vitesse de déplacement ;
- définir les actions à effectuer pendant la mission.

Exemple :

```
Point de départ
      |
      v
Waypoint 1
      |
      v
Waypoint 2
      |
      v
Zone d'observation
      |
      v
Retour base
```

---

## FS1.2 — Chargement d'une mission

Le système doit permettre :

- la transmission d'une mission depuis la station de contrôle ;
- la validation des paramètres reçus ;
- le stockage temporaire de la mission dans le drone.

---

## FS1.3 — Navigation autonome

Le drone doit pouvoir :

- suivre une trajectoire GPS ;
- maintenir une altitude définie ;
- ajuster sa trajectoire ;
- compenser les perturbations extérieures.

---

## FS1.4 — Gestion de fin de mission

Le drone doit pouvoir :

- terminer automatiquement une mission ;
- retourner au point de départ ;
- effectuer un atterrissage contrôlé ;
- signaler l'état final de la mission.

---

# FP2 — Acquisition et collecte de données

## Objectif

Permettre au drone d'observer son environnement et de collecter des informations exploitables.

---

## FS2.1 — Acquisition vidéo

Le système doit permettre :

- la capture d'images ;
- l'enregistrement vidéo ;
- la transmission du flux vidéo ;
- l'association des images avec des données de position.

---

## FS2.2 — Acquisition des données de vol

Le système doit enregistrer :

- position GPS ;
- altitude ;
- vitesse ;
- orientation ;
- niveau de batterie ;
- état des composants.

---

## FS2.3 — Stockage des données

Le système doit :

- sauvegarder les données collectées ;
- organiser les données par mission ;
- permettre l'exportation des résultats.

---

## FS2.4 — Traitement embarqué

Le système peut effectuer :

- analyse d'image ;
- filtrage des données ;
- extraction d'informations utiles ;
- prétraitement avant transmission.

---

# FP3 — Communication avec une station de contrôle

## Objectif

Permettre à un opérateur de superviser et d'interagir avec le drone.

---

## FS3.1 — Transmission de télémétrie

Le drone doit transmettre :

- position ;
- altitude ;
- vitesse ;
- orientation ;
- état batterie ;
- état de mission.

---

## FS3.2 — Commande à distance

L'opérateur doit pouvoir :

- démarrer une mission ;
- interrompre une mission ;
- modifier certains paramètres ;
- demander un retour automatique.

---

## FS3.3 — Supervision

La station de contrôle doit permettre :

- l'affichage de la position du drone ;
- la visualisation des données reçues ;
- le suivi de l'état du système ;
- la consultation de l'historique des missions.

---

# FP4 — Gestion de la sécurité du système

## Objectif

Garantir la fiabilité du système en cas d'événement inattendu.

---

## FS4.1 — Gestion de perte de communication

En cas de perte de liaison, le système doit :

- détecter la perte de communication ;
- appliquer une procédure définie ;
- informer l'opérateur.

---

## FS4.2 — Gestion de batterie faible

Le système doit :

- surveiller le niveau d'énergie ;
- avertir l'opérateur ;
- déclencher une procédure adaptée.

---

## FS4.3 — Surveillance interne

Le système doit surveiller :

- les erreurs capteurs ;
- la température des composants ;
- les anomalies système ;
- l'état général du drone.

---

# FP5 — Évolutivité de la plateforme

## Objectif

Permettre l'évolution du système après la première version.

---

## FS5.1 — Ajout de capteurs

La plateforme doit permettre l'intégration de :

- nouveaux capteurs ;
- modules de communication ;
- systèmes d'acquisition supplémentaires.

---

## FS5.2 — Extension logicielle

Le système doit permettre :

- l'ajout de nouveaux algorithmes ;
- la mise à jour logicielle ;
- l'ajout de nouveaux modes de fonctionnement.

---

# FP6 — Interaction utilisateur

## Objectif

Fournir une interface permettant l'utilisation et la supervision du drone.

---

## FS6.1 — Interface opérateur

L'utilisateur doit pouvoir :

- créer une mission ;
- suivre le drone ;
- consulter les données ;
- recevoir les alertes.

---

## FS6.2 — Gestion des accès

Le système peut gérer :

- différents profils utilisateurs ;
- différents niveaux d'autorisation ;
- l'historique des actions réalisées.

---

# 3. Résumé fonctionnel

| Domaine       | Fonction                              |
|---------------|---------------------------------------|
| Navigation    | Effectuer des missions autonomes      |
| Observation   | Capturer et analyser des données      |
| Communication | Échanger avec une station de contrôle |
| Sécurité      | Gérer les situations anormales        |
| Évolution     | Ajouter de nouvelles capacités        |
| Interaction   | Permettre la supervision humaine      |

---

# 4. Limites du périmètre v1.0

La version initiale du projet ne comprend pas :

- le développement d'un contrôleur de vol complet ;
- la conception d'un moteur de navigation propriétaire ;
- l'autonomie totale sans supervision humaine.

Le système s'appuie sur des briques existantes afin de concentrer le développement sur les fonctions autonomes, la collecte de données et l'intelligence embarquée.