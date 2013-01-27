Expression des Besoins
===

Après une étude de l'appel d'offre présenté nous avons défini un recueil des exigences en réfléchissant également aux problèmes qui pourraient survenir.
Le schéma ci-dessous est un premier découpage, plutot évident, du problème. Notre travail va commencer par s'attarder sur les premières interfaces mises à jour, puis nous approfondirons petit à petit notre approche.
![schéma général](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/schemaGeneral.png "schéma général")

A. Communication entre le système embarqué du site distant et le serveur central
--------------------------------------------------------------------------------
Le coeur du problème est le suivant: supposons que nous possédons des données sur l'état d'un site (nous verrons un peu plus tard d'où nous vient cette connaissance) et nous souhaitons les transmettre à une autre unitée distante: le cite central. Cette communication doit répondre aux exigences de qualité et de fiabilité. Par ailleurs, la communication de commandes remontant du site central jusqu'à des actionneurs devra être envisagée au moyen du même dispositif.

Si la connexion vers le site centrale est défaillante, le système embarqué du site distant doit déclencher une procedure de sauvegarde locale des données.
####Sauver des données####
![sauver données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/sauvegarde-locale.png "sauvegarde locale" )


Lorsque la connexion est rétablie, ou réparée, le système embarqué doit envoyer les données qu'il a sauvegardé. Ainsi malgré l'incident, il est possible d'avoir un suivi continu de l'acquisition des données.
####Transmettre des données####
 ![transmettre données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/transmettre-donnee.png "transmettre donnees" )
 
 
Que se passe t'il en cas de non reception de donnée sur le site central?
D'où vient le problème? Perte de connexion? Capteur defectueux? Système embarqué du site distant défaillant?

Si le capteur est defectueux, le site central reçoit tout de même les autres informations liées au site. Il s'agit donc de lever l'alerte adaptée au problème.

Qu'en est il de la distinction entre une perte de connexion et un système embarqué du site distant défaillant? On ne peut pas, il faut donc lever l'alerte correspondant au niveau de gravité le plus élevé : panne du système embarqué lui même. En effet, en cas de perte de connexion les données sont sauvergardée localement par le site isolé puis ré-envoyées dès la connexion rétablie. De plus il faut lever une alerte selon d'autres facteurs : le dernier état connu des capteurs, la criticité du site et la durée de "non réponse" du site.

B. L'acquisition des données et la communication entre les capteurs et le système embarqué du site distant
--------------------------------------------------------------------------
Nous avions jusqu'à présent des informations à transmettre au site central. Il s'agit de savoir comment ses données ont été collectées et comment elles ont été transmises au système embarqué du site isolé.
nécessité de connecter les capteurs de manière fiable
![contrainte de distance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/distance.png "contrainte de distance")


C. Génération des demandes de maintenance
-----------------------------------------

### 1. Détermination du niveau de gravité de l'évènement et émission d'une alerte ###

Quelles sont les conditions de déclenchant une alerte? Actuellement, c'est le propriétaire du site qui informe les sociétés de maintenance, on peut donc estimer qu'il peut toujours observer un problème sur le site et demander une intervention. La différence principale est qu'en absence du propriétaire, les sites sont toujours surveillés par le biais de capteurs. C'est le remontée d'information indiquant un état critique du paramètre observé qui déclenche l'alerte. 
![DP - Gérer de la génération des problèmes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/LucidAlerte.png)
Les capteurs et les sites isolés doivent transmettre des informations recueillies et non les alertes elles même. En effet, le système doit être fiable, or si un site isolé tombe en panne, il ne peut plus signaler au site central une alerte indiquant son non fonctionnement. Pour ces raisons plutôt évidentes, c'est le site central qui reçoit des informations, les traite et en conséquence génere des alertes. Un point particulier lié à un disfonctionnement et à la perte d'information sera développé plus loin.


![DP - Déterminer la gravité des problèmes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/GestionAlertes.png)
Pour pouvoir filtrer les alertes selon leur gravité (et ainsi pouvoir économiser des coûts de maintenance), nous devons pouvoir établir différents niveaux de gravité. Qui peut connaître cette gravaité? Actuellement le propriétaire du site, celui qui demande des interventions, n'a pas forcément de connaissance sur son site, et parfois même il peut se tromper en indiquant à la société de maintenance des points peu importants ou oublier des points essentiels. La connaissance de ces sites est donc chez les sociétés de maintenance. Avant de configurer notre système, il faudra réaliser une étude visant à mettre en commun les connaissance pour établir la criticité des situations.
![DP - Déterminer la gravité des problèmes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20D%C3%A9terminer%20la%20gravit%C3%A9%20des%20probl%C3%A8mes.png)
![DA - Déterminer la gravité des problèmes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20D%C3%A9termination%20de%20la%20gravit%C3%A9%20des%20probl%C3%A8mes.png)

Les alertes configurées par le directeur seront enregistrées dans la base du site central et levées quand une donnée transmise dépasse le seuil fixé, ou quand une erreur matériel ou de communication surgit. La création de ces alertes sera automatique, mais pourra nécessiter un traitement humain en aval.
![DP - Générer une alerte automatiquement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20Alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20automatique.png "générer alerte autoomatique")
![DA - Générer une alerte automatiquement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20Alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20manuelle.png DA - Générer une alerte automatiquement)

Même si l'objectif de la solution proposée est de limiter les interventions humaines, il peut arriver que des alertes soient créées manuellement. C'est notamment le cas lorsque le directeur constate une anomalie (soit dans les données transmises, soit parce qu'il s'est rendu sur place) : il doit dans ce cas remplir un formulaire et le transmettre au site central où il sera étudié.
![DP - Générer une alerte manuellement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9n%C3%A9rer%20une%20alerte%20manuellement.png)
![DA - Générer une alerte manuellement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20manuelle.png)


### 2. Optimisation des coûts de la maintenance ###

![01-Problème](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/DP-1.png "01 - Problème")
L'optimisation des coûts de la maintenance est l'une des exigences principales pour le projet. Elle se fait entre le moment où on reçoit une alerte et celui où une demande de maintenance est produite.

![02-Génération et journalisation](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/DP-2.png "02-Génération et journalisation")
Pour permettre de sécuriser le système et de retracer les actions effectuées, toute demande de maintenance doit être journalisée à sa création. Elle sera ensuite envoyée à une société de maintenance.

![03-Génération des demandes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/DP-3.png "03-Génération des demandes")
Pour éviter de demander des interventions lorsque cela n'est pas nécessaire, les alertes jugées mineures sont mises de côté pour chaque site tant qu'un nombre d'alertes mineures donnée n'est pas atteint. Lorsqu'il est atteint ou qu'une alerte critique survient, une demande de maintenance est générée.

![04-Automate de déclenchement d'une demande](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance/Automate.png "04-Automate de déclenchement d'une demande")

#### Séquence de génération d'une demande de maintenance ####

![06-Diagramme d'activité](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/5%20-%20Optimisation%20couts%20maintenance/OptimisationDemandesMaintenance.png "01 - Diagramme d'activité")


6. Journalisation des données
-----------------------------
Globalement, le projet vise à parvenir à récolter des données en provenance de sites isolés 
afin que celles ci nous aident à prendre des décisions sur les trajets que doivent effectuer les entreprises
de maintenance partenaires. 

Sans ces données, la nouvelle solution perd tout son intérêt puisque la supervision à distance devient impossible 
et il faut donc intervenir sur le site afin de prendre connaissance de son état, 
ce qui est justement le problème que la solution est censée résoudre.

Il apparaît donc que notre solution doit répondre à deux problèmes : 
 - sauvegarder les données
 - les extraire facilement

ces deux opérations pouvant s'effectuer efficacement à l'aide d'un système de gestion de base de donnée adapté.

 ![Journalisation des données2](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/6%20-%20Journalisation/DPJournalisation2.png "Journalisation des données2" )
 ![Journalisation des données1](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/6%20-%20Journalisation/DPJournalisation1.png "Journalisation des données1" )
 ![Journalisation des données3](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/6%20-%20Journalisation/DPJournalisation3.png "Journalisation des données3" )

 
 
D. Transmission d'une demande de maintenance à une société de maintenance
-------------------------------------------------------------------------

#### 01 - Choix de la société de maintenance ####

Avant d'envoyer une demande de maintenance à une société, il faut s'assurer qu'elle sera en mesure de la traiter dans les meilleurs délais. Pour cela, le système mémorise les informations de toutes les sociétés de maintenance en contrat avec COPEVUE. Celles-ci doivent indiquer les sites qu'elles sont capables de desservir et leurs domaines de compétence mais aussi indiquer leurs indisponibilités.
![01 - Transmission d'une demande de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/01ChoixDeLaSocieteDeMaintenance.png "01 - Transmission d'une demande de maintenance")


#### 02 - Transmission d'une demande de maintenance ####
Lorsqu'une demande de maintenance est générée par le système de décision du serveur central, celle-ci est transmise à la société de maintenance.
![02 - Transmission d'une demande de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/02TransmissionDemandeMaintenance.png "01 - Transmission d'une demande de maintenance")

On peut imaginer que l'envoi de la demande se fait via une service de type tickets permettant de contacter la société, ou par email, fax, ou encore appel téléphonique effectué par un opérateur. Lorsque la maintenance a été effectuée, la société de maintenance le notifie et le système peut journaliser cette notification.
