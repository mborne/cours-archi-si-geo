# IRL - un jeu qui varie les défis dans le monde réel!

## Contexte

Il nous vient l'idée (géniale) de développer un jeu mobile incitant à se promener avec des objectifs plus variés que capturer des êtres virtuels ou flasher des QR codes.

Nous voulons offrir **une grande diversité de défis dans le monde réel !**

Nous décidons d'éprouver le concept avec une première version qui proposera les défis suivants :

- **Se rendre à une position donnée** (nous ferons confiance au GPS du téléphone pour la validation du défi).
- **Flasher un QR code** (nous présenterons uniquement la position à l'utilisateur, qui devra soumettre la valeur d'un token encodé dans le QR code).
- **Suivre un parcours** avec un éventuel temps limite (nous présenterons la trace à suivre, l'utilisateur soumettra une trace GPS en guise de preuve).

## Les utilisateurs

Nous distinguerons deux rôles :

* Les **utilisateurs**.
* Les **administrateurs** (qui seront initialement au nombre de 1).

## Fonctionnalités détaillées

Un **utilisateur** devra :

- S'inscrire avec un email et un mot de passe.
- Se connecter (les utilisateurs non connectés seront redirigés vers la page de connexion ou d'inscription).

**Une fois connecté, l'utilisateur** pourra, à l'aide d'une carte :

- Visualiser les défis dans un rayon de 5 km autour de lui.
- Visualiser les détails d'un défi.
- Valider un défi en soumettant une preuve.

Un **administrateur** pourra de son côté :

- Gérer les utilisateurs.
- Gérer les défis.

## Choix d'architecture initiaux

Pour valider le concept :

- Nous minimiserons les frais de développement en créant une **application web** (qui sera ouverte dans le navigateur du téléphone).
- Nous minimiserons les frais d'hébergement en utilisant une **architecture monolithique** (une seule machine pour le site et sa BDD).
- Nous exploiterons nos connaissances ENSG en utilisant le **SGBD PostgreSQL avec l'extension PostGIS** pour stocker des positions et des chemins.
- Nous irons au plus simple pour l'inscription (`/register`) et la connexion (`/login`) avec des formulaires web classiques.
- Nous préparerons la croissance avec une **API REST/JSON** pour :
  - La **recherche des défis** dans un rayon de 5 km (`GET /api/challenges?lon=...&lat=...`).
  - La **validation des défis** par soumission d'une preuve (`POST /api/challenges/{id}/validate`).

## Phase 1 - Un monolithe pour le MVP

Exercice :

- a) Proposer un **diagramme des cas d'utilisation** pour décrire les fonctionnalités.
- b) Proposer un **diagramme de classes** pour le schéma de la base de données.
- c) Proposer un **diagramme de déploiement**.
- d) Identifier les avantages et inconvénients de cette architecture.
- e) (Bonus) Proposer des spécifications au format OpenAPI pour l'API.

## Phase 2 - Une architecture client/serveur pour le décollage !

Un influenceur (heureusement peu connu) parle de l'application ! Les utilisateurs commencent à affluer, la machine souffle, certaines requêtes tombent en erreur...

Toutefois, le début de croissance nous permet de vendre des QR codes à quelques commerçants, qui peuvent les placer en fond de boutique ou proposer de les scanner contre des menus.

Nous pouvons nous offrir un hébergement plus solide avec :

- Une machine dédiée pour le site.
- Une base de données gérée par un hébergeur (SaaS).

Exercice :

- a) Proposer un schéma de l'architecture.
- b) Identifier les avantages et inconvénients de cette architecture.

## Phase 3 - Bascule sur une architecture n-tiers

Nous avons enfin le budget pour développer une application mobile ! Nous décidons de préparer le terrain en décomposant l'application en modules avec :

- L'**application web** qui devient une SPA (Single Page Application).
- Le **backoffice** (`/admin`) qui reste une application statique.
- L'**API** qui devient indépendante.
- La **base de données**.

Nous mettrons ainsi à disposition l'**application web** sous forme de site web et d'application mobile.

Exercice :

- a) Identifier la fonctionnalité qui rendra ce changement difficile.
- b) Proposer un schéma de l'architecture.
- c) Identifier les avantages et inconvénients de cette architecture.

## Phase 4 - Passage au microservice pour exploiter CQRS avec les services clés

Avant le lancement de l'application mobile et de lancer une opération de communication, nous devons nous assurer que notre application tiendra la charge.

Or, la base de données continue de souffrir et nous remarquons que :

- Nous payons une base de données avec des répliques en lecture seule qui ne sont pas utilisées !
- La fonctionnalité la plus sollicitée est la **recherche des défis**, qui peut exploiter une réplique en lecture seule !

Nous décidons donc de décomposer l'API en microservices avec :

- Un **service de recherche des défis** exploitant une connexion en lecture seule.
- Un **service de validation des défis** exploitant une connexion en lecture/écriture.

## Phase 5 - Passage en EDA pour bannir les tricheurs !

Nous lançons l'application mobile avec une opération de communication consistant à récompenser la résolution de défis !

Nous constatons que des petits malins manipulent la position de leur GPS pour résoudre les défis.

Pour les bannir, nous décidons de procéder comme suit :

- Nous ajoutons un système de gestion des événements (ex : Kafka).
- Pour chaque défi résolu, nous émettrons un événement avec l'identifiant de l'utilisateur, sa position et l'heure.
- Nous développons un service écoutant ces événements pour **calculer la vitesse de déplacement des utilisateurs** et **bannir ceux qui se déplacent trop rapidement**.

Exercice :

- a) Proposer un schéma de l'architecture.
- b) Identifier les avantages et inconvénients de cette architecture.
