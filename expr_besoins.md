Recueil des exigences
======================

Après une étude de l'appel d'offre présenté nous avons défini un recueil des exigences en réfléchissant également aux problèmes qui pourraient survenir.
Le schéma ci-dessous est un premier découpage, plutot évident, du problème. Notre travail va commencer par s'attarder sur les premières interfaces mises à jour, puis nous approfondirons petit à petit notre approche.
#### Découpage grossier du problème ####
![schéma général](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/schemaGeneral.png "schéma général")

A. Communication entre le système embarqué du site distant et le serveur central
--------------------------------------------------------------------------------
Le coeur du problème est le suivant: supposons que nous possédons des données sur l'état d'un site ( nous verrons un peu plus tard d'où nous vient cette connaissance ) et que nous souhaitons les transmettre à une autre unité distante : le cite central. Cette communication doit répondre à des exigences de qualité et de fiabilité. Par ailleurs, la communication de commandes remontant du site central jusqu'à des actionneurs devra être envisagée au moyen du même dispositif.

Si la connexion vers le site centrale est défaillante, le système embarqué du site distant doit déclencher une procédure de sauvegarde locale des données.
#### Sauver des données ####
![sauver données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/sauvegarde-locale.png "sauvegarde locale" )


Lorsque la connexion est rétablie ( ou réparée ) le système embarqué doit envoyer les données qu'il a sauvegardé. Ainsi malgré l'incident, il est possible d'avoir un suivi continu de l'acquisition des données.
#### Transmettre des données ####
 ![transmettre données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/transmettre-donnee.png "transmettre donnees" )
 
 
Que se passe-t-il en cas de non réception de données sur le site central ?
D'où vient le problème ? Perte de connexion ? Capteur défectueux ? Système embarqué du site distant défaillant ?

Si le capteur est défectueux, le site central reçoit tout de même les autres informations liées au site. Il s'agit donc de lever l'alerte adaptée au problème.

Qu'en est-il de la distinction entre une perte de connexion et un système embarqué du site distant défaillant? On ne peut pas décider sans plus d'information, il faut donc lever l'alerte correspondant au niveau de gravité le plus élevé : panne du système embarqué lui même. En effet, en cas de perte de connexion les données sont sauvergardées localement par le site isolé puis envoyées dès la connexion rétablie. De plus il faut lever une alerte selon d'autres facteurs : le dernier état connu des capteurs, la criticité du site et la durée de "non réponse" du site.

Enfin, nous travaillons pour des sites dans le nord de la Norvège, ce qui implique des conditions climatiques particulières ( autour des -40°C en hiver ). Il est important de surveiller la résistance des appareils du système au froid où d'y ajouter un dispositif permettant de les isoler.

B. Acquisition des données et communication entre les capteurs et le système embarqué du site distant
--------------------------------------------------------------------------
Nous avions jusqu'à présent des informations à transmettre au site central. Il s'agit de savoir comment ces données ont été collectées et comment elles ont été transmises au système embarqué du site isolé. Il y a une nécessité de connecter les capteurs de manière fiable, car, comme nous l'avons vu précédemment, l'absence de donnée est considérée comme une défaillance et entraîne une maintenance.
#### Modélisation de la contrainte de distance ####
![contrainte de distance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/distance.png "contrainte de distance")

Les sites ont des tailles différentes, superficies allant d'une centaine de mètres de diamètre jusqu'à un kilomètre de diamètre, la solution doit prendre en compte ces contraintes. Doit-on proposer une solution générique, en adapter plusieurs selon la taille des sites? Il faut aussi tenir compte de la topologie des sites : notre solution convient-elle à un site escarpé (installation, possibilité d'émettre des ondes, ...)?

La fréquence de ces acquisitions est aussi une question intéressante. Actuellement, les sites sont vérifiés ponctuellement, voir rarement, par le propriétaire. L'absence de suivi régulier entraîne des accidents révélés trop tard qui se révèlent fort couteux. Cependant dans la majorité des cas tous se passe bien, bien que le relevé de données puisse être couteux en ressources, augmenter la complexité du système et aussi les coûts. Or, l'intérêt du système est son autonomie, si le système de monitoring demande le passage d'une société de maintenance tous les trois jours, on voit rapidement l'absurdité d'un tel système.

D'autrepart, concernant la journalisation des données, lorsque tout se passe bien, stocker des informations toutes les dix minutes semble aberrant.
Pourtant lorsqu'un problème survient la rapidité du système à détecter le problème et à transmettre l'information est primordiale ( surveillance de cuve de pétrole ou d'eau en cas de feu de forêt, fuite de liquide toxique,... ).

Nous avons déjà abordé la question du froid lors de la partie précédente, mais même si les appareils de mesure se situent dans les cuves, donc un peu moins exposés au froid, la question demeure lorsqu'il s'agit de leur système d'alimentation et de transmission de données. Si d'un point de vue financier envisager un investissement important pour chaque site pour protéger le système embarqué est envisageable, le choix de solution d'isolation coûteuses pour chaque cuve peut faire très vite trop grimper le prix.

Il s'agit de trouver un compromis intelligent entre autonomie et rapidité du système à détecter une faille.

C. Génération des demandes de maintenance
-----------------------------------------

### 1. Détermination du niveau de gravité de l'évènement et émission d'une alerte ###

Quelles sont les conditions de déclenchement d'une alerte ? Actuellement, c'est le propriétaire du site qui informe les sociétés de maintenance, on peut donc estimer qu'il peut toujours observer un problème sur le site et demander une intervention. La différence principale est, qu'en absence du propriétaire, les sites seront constamment surveillés par le biais de capteurs. C'est le remontée d'informations indiquant un état critique du paramètre observé qui déclenchera l'alerte. 
#### Gérer de la génération des problèmes ####
![DP - Gérer de la génération des problèmes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/LucidAlerte.png)
Les capteurs et les sites isolés doivent transmettre des informations recueillies et non les alertes elles-mêmes. En effet, le système doit être fiable, or si un site isolé tombe en panne, il ne peut plus signaler au site central une alerte indiquant son non-fonctionnement. Pour ces raisons plutôt évidentes, c'est le site central qui reçoit des informations, les traite et génere des alertes en conséquence. Un point particulier lié à un dysfonctionnement et à la perte d'information a déjà été développé précédemment.

####  Déterminer la gravité des problèmes ####
![DP - Déterminer la gravité des problèmes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/GestionAlertes.png)
Pour pouvoir classer les alertes selon leur gravité ( et ainsi pouvoir économiser des coûts de maintenance ), nous devons pouvoir établir différents niveaux de gravité. Qui peut connaître cette gravité ? Actuellement le propriétaire du site n'a pas forcément de connaissances sur son site, et il peut même parfois se tromper en indiquant à la société de maintenance des points peu importants ou oublier des points essentiels. La connaissance de ces sites est donc du côté des sociétés de maintenance. Avant de configurer notre système, il faudra réaliser une étude visant à mettre en commun leurs connaissances pour définir les criticités des situations.

Les alertes configurées seront enregistrées dans la base du site central et levées quand une donnée transmise dépasse le seuil fixé, ou quand une erreur matérielle ou de communication surgit. La création de ces alertes sera automatique, mais pourra auusi venir d'un traitement humain en aval.

#### Générer une alerte automatiquement ####
![DA - Générer une alerte automatiquement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20Alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20automatique.png "DA - Générer une alerte automatiquement")

#### Générer une alerte manuellement ####
![DA - Générer une alerte manuellement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20Alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20manuelle.png "DA - Générer une alerte manuellement")

Même si l'objectif de la solution proposée est de limiter les interventions humaines, il peut arriver que des alertes soient créées manuellement. C'est notamment le cas lorsque le directeur constate une anomalie ( soit dans les données transmises, soit parce qu'il s'est rendu sur place ) : il doit dans ce cas remplir un formulaire et le transmettre au site central où il sera étudié.

### 2. Optimisation des coûts de la maintenance ###

![01-Problème](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/DP-1.png "01 - Problème")
L'optimisation des coûts de la maintenance est l'une des exigences principales de ce projet. Elle se fait entre le moment où on reçoit une alerte et celui où une demande de maintenance est produite.

![02-Génération et journalisation](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/DP-2.png "02-Génération et journalisation")

Pour permettre de sécuriser le système et de retracer les actions effectuées, toute demande de maintenance doit être journalisée à sa création.

![03-Génération des demandes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/DP-3.png "03-Génération des demandes")

Pour éviter de demander des interventions lorsque cela n'est pas urgent, les alertes jugées mineures sont mises de côté pour chaque site tant qu'un nombre d'alertes mineures donné n'est pas atteint. Lorsque ce nombre est atteint ou qu'une alerte critique survient, une demande de maintenance est générée et prend en compte toutes les demandes non-traitées.

![04-Automate de déclenchement d'une demande](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/Automate.png "04-Automate de déclenchement d'une demande")

#### Séquence de génération d'une demande de maintenance ####

![06-Diagramme d'activité](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/5%20-%20Optimisation%20couts%20maintenance/OptimisationDemandesMaintenance.png "01 - Diagramme d'activité")

### 3. Journalisation des données ###
Globalement, ce projet vise à parvenir à récolter des données en provenance de sites isolés afin que celles-ci nous aident à prendre des décisions sur les trajets que doivent effectuer les sociétés de maintenance partenaires. 

#### Sous système d'aide à la décision ####
 ![Aide à la decision](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/6%20-%20Journalisation/aide%20decision.png "Aide à la decision" )

Sans ces données, la nouvelle solution perd tout son intérêt puisque la supervision à distance deviendrait impossible et il faudrait intervenir sur le site afin de prendre connaissance de son état, ce qui est justement le problème que la solution est censée résoudre.

Il apparaît donc que notre solution doive répondre à deux problèmes : 
 - sauvegarder les données
 - les extraire facilement

Ces deux opérations pouvant s'effectuer efficacement à l'aide d'un système de gestion de base de données adapté.

#### Journaliser ... ####
 ![Journalisation des données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/6%20-%20Journalisation/journalisation.png "Journalisation des données" )

#### ... Et extraire des donnes ####
 ![extraction des données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/6%20-%20Journalisation/extraction.png "Extraction des données" )
 
D. Transmission d'une demande de maintenance à une société de maintenance
-------------------------------------------------------------------------

#### 01 - Choix de la société de maintenance ####

Le système dispose d'un annuaire de sociétés de maintenances, lui permettant de savoir quelles sociétés de maintenance peuvent effectuer une intervention sur un site donné. Si la société attitrée à un site distant est momentanément indisponible, le système choisira une autre société disponible lorsqu'une maintenance doit être effectuée.

![01 - Transmission d'une demande de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/01ChoixDeLaSocieteDeMaintenance.png "01 - Transmission d'une demande de maintenance")

#### 02 - Transmission d'une demande de maintenance ####

Lorsqu'une demande de maintenance est générée par le système de décision du serveur central, celle-ci est transmise à la société de maintenance.

![02 - Transmission d'une demande de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/02TransmissionDemandeMaintenance.png "01 - Transmission d'une demande de maintenance")

On peut imaginer que l'envoi de la demande se fait via une service de type tickets permettant de contacter la société par email, par fax, ou encore par un appel téléphonique effectué par un opérateur. Lorsque la maintenance a été effectuée, la société de maintenance le notifie et le système peut journaliser cette notification. Si l'intervention ne peut pas être réalisée actuellement par la société, une autre sera demandée.
