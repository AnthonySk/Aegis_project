# Projet AEGIS v1.0
# Spécifications techniques complètes

---

# 1. Présentation du projet

## 1.1 Description

AEGIS est une plateforme drone autonome développée autour d'un contrôleur de vol propriétaire conçu et fabriqué sur mesure.

Le projet a pour objectif de créer une architecture complète comprenant :

- une carte électronique de contrôle de vol développée en interne ;
- un firmware PX4 (à déveloper seul ?);
- un calculateur temps réel basé sur STM32H743 ;
- un ordinateur embarqué dédié à l'intelligence artificielle ;
- un système de vision ;
- une communication longue portée ;
- une station de contrôle au sol.

---

# 1.2 Objectifs techniques

La plateforme AEGIS doit permettre :

- stabilisation automatique du drone ;
- contrôle précis des moteurs ;
- navigation GPS autonome ;
- missions programmées ;
- transmission de télémétrie ;
- acquisition vidéo ;
- traitement d'image embarqué ;
- exécution de modèles IA ;
- évolution vers une autonomie avancée.

---

# 2. Architecture générale

Le système AEGIS est composé de trois sous-systèmes principaux :

## 2.1 Contrôleur de vol AEGIS Flight Controller

Fonctions :

- gestion du vol temps réel ;
- lecture des capteurs ;
- calcul d'attitude ;
- contrôle moteur ;
- communication MAVLink ;
- sécurité du drone.

Technologies :

- PCB propriétaire ;
- STM32H743 ;
- PX4 Autopilot.

---

## 2.2 Ordinateur embarqué

Fonctions :

- intelligence artificielle ;
- vision ;
- traitement vidéo ;
- ROS 2 ;
- calcul haut niveau.

Solutions :

- Raspberry Pi 5 + Hailo-8 ;
- NVIDIA Jetson Orin Nano.

---

## 2.3 Station sol

Fonctions :

- préparation des missions ;
- supervision ;
- affichage vidéo ;
- récupération des données.

---

# 3. Architecture système

Flux général :

Station sol

    |
    |
MAVLink

    |
    v

AEGIS Flight Controller

    |
    |
    +-- Capteurs
    |
    +-- ESC et moteurs

    |
    |
MAVLink / UART

    |
    v

Ordinateur embarqué

    |
    |
Caméra + IA + ROS 2

---

# 4. Plateforme aérienne

# 4.1 Châssis

Type :

- quadricoptère.

Configuration :

- X.

Matériaux possibles :

- composite ;
- plastique renforcé ;
- pièces imprimées en 3D.

Caractéristiques :

- bras démontables ;
- support batterie ;
- support contrôleur de vol ;
- support ordinateur embarqué ;
- support caméra.

Contraintes :

- faible masse ;
- rigidité ;
- résistance aux vibrations ;
- maintenance simple.

---

# 4.2 Propulsion

## Moteurs

Type :

- brushless triphasés 

Nombre :

- 4 moteurs.

Caractéristiques :

| Paramètre     | Valeur          |
|---------------|-----------------|
| Type          | Brushless       |
| KV            | 800 à 1000 KV   |
| Batterie      | LiPo 4S         |
| Configuration | Quadricoptère X |

Exemple :

- moteur 2216 900KV.

---

## ESC (Electronic Speed Controllers)

Fonction :

- commander la vitesse moteur ;
- convertir le signal du contrôleur ;
- protéger le moteur.

Caractéristiques :

| Paramètre | Valeur      |
|-----------|-------------|
| Courant   | 30 à 40A    |
| Signal    | PWM / DShot |
| Quantité  | 4           |

---

## Hélices

Caractéristiques :

- équilibrées ;
- adaptées au moteur ;
- faible vibration.

Exemple :

- 10x4.5 pouces.

---

# 5. Alimentation électrique

## 5.1 Batterie

Type :

- LiPo.

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| Cellules | 4S |
| Tension | 14.8V |
| Capacité | 5000 mAh |

---

## 5.2 Carte d'alimentation

Développement :

- PCB propriétaire AEGIS Power Board.

Fonctions :

- distribution batterie ;
- mesure tension ;
- mesure courant ;
- conversion 5V ;
- protection électrique.

Sorties :

- alimentation contrôleur de vol ;
- alimentation ordinateur embarqué ;
- alimentation capteurs.

---

# 6. Contrôleur de vol AEGIS Flight Controller

## 6.1 Objectif

Le contrôleur de vol AEGIS est une carte électronique conçue entièrement sur mesure.

Il remplace les cartes commerciales de type Pixhawk.

Fonctions :

- exécution PX4 ;
- stabilisation ;
- contrôle moteur ;
- gestion capteurs ;
- communication.

---

# 6.2 Processeur principal

## STM32H743

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| Architecture | ARM Cortex-M7 |
| Fréquence | 480 MHz |
| Bits | 32 bits |
| RAM | 1 Mo |
| Flash | 2 Mo |
| FPU | Oui |

---

# 6.3 Rôle du STM32H743

Le microcontrôleur réalise :

- boucle PID ;
- calcul attitude ;
- fusion capteurs ;
- gestion temps réel ;
- communication bas niveau ;
- commande moteurs.

---

# 6.4 Firmware du contrôleur de vol

Solution retenue :

PX4 Autopilot

Fonctions :

- stabilisation automatique ;
- contrôle des moteurs ;
- gestion des modes de vol ;
- navigation autonome ;
- gestion des sécurités ;
- communication MAVLink.

Le firmware PX4 est exécuté directement sur le STM32H743 du contrôleur AEGIS.

---

# 6.5 Capteurs embarqués

## IMU principale

Modèle :

ICM-42688-P

Fonctions :

- mesure accélération ;
- mesure vitesse angulaire ;
- estimation du mouvement.

Interface :

- SPI.

Rôle :

- fournir les données principales pour la stabilisation du drone.

---

## IMU secondaire

Modèle :

BMI088

Fonctions :

- accéléromètre ;
- gyroscope ;
- redondance capteur.

Interface :

- SPI.

Rôle :

- améliorer la fiabilité ;
- détecter une anomalie de la première IMU ;
- augmenter la sécurité du système.

---

## Baromètre

Modèle :

BMP390

Fonction :

- mesure altitude relative.

Interfaces :

- SPI ;
- I2C.

Rôle :

- maintien d'altitude ;
- estimation verticale.

---

## GPS

Modèle :

u-blox M10

Fonctions :

- position GPS ;
- vitesse ;
- navigation.

Interface :

- UART.

Rôle :

- navigation autonome ;
- missions GPS ;
- retour automatique.

---

# 6.6 Interfaces électroniques du contrôleur AEGIS

## Communication

Interfaces disponibles :

- UART ;
- SPI ;
- I2C ;
- CAN ;
- USB.

---

## Contrôle moteur

Sorties :

- PWM ;
- DShot.

Utilisation :

- communication avec les ESC ;
- contrôle précis de la vitesse moteur.

---

## Programmation et maintenance

Interface :

- SWD Debug.

Fonctions :

- programmation STM32 ;
- débogage firmware ;
- diagnostic matériel.

---

# 6.7 Architecture PCB AEGIS Flight Controller

La carte électronique comprend :

## Partie calcul

Composants :

- STM32H743 ;
- mémoire Flash ;
- oscillateur ;
- interface debug.

---

## Partie capteurs

Composants :

- ICM-42688-P ;
- BMI088 ;
- BMP390.

---

## Partie alimentation

Composants :

- régulateur 3.3V ;
- régulateur 5V ;
- protections électriques ;
- filtres anti-bruit.

---

## Partie communication

Composants :

- connecteurs UART ;
- bus CAN ;
- USB ;
- interfaces périphériques.

---

# 7. Ordinateur embarqué

## 7.1 Fonction

L'ordinateur embarqué réalise les calculs qui ne sont pas critiques pour la stabilité.

Fonctions :

- intelligence artificielle ;
- traitement vidéo ;
- reconnaissance d'image ;
- calcul autonome ;
- ROS 2 ;
- communication haut niveau.

---

# 7.2 Solution économique

## Raspberry Pi 5 + accélérateur IA

---

## Raspberry Pi 5

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| Processeur | Broadcom BCM2712 |
| Architecture | ARM Cortex-A76 |
| Fréquence | 2.4 GHz |
| RAM | 8 Go |
| Système | Linux |

---

## Accélérateur IA Hailo-8

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| Type | Accélérateur neuronal |
| Puissance | 26 TOPS |
| Utilisation | Réseaux neuronaux |

Applications :

- détection d'objet ;
- classification ;
- vision temps réel.

---

# 7.3 Solution haute performance

## NVIDIA Jetson Orin Nano

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| CPU | ARM Cortex-A78AE |
| GPU | NVIDIA Ampere |
| IA | Jusqu'à 40 TOPS |
| RAM | 8 Go |

Utilisation :

- SLAM ;
- navigation autonome avancée ;
- traitement vidéo complexe ;
- modèles IA lourds.

---

# 8. Système de vision

## 8.1 Caméra

Solution :

Raspberry Pi Camera Module 3

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| Capteur | Sony |
| Résolution | 12 MP |
| Vidéo | 1080p |
| Interface | CSI |
| Autofocus | Oui |

---

# 8.2 Traitement d'image

Bibliothèques :

- OpenCV ;
- ONNX Runtime ;
- TensorFlow Lite.

Fonctions :

- détection d'objet ;
- suivi ;
- classification ;
- analyse environnementale.

---

# 8.3 Intelligence artificielle

Modèles possibles :

- YOLO ;
- MobileNet ;
- modèles ONNX.

Exemples d'utilisation :

- reconnaissance d'objet ;
- évitement d'obstacle ;
- assistance navigation ;
- analyse terrain.

---

# 9. Communication

# 9.1 MAVLink

MAVLink est le protocole principal de communication du système.

Connexions :

AEGIS Flight Controller ↔ Ordinateur embarqué

AEGIS Flight Controller ↔ Station sol

---

Données échangées :

- télémétrie ;
- position ;
- vitesse ;
- état batterie ;
- commandes ;
- missions.

---

# 9.2 Liaison radio

Solution :

SiK Telemetry Radio.

Caractéristiques :

| Paramètre | Valeur |
|-|-|
| Fréquence | 915 MHz |
| Portée | 1 à 5 km |
| Protocole | MAVLink |

---

# 10. Architecture logicielle

# 10.1 Contrôleur de vol

Système :

PX4 Autopilot

Langage :

C/C++

Fonctions :

- contrôle temps réel ;
- gestion capteurs ;
- stabilisation ;
- commande moteurs.

---

# 10.2 Ordinateur embarqué

Système :

Linux.

Middleware :

ROS 2 Humble.

Fonctions :

- communication entre logiciels ;
- gestion des nœuds ;
- traitement données.

---

# 10.3 Langages utilisés

## C++

Utilisation :

- firmware ;
- drivers ;
- communication bas niveau ;
- modules temps réel.

---

## Python

Utilisation :

- intelligence artificielle ;
- traitement d'image ;
- automatisation ;
- analyse données.

---

# 11. Simulation et développement

## Outils logiciels

Utilisation :

- Git ;
- CMake ;
- Docker ;
- VS Code.

---

# 11.1 Simulation

Technologies :

- PX4 SITL ;
- Gazebo.

Objectifs :

- tester les vols virtuels ;
- valider les algorithmes ;
- développer sans risque matériel.

---

# 12. Architecture finale AEGIS

Résumé :

| Élément | Technologie |
|-|-|
| Projet | AEGIS |
| Contrôleur de vol | AEGIS Flight Controller |
| Firmware | PX4 Autopilot |
| Microcontrôleur | STM32H743 |
| Fréquence MCU | 480 MHz |
| IMU principale | ICM-42688-P |
| IMU secondaire | BMI088 |
| Baromètre | BMP390 |
| GPS | u-blox M10 |
| Ordinateur embarqué | Raspberry Pi 5 |
| Accélérateur IA | Hailo-8 |
| Alternative IA | Jetson Orin Nano |
| Middleware | ROS 2 Humble |
| Communication | MAVLink |
| Vision | OpenCV |
| IA | ONNX / TensorFlow Lite |
| Simulation | PX4 SITL + Gazebo |

---

# 13. Budget estimatif

| Élément | Prix estimé |
|-|-:|
| PCB AEGIS Flight Controller | 50-100 € |
| STM32H743 | 20 € |
| IMU principale | 10-20 € |
| IMU secondaire | 10-20 € |
| Baromètre | 5-10 € |
| GPS | 35 € |
| Raspberry Pi 5 | 90 € |
| Hailo-8 | 100 € |
| Caméra | 40 € |
| Radio MAVLink | 40 € |
| Moteurs | 80 € |
| ESC | 60 € |
| Batterie | 60 € |
| Châssis | 50 € |

---

# Budget total estimé

Environ :

650 à 750 €

---

# 14. Objectif AEGIS v1.0

La première version doit permettre :

- conception d'un contrôleur de vol propriétaire ;
- exécution PX4 ;
- stabilisation complète ;
- contrôle moteurs ;
- navigation GPS ;
- communication MAVLink ;
- traitement vidéo ;
- intelligence artificielle embarquée ;
- évolution vers un drone autonome complet.

---

# 15. Évolutions futures

## AEGIS v2.0

Possibilités :

- LiDAR ;
- caméra stéréo ;
- évitement d'obstacles ;
- SLAM ;
- navigation sans GPS ;
- essaim de drones.

---

## AEGIS v3.0

Objectif :

- autonomie complète ;
- prise de décision embarquée ;
- missions complexes ;
- coopération multi-drones.