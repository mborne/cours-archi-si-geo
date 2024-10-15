
# API REST

## Définition

**REST (Representational State Transfer)**  est un **style architecture** proposé par **Roy Fielding** en 2000 dans sa thèse pour construire des API sur la base des standards du WEB (principalement **HTTP**).

## Points clés

- Approche **client/serveur** et **stateless** (chaque requête contient toutes informations nécessaires)
- Utilisation des verbes HTTP :
  - **GET** pour récupérer une ressource (ex : `GET /api/users/{id}`) ou une collection de ressources (ex : `GET /api/users`)
  - **POST** pour créer une nouvelle ressource (ex : `POST /api/users`)
  - **PUT** pour mettre à jour une ressource existante (ex : `PUT /api/users/{id}`)
  - **DELETE** pour supprimer une ressource (ex : `DELETE /api/users/{id}`)
- Utilisation des **entêtes HTTP** en complément par exemple pour la **gestion du cache**

## Avantages de REST

- **Simplicité** (HTTP)
- **Interopérabilité** (HTTP)
- **Scalabilité** (stateless)

## Ressources

* [blog.octo.com - Designer une API REST](https://blog.octo.com/designer-une-api-rest)
