# Vente de carte en ligne

## Contexte

Nous souhaitons développer un site de e-commerce spécialisé dans la vente de cartes papiers (IGN, Michelin,...).

## Les utilisateurs

Nous distinguons :

- Les **clients** qui achètent des cartes.
- Les **administrateurs** qui gèrent la liste des références en vente et les stocks.

## Fonctionnalités du MVP

Un **client** devra :

- **S'inscrire** avec un email et un mot de passe.
- **Se connecter** (les utilisateurs non connectés seront redirigés vers la page de connexion ou d'inscription).

Une fois connecté, **le client** pourra :

- **Rechercher une carte** avec la possibilité de :
  - Filtrer par fournisseur
  - Filtrer par lieu d'intérêt
- **Commander une carte** en spécifiant son adresse de livraison (nous ne traiterons pas l'intégration du module de paiement).
- **Afficher la liste de ses commandes** avec leur statut ("en attente de traitement", "expédiée")

Un **administrateur** aura quand à lui la charge de :

- **Gérer les cartes**
  - **Ajouter une carte** (référence, fournisseur, emprise géographique, nombre en stock...)
  - **Mettre jour une carte** (ex : mise à jour du stock)

- **Gérer les commandes**
  - **Afficher la liste des commandes** "en attente de traitement"
  - **Changer le statut d'une commande** en "expédiée" (après avoir envoyé la carte au client par courrier)

Nous mettons aussi en oeuvre les automatismes suivants :

- En cas de **nouvelle commande**, un mail est envoyé aux administrateurs.
- En cas de **changement de statut de la commande**, un mail est **envoyé à l'utilisateur**. 



Exercice :

- a) Choisir un solution pour procéder au géocodage (côté client? côté serveur?)
- b) Proposer une architecture pour l'application.
- c) Proposer une diagramme de classe pour représenter les données et principaux services de l'application.


## V2 - Carte à la demande

Pour enrichir l'offre, nous décidons de proposer des cartes imprimées à la demande à partir des flux WMTS de la Géoplateforme.

### Nouvelle fonctionnalités

Une fois connecté, **l'utilisateur** peut désormais :

- **Commander une impression de carte** en spécifiant le centre et le niveau de zoom.

Pour limiter les opérations de l'**administrateur**, la commande d'une impression de carte déclenche :

- Le **rendu de la carte sous forme d'une image** (avec ajout d'une référence à la commande)
- Le lancement sur un **serveur d'impression** de :
  - L'**impression de la carte** (avec la référence de la commande)
  - L'**impression de l'adresse sur une enveloppe** (avec la référence de la commande)

Notre **administrateur** procède à un contrôle qualité visuel avant de :

- Mettre la carte dans l'enveloppe
- Changer le statut de la commande en "expédiée"


Exercice :

- a) Adapter le modèle de données
- b) Proposer une nouvelle architecture pour l'application en supposant que le serveur d'impression présente une API REST pour contrôler l'impression









