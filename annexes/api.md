
# API

## Définition

Une **API (Application Programming Interface)** est comme son nom l'indique une interface permettant la communication entre deux programmes.

## Différents types d'API

Il existe plusieurs type d'API pour mettre à disposition une fonctionnalité :

- Une **bibliothèque de programmation** qui met à disposition une fonctionnalité sous forme d'une fonction ou d'une classe.
- Une **API WEB** (ex : [API REST](rest.md)) qui met à disposition une fonctionnalité via le réseau en HTTP.
- Une **API CLI (Command Line Interface)** pour l'accès à une fonctionnalité en ligne de commande.

## Complémentarité des types d'API

Chaque type d'API possède ses avantages et inconvénients :

|                 |        **Bibliothèque**         |                  **API CLI**                  |     **API WEB**      |
| --------------- | :-----------------------------: | :-------------------------------------------: | :------------------: |
| **Mise à jour** |      À traiter côté client      |             À traiter côté client             |   **Centralisée**    |
| **Cible**       |      Développeur (backend)      |    Technicien, orchestrateur de traitement    | Développeur (front)  |
| **Performance** |     Souplesse d'utilisation     | Fichier temporaire si chaînage de traitements | **Transfert réseau** |
| **Portabilité** | Langage de programmation imposé |       éventuellement dépendance à l'OS        |   **accès réseau**   |

## Une approche complète possible

Il est possible de **mettre à disposition une fonctionnalité sous les trois formes** pour laisser le choix à l'utilisateur en fonction de son cas d'utilisation.

A titre d'exemple, pour [Mapshaper](https://github.com/mbloch/mapshaper) qui offre une fonctionnalité de simplification des géométries, nous trouvons :

- Un service web ( https://mapshaper.org/ )
- Un exécutable en ligne de commande (c.f. [mapshaper - Command line tools](https://github.com/mbloch/mapshaper?tab=readme-ov-file#command-line-tools))
- Un bibliothèque JavaScript (c.f. [npmjs - mapshaper](https://www.npmjs.com/package/mapshaper))

NB : Nous ne coupons pas à développement de cette dernière que nous ciblions une API WEB ou une API CLI.


