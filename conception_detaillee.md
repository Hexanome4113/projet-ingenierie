Conception détaillée
====================


1. Présentation du sous-système choisi
--------------------------------------

Dans notre solution, une part importante du travail effectué par le système embarqué est la détermination du moment auquel envoyer les mesures des capteurs au site central, ainsi que l'envoi en lui même de ces mesures.

L'objet de ce document est de détailler le sous-système en charge de ces tâches, intitulé : « Prise en charge des données capteurs par le système embarqué d'un site isolé », jusqu'à aboutir à une spécification logicielle globale.


### a. Périmètre du sous-système ###

#### Ce qui n'est pas réalisé par le sous-système ####

Le sous-système étudié ne s'occupe pas de l'unification des données reçues à l'entrée du microcontrôleur. En effet, comme ces données ne sont pas toutes obtenues par le système embarqué de la même façon, elles ne contiennent pas les mêmes informations.

Les données brutes, reçues par le système embarqué, sont hétérogènes sur deux aspects :

1.  Les données peuvent provenir directement des capteurs reliés par une connexion filaire au système embarqué. Ces données ne comportent alors qu'une mesure, celle du capteur relié au microcontrôleur.

    En revanche, dans le cas de la connexion par ondes radios, un autre microcontrôleur agrège les mesures de tous les capteurs de la cuve, avant de les transmettre en une fois au système embarqué.

    Dans ce cas, la donnée transmise contient plusieurs mesures. La première différence entre les données se situe donc au niveau du nombre de mesures par données reçues.

2.  La nature même des données reçues (indépendamment du nombre de mesures qu'elles contiennent) est différente, suivant que la donnée provienne directement d'un capteur ou soit passée entre temps par un microcontrôleur sur la cuve (pour la transmission par radio).

    Dans le premier cas, le capteur ne fournit le plus souvent qu'une représentation codée de la valeur mesurée (cas d'un capteur à sortie numérique). Aucune autre information (identifiant du capteur, heure de la prise de mesure, etc.) n'est alors présente dans la donnée reçue. Les capteurs peuvent même fournir une grandeur analogique, corrélée à la grandeur physique qu'ils mesurent, que le microcontrôleur du site central doit alors avant toute autre chose numériser.

    Dans le second cas, les données envoyées par ondes radios contiennent déjà toutes les informations utiles pour chaque mesure (identificateur du capteur ayant fourni la mesure, modèle du capteur, etc.).

Il existe donc un sous-système de pré-traitement des mesures, qui ne sera pas détaillé, dont le rôle est de masquer ces différences afin de fournir des données homogènes en entrée du sous-système étudié (voir figure ci-dessous).

![Figure manquante — Sous-systèmes en lien avec le sous-système détaillé](../../raw/master/images/AdvancedConception/sous-systemes-en-lien-avec-le-sous-systeme-detaille.png "Sous-systèmes en lien avec le sous-système détaillé")

La nature exacte de ces données d'entrée est détaillée au paragraphe [b. Données à l'entrée du sous-système](#b-donn%C3%A9es-%C3%A0-lentr%C3%A9e-du-sous-syst%C3%A8me).


#### Ce qui est réalisé par le sous-système ####

Le but du sous-système est de déterminer les transmissions à effectuer vers le site central. En analysant les mesures reçues, et en les comparant à une valeur de référence, le sous-système décide s'il doit immédiatement entamer une transmission.

Dans tous les cas, le système transmet la dernière mesure qu'il a obtenu de chaque capteur toutes les 24 heures.

En plus de déterminer quand il doit envoyer les mesures des capteurs, le sous-système supervise également cet envoi. La transmission des mesures a lieu via le système de transmission satellite. En cas d'échec (si la connexion n'est pas disponible, ou si le transfert échoue), le sous-système doit assurer la sauvegarde des données de la transmission, afin de pouvoir les retransmettre une fois la situation rétablie.


### b. Données à l'entrée du sous-système ###

Comme il a été dit précédemment, un sous-système en amont de celui-ci se charge d'effacer les différences entre les différentes données reçues par le système embarqué (voir à ce propos le paragraphe [Ce qui n'est pas réalisé par le sous-système](#ce-qui-nest-pas-r%C3%A9alis%C3%A9-par-le-sous-syst%C3%A8me)).

Le sous-système de prise en charge des données capteurs n'a donc à faire qu'à des données homogènes, chaque donnée contenant une et une seule mesure (provenant d'un capteur bien identifié).

Les données exploitées en entrée par ce sous-système sont donc composées :

- de l'identifiant du capteur qui a fourni cette mesure ;
- du numéro de modèle du capteur ;
- du type de mesure (mesure de pH, de température ou de niveau) ;
- d'un horodatage correspondant à l'heure où la prise de mesure a été effectuée ;
- et enfin, de la valeur pré-traitée, déduite la grandeur transmise par le capteur (par exemple, la conversion de 42 sur une échelle linéaire de valeurs entières, codée entre 0 et 255, pour des valeurs de pH allant de 2 à 14, c'est-à-dire 3,98).


### c. Organisation de la mémoire externe ###

Pour assurer un fonctionnement optimal, y compris en cas d'impossibilité de transmettre les mesures des capteurs, ce sous-système a besoin de stocker des données en mémoire. C'est pour cette raison que, dans notre solution, une mémoire externe vient en complément du microcontrôleur composant le système embarqué.

Cette mémoire est partagée en plusieurs zones distinctes. Chaque zone a pour rôle le stockage d'un type d'information bien défini :

- Zone 1 (notée _Z1_) : pour chaque capteur du site isolé, de la mémoire est réservée dans cette zone pour contenir un écart maximum toléré entre la valeur de référence et les valeurs mesurées ;
- Zone 2 (notée _Z2_) : pour chaque capteur du site isolé, de la mémoire est réservée dans cette zone pour contenir une valeur de référence ;
- Zone 3 (notée _Z3_) : pour chaque capteur du site isolé, de la mémoire est réservée dans cette zone pour contenir la dernière valeur mesurée ;
- Zone 4 (notée _Z4_) : pour chaque transmission en attente, de la mémoire est réservée dans cette zone pour contenir les infos qu'il est prévu de transmettre.

Les notations _Z1_ à _Z4_ seront utilisées par la suite pour se rapporter à ces zones de la mémoire externe.


### d. Aperçu du fonctionnement du sous-système ###

Le processus suivant donne une vue logique du fonctionnement du sous-système. Cette description textuelle vient en complément des diagrammes qui suivent, dans le but d'en faciliter la compréhension. La même notation (_C_ pour le capteur type et _D_ pour la donnée reçue de ce capteur) est utilisée dans les diagrammes qui s'y prêtent.

> -   À la réception d'une donnée _D_, provenant du capteur _C_ :
>    -   Enregistrer _D_ en tant que dernière donnée reçue pour _C_, dans _Z3_.
>    -   Si la donnée de référence pour _C_ date de plus de 1 jour __ou__ si _D_ est très éloignée de la donnée de référence (écart supérieur à l'écart maximum toléré, trouvé dans _Z1_) :
>        -   Mettre à jour la donnée de référence de tous les capteurs avec leur dernière donnée reçue, dans _Z2_.
>        -   Préparer une transmission de la dernière donnée reçue de tous les capteurs, dans _Z4_.
>    -   Sinon :
>        -   Rien à faire.
>-   Lorsqu'une transmission est prête :
>    -   Lire les données de transmission dans _Z4_.
>    -   Si la connexion satellitaire est opérationnelle :
>        -   Transmettre les données.
>            -   Si la transmission réussie :
>                -   Supprimer les données de transmission de _Z4_.
>            -   Sinon :
>                -   Rien à faire.
>    -   Sinon :
>        -   Rien à faire.
>-   Dès que la connexion satellitaire est de nouveau opérationnelle (si elle ne l'était plus), retenter les transmission prêtes.

Afin de détailler le fonctionnement du sous-système, plusieurs diagrammes sont présentés ci-après :

- un découpage en classe logicielle du sous-système est proposé à la partie [2. Diagramme de classes](#2-diagramme-de-classes) ;
- plusieurs diagrammes présentes les différents états et les activités des composants du sous-système [3. Diagrammes d'états et d'activités](#3-diagrammes-d%C3%A9tats-et-dactivit%C3%A9s) ;
- plusieurs diagrammes de communication montre également comment ces classes interopèrent [4. Diagrammes de communication](#4-diagrammes-de-communication).


2. Diagramme de classes
-----------------------

![Figure manquante — Diagramme de classes du sous-système de prise en charge des données capteurs](../../raw/master/images/AdvancedConception/diagramme-de-classes.png "Diagramme de classes du sous-système de prise en charge des données capteurs")


3. Diagrammes d'états et d'activités
------------------------------------

Présentation des différents états, diagramme de transitions

![Figure manquante — Diagramme d'activité : après réception d'une mesure](../../raw/master/images/AdvancedConception/da-apres-receptin-d-une-mesure.png "Diagramme d'activité : après réception d'une mesure")

![Figure manquante — Diagramme d'activité : transmission](../../raw/master/images/AdvancedConception/da-transmission.png "Diagramme d'activité : transmission")

![Figure manquante — Diagramme d'état : transmission](../../raw/master/images/AdvancedConception/de-transmission.png "Diagramme d'état : transmission")

![Figure manquante — Diagramme d'état : modem](../../raw/master/images/AdvancedConception/de-modem.png "Diagramme d'état : modem")


4. Diagrammes de communication
------------------------------
Collecte d'informations, divers tests, envoi

![Figure manquante — Diagramme de communication : enregistrement d'une mesure](../../raw/master/images/AdvancedConception/dc-enregistrement-d-une-mesure.png "Diagramme de communication : enregistrement d'une mesure")

![Figure manquante — Diagramme de communication : transmission](../../raw/master/images/AdvancedConception/dc-transmission.png "Diagramme de communication : transmission")


5. Validation croisée
---------------------
