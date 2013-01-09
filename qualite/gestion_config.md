Gestion de configurations
========


Contrôle des modifications
------

La plateforme de gestion des documents choisie est GIT. Ainsi, les fonctionnalités suivantes sont disponibles nativement
- Gestion de l'historique, avec un traçage du responsable, de la date, de la description des changements, etc
- Visualisation des modifications entre différentes versions
- Récupération de versions précédentes
- etc.

En parallèle, une identification des versions significative est faite grâce à un [document tableur](https://docs.google.com/spreadsheet/ccc?key=0AsECmMGkrcOvdEg2aWI0RzZZYXBHeXBxN2tIbU9iS3c#gid=0).
Ainsi, à chaque versions significative, les informations suivantes doivent être renseignées:
- Nom du document
- Numéro de version
- Date
- Identifiant de commit
- Responsable


Conventions d'identification
---------

L'attribution des numéros de version se fait sous la supervision du Responsable Qualité, après validation du document.
Chaque document, à sa création, a pour version 0.1
La numéro de version majeure du document est incrémentée à la validation du document en prévision d'une présentation au client, ou lorsqu'un objectif majeur est atteint.
Les changements intermédaires (travail d'une séance par ex) incrémentent le numéro de version mineure.


Livraison des articles de configuration
----

A chaque livraison, le document de [traçage des livraisons](https://docs.google.com/spreadsheet/ccc?key=0AsECmMGkrcOvdEg2aWI0RzZZYXBHeXBxN2tIbU9iS3c#gid=1) doit être mis à jour.
Il associe à chaque livraison la liste des documents concernés et leur version respective