---
theme: marp-ensg
paginate: true
footer: <a href="https://github.com/mborne/cours-archi-sig" target="_blank">Introduction à l'architecture des SI</a> - octobre 2024
header: '<div><img src="img/logo-ensg.png" alt="ENSG" height="64px"/></div>'
---


# Introduction à l'architecture des SI

- [Introduction](#introduction)
- [Les principaux défis](#les-principaux-défis)
- [Les principes d'architecture](#les-principes-darchitecture)
- [Les styles d'architecture](#les-styles-darchitecture)
- [Les spécificités liées aux données géographiques](#les-spécificités-liées-aux-données-géographiques)
- [Les infrastructures de données géographiques](#les-infrastructures-de-données-géographiques)

---

## Introduction

### Définition d'un SI

Selon [fr.wikipedia.org](https://fr.wikipedia.org/wiki/Syst%C3%A8me_d%27information) :

> Le **système d'information (SI)** est un ensemble organisé de ressources qui permet de collecter, stocker, traiter et distribuer de l'information, en général grâce à un réseau d'ordinateurs.


Le SI se décompose en un **système organisationnel** et un **système technique** : Le **système informatique** (le matériel informatique, les logiciels, les données, les services, les réseaux,...)

---

## Introduction

### Plusieurs types de SI

Nous trouverons plusieurs types de systèmes d'information :

- Des **systèmes de traitement des transactions (TPS)** pour gérer les ventes, les paiements,...
- Des **Systèmes d'Information des Ressources Humaines (SIRH)** pour gérer les abscences, les paies, les recrutements... 
- Des **Système d'entreprise ou ERP (Enterprise Resource Planning)** pour gérer les processus et les ressources
- Des **Système d'aide à la décision** qui s'appuie sur des analyses de données internes ou externes
- ...

---

## Introduction

### Le système d'information géographique (SIG)

Le SIG sera un type de SI se focalisant sur la composante spatiale des données :

> "Un **système d'information géographique ou SIG** est un système d'information conçu pour recueillir, stocker, traiter, analyser, gérer et présenter tous les types de données spatiales et géographiques"

Source : [fr.wikipedia.org - Système d'information géographique](https://fr.wikipedia.org/wiki/Syst%C3%A8me_d%27information_g%C3%A9ographique)

Pour cette introduction à l'architecture des SI :

- Nous nous concentrerons sur l'architecture des SI avec une forte composante spatiale.
- Nous remarquerons que la composante spatiale peut être exploitée dans d'autres types de SI (ex : cartographie dans un système d'aide à la décision). 

---

## Les principaux défis

### L'hétérogénéité des acteurs

La conception d'une architecture devra prendre en compte :

- Les **clients** (internes ou externes)
- Le(s) **métier**(s)
- La **sécurité**
- La **politique** de l'organisation
- ...

Or, ces acteurs auront souvent des objectifs divergents.

---

## Les principaux défis

### Documenter l'architecture (1/2)

Il sera important de **documenter l'architecture** tant sur le plan **logique** que **technique**. Nous pouvons pour ce faire nous appuyer sur :

- Les **diagrammes UML de composants** pour décrire l'architecture logique et les interfaces.
- Les **diagrammes UML de déploiement** pour décrire l'architecture technique.

---

## Les principaux défis

### Documenter l'architecture (2/2)

Nous soulignerons toutefois que :

- **Présenter le bon niveau de détail aux différents acteurs ne sera pas évident** (d'où des approches telles [C4 model](https://c4model.com))
- Des libertés seront souvent prises par rapport au formalisme UML.

---

## Les principaux défis

### Documenter précisément les interfaces

Il conviendra de documenter précisément les interfaces. Nous systématiserons par exemple la rédaction de spécification au format [OpenAPI](https://swagger.io/specification/) pour les API REST/JSON.

---

## Les principaux défis

### Gouverner sans bloquer l'innovation

La nécessité d'**assurer la cohérence** et de **rationnaliser** induira un besoin de standardisation.

Toutefois, **imposer un cadre technique précis et figé** induira un **risque de blocage de l'innovation**. A ce titre, il sera intéressant de :

- Décrire le cadre technique (sans le figer)
- Poser un cadre pour gérer les évolutions (ex : [Architecture Decision Record (ADR)](https://blog.octo.com/architecture-decision-record))
- Poser un cadre permettant de cartographier dynamiquement le SI  (voir [backstage de spotify et son métamodèle](https://backstage.io/docs/features/software-catalog/descriptor-format))

---

## Les principaux défis

### Faire communiquer efficacement les services

La recherche d'une communication efficace entre les services se retrouve dans l'évolution des formats et protocoles au niveau des services web :

* Fin des années 90, le **format XML** domine avec **WSDL** (Web Services Description Language) et **SOAP** (Simple Object Access Protocol).
* Depuis 2000, le **format JSON** gagne du terrain dans les API REST.
* 2011, [WebSocket](https://fr.wikipedia.org/wiki/WebSocket) permettant une communication bidirectionnelle.
* 2012, [GraphQL](https://graphql.org/) limitant le nombre de requêtes par rapport aux API REST.
* 2015, gRPC s'appuyant sur le **format [Protocol Buffers](https://protobuf.dev/)** et HTTP/2 avec une communication bidirectionnelle en temps réel.

---

## Les principes d'architecture

### Séparation des préoccupations (*Separation of Concerns*)

A l'échelle du système, **chaque composant doit avoir une responsabilité claire et unique**.

> Nous retrouvons ce principe en P.O.O. dans le S de SOLID avec le **principe de responsabilité unique (*Single responsibility principle*)**.

---

## Les principes d'architecture

### Modularité

En corrolaire du point précédent, le système est décomposé en plusieurs modules indépendants qui peuvent être développés, testés et maintenus séparément.

---

## Les principes d'architecture

### Abstraction

L'abstraction est un processus consistant à se concentrer sur les caractéristisques essentielles d'un composant ou d'un système en ignorant les détails.

Nous la retrouverons sous plusieurs formes à l'échelle d'un SI en considérant :

- Les différentes **couches d'un système** (interface graphique, logique métier, persistence des données)
- Les **services** composant ce système.
- Les **classes et interfaces** d'un composant.

---

## Les principes d'architecture

### Encapsulation

Les détails internes d'un module doivent être cachés aux autres modules. Les interactions entre modules se font uniquement via des interfaces bien définies. 

---

## Les principes d'architecture

### Couplage faible

Les modules doivent être aussi indépendants que possible les uns des autres. Un **couplage faible** facilite la **modification ou le remplacement de modules** sans affecter les autres parties du système.

> NB : Le couplage prendra plusieurs formes (couplage par message ou événement, couplage par interface, couplage par données, couplage par contrôle, couplage temporel...)

---

## Les principes d'architecture

### Cohésion forte

> TODO : reformuler

Les composants d'un module doivent être liés et centrés sur une tâche spécifique. Cela rend le module plus compréhensible et maintenable.

---

## Les principes d'architecture

### Réutilisabilité

> TODO : reformuler

Encourager la création de composants réutilisables permet d'optimiser le développement et d'améliorer la qualité du SI en réduisant les redondances de code.

---

## Les principes d'architecture

### Scalabilité

> TODO : reformuler

L'architecture doit être conçue pour supporter la montée en charge (scalabilité horizontale ou verticale) afin que le système puisse évoluer en fonction des besoins (évolution du nombre des appels de service, évolution du volume des données,...).

---

## Les principes d'architecture

### Interopérabilité

> TODO : reformuler

Les composants doivent être capables de communiquer entre eux, même s'ils proviennent de systèmes différents.

---

## Les principes d'architecture

### Conformité aux normes

Respecter les standards et bonnes pratiques de l’industrie (comme les architectures REST, SOA, ou microservices) facilitera l'**interopérabilité**, la **réutilisation**, et la **maintenabilité**.

---

## Les principes d'architecture

### Résilience et tolérance aux pannes

Le système doit être conçu pour continuer à fonctionner (ou se dégrader de façon contrôlée) en cas de défaillance d’un ou plusieurs composants.

---

## Les principes d'architecture

### Évolutivité

L'architecture doit permettre des évolutions futures sans remettre en cause l'ensemble du système, en utilisant des principes comme le versionnage des APIs ou l'intégration continue.

---

## Les principes d'architecture

### Portabilité

Les composants doivent être capables de fonctionner dans différents environnements (ex. cloud, on-premise) sans nécessiter de modifications majeures.

---

## Les principes d'architecture

### Observabilité

Le système doit être instrumenté pour permettre l'identification et résolution rapide des problèmes.


---

### Intégrer la sécurité dans la conception

L’architecture doit intégrer la sécurité dès la conception. Par exemple, l'approche [*secure by design*](https://www.oracle.com/fr/security/secure-by-design/) invite entre particulier à :

- **Minimiser la surface d'attaque**
- Appliquer le **principe de moindre privilège** (i.e. prévoir des mécanismes d'authenfication et d'autorisation)
- Adopter une **stratégie de défense en profondeur**
- Prendre des précautions vis-à-vis des services tiers


---

## Les styles d'architecture

> Remplace "Architectures client/serveur multi-tiers / API/ ServiceWeb"

* Architecture client/serveur (ex : QGIS + PostgreSQL)
* Architecture n-tiers (ex : WAF -> LB -> API -> BDD)
* Architecture monolithique (ex : GeoServer?)
* Architecture orientée services (SOA) (standards OGC, api.gouv.fr,...) 
* Architecture microservices (ex : GeoServer cloud)
* Event-Driven Architecture (ex : orchestrateur GéoPlateforme)
* Serverless Architecture (microservice + EDA)

---

## Les spécificités liées aux données géographiques

* La diversité des données (images, nuages de points, données vectorielles, métadonnées...)
* Le volume des données
* Les standards dédiés (INSPIRE, CNIG, OCG,...)
* Les formats et services spécifiques

> (GML, GeoJSON, métadonnées ISO 19115...) + (WMS, WMTS/TMS,...)

> "Spatial is not special" mais les formats ont tendances à mettre la géométrie sur un piédestal (feature GML / feature GeoJSON vs sérialisation des géométrie en XML / JSON).

* La diversité des acteurs (collaboratif (OSM), institutions (INSEE, IGN, collectivités,...), entreprises (Google Maps, LaPoste,...),...)
* La diversité des modes de production des données (centralisée vs décentralisée)
  * La validation et d'agrégation des données (GéoPortail de l'Urbanisme, BAN,...)
  * La gestion des identifiants (avec des objets qui fusionnent ou que l'on découpe)

* Une asymétrie entre la production et la consommation des données (-> CQRS)
* Des services de calcul gourmand en ressources (calcul géométrique, rendu cartographique, calcul d'itinéraire et d'isochrone,...)

---

## Les infrastructures de données géographiques

> Reprend : "Les infrastructures des données géographiques (IDG) (Infrastructure de Données Spatiale - IDS)" et
> "Rôle et place des SIG dans les organisations"

* Définition


« Une infrastructure de données géographiques est une structure de mutualisation, d’échange et de diffusion de données géographiques à l’échelle d’un territoire et au bénéfice d’acteurs publics, et indirectement des citoyens. », Source : Afigeo

