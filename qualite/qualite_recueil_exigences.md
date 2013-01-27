Procédure pour le contrôle qualité du recueil des exigences
=====

Analyse des exigences et décomposition du problème
---

Une exigence correspond à un problème, qui doit être compris et détaillé afin de pouvoir y apporter une solution complète et approprié. Pour cela, ce problème devra être décomposé en sous-problèmes de plus en plus simples. 

Le monde du problème est constitué de divers éléments physiques et humain appelés domaines du problème. Une machine interagit avec ces domaines afin de satisfaire une exigence. Lors de la résolution du problème, des modèles, représentant des objets virtuels, peuvent être introduits.

Les interactions entre les différents éléments du domaines doivent être définies au moyen d'interfaces. Celles-ci décrivent les actions possibles sur les éléments participant au lien.

### Formalisme ###
* Domaine du problème: Rectangle simple
* Exigence: Ellipse
* Machine: Rectangle avec trois barres à gauche.
* Modèle: Rectange avec deux barres à gauche.
* Interface: Lettre sur le lien entre deux éléments. Elle doit être détaillée en légende du schéma.

### Décomposition ###
Le coeur de l'analyse des exigences est la décomposition d'un problème en sous-problèmes. Chaque sous-problème doit expliquer un aspect du problème père. Ils doivent donc être plus simples et être constitués d'éléments appartenant au domaine du problème père.

On considère un problème simple lorsqu'il correspond aux critères suivants:
* Exigence unique: le problème correspond à un besoin élémentaire bien précis.
* Etat unique: si des objets peuvent être dans plusieurs états (cas d'erreur par exemple) c'est que le problème doit être redivisé en un sous problème par état.
* Étape unique: Pour un processus se faisant en plusieurs étapes, chaque étape représente un problème qui doit être détaillé séparément. Un diagramme de séquence pourra permettre de visualiser le processus en entier.


### Design Patterns ###

#### 1. Introduction d'un modèle ####

[Introduction d'un modèle](http://github.com/404 "Introduction d'un modèle")


#### 2. Rupture ####

Une rupture se produit lorsqu'un élément du domaine peut changer d'état à la suite d'une séquence d'éléments imprévisibles. Lorsque c'est le cas, on utilise des diagrammes d'états pour visualiser les différentes possiblités. L'objectif est de pouvoir définir dans quelles conditions on se trouve en erreur, et comment en sortir.

[Rupture](http://github.com/404 "Rupture")


Procédure qualité
----------------

La procédure qualité aura pour objectif de vérifier que le recueil des exigences conserve les propriétés suivantes à travers tous les documents produits:
- Cohérence: Du point de vue des fonctionnalités, des objets introduits, mais aussi de la présentation
- Logique: Les différents documents et diagrammes doivent permettre de reconstituer le scénario logique ayant permis de les produire et d'arriver aux différentes conclusions. Ils doivent donc suivre un scénario évident.
- Clarté: Les documents doivent pouvoir être compris par le client et par des individus extérieurs au projet.
- Respect du formalisme et des règles de présentation
