# Conception du SI d'une ville intelligence

## Contexte

Nous allons réfléchir à l'architecture du SI d'une ville intelligente.

## Point de départ

Nous partons des principes d'architecture suivants :

- Le SI est organisé en sous-système correspondant chacun à un thème (ex : "Gestion des déchêts")
- Une application web est mise à disposition pour chacun des thèmes (ex : "https://dechets.ma-ville.fr")
- L'authentification est systématique (les utilisateurs sont toujours authentifié)
- L'authentification est traitée de manière transverse (nous n'avons pas besoin de nous en préoccuper dans la conception)

Notre mission consiste à proposer une architecture pour mettre en oeuvre les fonctionnalités demandées pour les thèmes ci-après.

## Les utilisateurs

- Un **usager** dispose de droits limités.
- Un **agent** est habilité à traiter les demandes des usagers.

## Gestion des déchets

Un utilisateur peu :

- **Consulter le plan de ramassage des encombrants** (une carte affiche les rues avec une légende indiquant le jour de passage)
- **Signaler un dépôt sauvage** en fournissant la position et une photo.
- **Demander un ramassage d'emcombrant** en fournissant une position et une date de ramassage précise.

Exercice :

- a) Proposer une solution pour gérer et mettre à disposition le plan de ramassage des encombrants
- b) Proposer une architecture pour l'application avec un MCD pour l'éventuelle base de données


## Gestion du traffic

Nous disposons d'un ensemble de **capteurs intelligents** positionnés sur le réseau routier de la commune.

A chaque passage d'un véhicule, ces capteurs appellent une URL de notre choix en fournissant :

- L'identifiant du capteur.
- La vitesse du véhicule.

Nous exploitons les données en mettant en oeuvre les fonctionnalités suivantes accessibles par les **agents** :

- **Gérer les capteurs**
  - **Ajouter un capteur** (en spécifiant sa position GPS et la vitesse limite autorisée)
  - **Modifier un capteur** (en cas de déplacement)
  - **Supprimer un capteur** (en cas de déinstallation)
- **Calculer des statistiques** sur les 15 dernières minutes :
  - Le nombre de véhicules observés
  - La vitesse moyenne
  - La vitesse maximale
  - Le nombre d'excès de vitesse
- **Visualiser la liste des capteurs** avec :
  - Le temps écoulé depuis la dernière mesure.
  - La dernière mesure de vitesse.
  - Les statistiques sur les 15 dernières minutes.

Exercice :

- a) Proposer une architecture pour l'application
- b) Décrire le MCD de la base des capteurs


## Surveillance de l'espace public

Nous disposons d'un ensemble de caméra accessible via un réseau sécurisé par leurs adresses IP. Pour chaque camera :

- Nous connaissons la position et l'orientation.
- Nous avons accès au flux vidéo (`GET http://{IP_CAMERA}:8000/api/stream.avi`) et à la dernière image (`GET http://{IP_CAMERA}:8000/api/capture.png`)
- Nous pouvons réaliser un test de vie (`GET http://{IP_CAMERA}:8000/api/health` renvoyant un code 200 si tout va bien)

Nous souhaitons mettre à disposition des **agents** les fonctionnalités suivantes :

- **Gérer les caméras**
  - Ajouter, modifier ou supprimer une caméra 
  - Afficher la liste des caméras avec leur statut (le code de retour de `GET /api/health`)
  - Afficher le flux vidéo d'une caméra
- **Détecter des problèmes** en procédant comme suit :
  - **Analyser les images pour identifier les objets (personne, flamme,...)** (ex : [huggingface.io - object-detection - facebook/detr-resnet-50](https://huggingface.co/facebook/detr-resnet-50))
  - **Détecter un éventuellement attroupement** (plus de 10 personnes apparaissent sur une image).
  - **Détecter un personne immobile** (depuis plus de 15 minutes).
- **Visualiser les problèmes**

Exercice :

- a) Proposer une modélisation pour les données
- b) Proposer une architecture pour l'application

