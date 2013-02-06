Conception détaillée
====================


1. Présentation du sous-système choisi
--------------------------------------

Dans notre solution, une part importante du travail effectué par le système embarqué est la détermination du moment auquel envoyer les mesures des capteurs au site central, ainsi que l'envoi en lui même de ces mesures.

L'objet de ce document est de détailler le sous-système en charge de ces tâches, intitulé&nbsp;: «&nbsp;Prise en charge des données capteurs par le système embarqué d'un site isolé&nbsp;», jusqu'à aboutir à une spécification logicielle globale.


### a. Périmètre du sous-système ###

#### Ce qui n'est pas réalisé par le sous-système ####

Le sous-système étudié ne s'occupe pas de l'unification des données reçues à l'entrée du microcontrôleur. En effet, comme ces données ne sont pas toutes obtenues par le système embarqué de la même façon, elles ne contiennent pas les mêmes informations.

Les données brutes, reçues par le système embarqué, sont hétérogènes sur deux aspects :

1. Les données peuvent provenir directement des capteurs reliés par une connexion filaire au système embarqué. Ces données ne comportent alors qu'une mesure, celle du capteur relié au microcontrôleur.  
En revanche, dans le cas de la connexion par ondes radios, un autre microcontrôleur agrège les mesures de tous les capteurs de la cuve, avant de les transmettre en une fois au système embarqué.  
Dans ce cas, la donnée transmise contient plusieurs mesures. La première différence entre les données se situe donc au niveau du nombre de mesures par données reçues.

2. La nature même des données reçues (indépendamment du nombre de mesures qu'elles contiennent) est différente, suivant que la donnée provienne directement d'un capteur ou soit passée entre temps par un microcontrôleur sur la cuve (pour la transmission par radio).  
Dans le premier cas, le capteur ne fournit le plus souvent qu'une représentation codée de la valeur mesurée (cas d'un capteur à sortie numérique). Aucune autre information (identifiant du capteur, heure de la prise de mesure, etc.) n'est alors présente dans la donnée reçue. Les capteurs peuvent même fournir une grandeur analogique, corrélée à la grandeur physique qu'ils mesurent, que le microcontrôleur du site central doit alors avant toute autre chose numériser.  
Dans le second cas, les données envoyées par ondes radios contiennent déjà toutes les informations utiles pour chaque mesure (identificateur du capteur ayant fourni la mesure, modèle du capteur, etc.).

Il existe donc un sous-système de pré-traitement des mesures, qui ne sera pas détaillé, dont le rôle est de masquer ces différences afin de fournir des données homogènes en entrée du sous-système étudié (voir figure ci-dessous).

![Figure&nbsp;: Sous-systèmes en lien avec le sous-système détaillé](../../raw/master/images/AdvancedConception/sous-systemes-en-lien-avec-le-sous-systeme-detaille.png "Sous-systèmes en lien avec le sous-système détaillé")

La nature exacte de ces données d'entrée est détaillée au paragraphe [b. Données à l'entrée du sous-système](#b-donnees-a-l-entree-du-sous-systeme).


#### Ce qui est réalisé par le sous-système ####

Le but du sous-système est de déterminer les transmissions à effectuer vers le site central. En analysant les mesures reçues, et en les comparant à une valeur de référence, le sous-système décide s'il doit immédiatement entamer une transmission.

Dans tous les cas, le système transmet la dernière mesure qu'il a obtenu de chaque capteur toutes les 24 heures.

En plus de déterminer quand il doit envoyer les mesures des capteurs, le sous-système supervise également cet envoi. La transmission des mesures a lieu via le système de transmission satellite. En cas d'échec (si la connexion n'est pas disponible, ou si le transfert échoue), le sous-système doit assurer la sauvegarde des données de la transmission, afin de pouvoir les retransmettre une fois la situation rétablie.


### b. Données à l'entrée du sous-système ###

### c. Organisation de la mémoire externe ###

2. Diagramme de Classes
-----------------------


3. Etats et Transitions
-----------------------
Présentation des différents états, diag de transitions


4. Séquence de collecte de données
----------------------------------
Collecte d'informations, divers tests, envoi


5. Validation croisée
---------------------
