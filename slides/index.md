# Introduction à l'architecture des SI

Adaptation de l'ancien plan :

* [x] Définitions d’un SI
* [x] Architectures client/serveur multi-tiers / API/ ServiceWeb
* [x] Conception d’une architecture en utilisant les diagrammes UML : composants et déploiement
* [x] Rôle et place des SIG dans les organisations
* [x] Les infrastructures des données géographiques - IDG (Infrastructure de Données Spatiale - IDS)
* [ ] ~~Les spécificités d'un projet de SIG et les acteurs des SIG en entreprise~~

## Introduction

> Remplace "Définitions d’un SI"

* Définition d'un SI
* Exigences fonctionnelles vs non fonctionnelles.
* Les objectifs (maintenabilité, évolutivité, résilience,...)
* Les principes fondamentaux (Separation of Concerns, Modularité, Encapsulation,...)

## Les principaux défis

> Intègre "Conception d’une architecture en utilisant les diagrammes UML : composants et déploiement"

* Hétérogénéité des acteurs (les clients, les métiers, la sécurité, la politique,...)
* Documenter l'architecture (UML, C4 Model,...) et les API (OpenAPI)
* Gouverner sans bloquer l'innovation (ex : décrire le cadre technique, faire des choix (ADR),...)
* Cartographier une architecture dynamique (ex : backstage de spotify)
* Assurer la cohérence à l'échelle du SI (standardisation des API, cas de [api.gouv.fr](https://api.gouv.fr/rechercher-api),...)
* Faire communiquer efficacement les services
 * Les protocoles et les formats : SOAP/XML (WFS, WMS, WMTS,...), REST/JSON (OGC API), gRPC (HTTP/2 + Protocol Buffers)
 * L'authentification (compte utilisateurs vs compte de service, token, JWT,...)

## Les styles d'architecture

> Remplace "Architectures client/serveur multi-tiers / API/ ServiceWeb"

* Architecture client/serveur (ex : QGIS + PostgreSQL)
* Architecture n-tiers (ex : WAF -> LB -> API -> BDD)
* Architecture monolithique (ex : GeoServer?)
* Architecture orientée services (SOA) (standards OGC, api.gouv.fr,...) 
* Architecture microservices (ex : GeoServer cloud)
* Event-Driven Architecture (ex : orchestrateur GéoPlateforme)
* Serverless Architecture (microservice + EDA)

## Les spécificités liées aux données géographiques

* La diversité (images, nuages de points, données vectorielles, métadonnées...) et le volume des données
* Les standards dédiés (INSPIRE, CNIG, OCG,...)
* Les formats (GML, GeoJSON, métadonnées ISO 19115...) et services (WMS, WMTS/TMS,...) spécifiques

> "Spatial is not special" mais les formats ont tendances à mettre la géométrie sur un piédestal (feature GML / feature GeoJSON vs sérialisation des géométrie en XML / JSON).

* La diversité des acteurs (collaboratif (OSM), institutions (INSEE, IGN, collectivités,...), entreprises (Google Maps, LaPoste,...),...)
* La diversité des modes de production des données (centralisée vs décentralisée)
  * La validation et d'agrégation des données (GéoPortail de l'Urbanisme, BAN,...)
  * La gestion des identifiants (avec des objets qui fusionnent ou que l'on découpe)

* Une asymétrie entre la production et la consommation des données (-> CQRS)
* Des services de calcul gourmand en ressources (calcul géométrique, rendu cartographique, calcul d'itinéraire et d'isochrone,...)

## Les infrastructures de données géographiques

> Reprend : "Les infrastructures des données géographiques (IDG) (Infrastructure de Données Spatiale - IDS)" et
> "Rôle et place des SIG dans les organisations"

* Définition

« Une infrastructure de données géographiques est une structure de mutualisation, d’échange et de diffusion de données géographiques à l’échelle d’un territoire et au bénéfice d’acteurs publics, et indirectement des citoyens. », Source : Afigeo

