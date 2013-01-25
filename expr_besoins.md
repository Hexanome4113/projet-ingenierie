Expression des Besoins
===

Après une étude de l'appel d'offre présenté nous avons défini un recueil des exigences en réfléchissant également aux problèmes qui pourraient survenir.
Le schéma ci-dessous est un premier découpage, plutot évident, du problème. Notre travail va commencer par s'attarder sur les premières interfaces mises à jour, puis nous approfondirons petit à petit notre approche.
![schéma général](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/schemaGeneral.png "schéma général")

A. Communication entre le système embarqué du site distant et le serveur central
--

B. Communication entre les capteurs et le système embarqué du site distant
--

La communication des données des capteurs/actionneurs au site central est nécessaire à la satisfaction de nombreux besoins fonctionnels du système. Ainsi, les différentes étapes de cette communication doivent répondre à des exigences de qualité et de fiabilité. Cette communication est divisée en deux parties successives: le relevé des mesures par un système sur le site distant, que l'on nommera "système embarqué", et le rapatriement de ces informations jusqu'au site central. Par ailleurs, la communication de commandes remontant du site central jusqu'aux actionneurs devra être envisagée au moyen du même dispositif.

* __Communication site central - site distant__

* __Communication système embarqué - capteurs__
 
Les capteurs/actionneurs sont directement reliés au système embarqué, qui a pour role de relever et stocker les données afin de les communiquer ensuite au site central.

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/DPCommInterneSI.png "DP - Rôle de la communication système embarqué / capteurs")

Cette décomposition met en évidence deux sous problèmes liés: la nécessité de connecter les capteurs de manière fiable, dans le but de centraliser l'information sur le système embarqué.

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/DPCentraliserLesInformations.png "DP - centraliser les données")
La centralisation des données conditionne le système embarqué, et nécessite la mise en place d'une base de donnée locale ou d'un dispositif équivalent. Par ailleurs, il faut bien évidement que les capteurs soient reliés de manière fiable afin de pouvoir acquérir les mesures, ce qui nous amène au deuxième sous problème.
La fiabilité de la liaison système embarqué/capteurs repose sur deux axes principaux, l'objectif est de récupérer des mesures de qualité, et de ne rater aucune de ces mesures. Dans cette optique, nous allons nous pencher sur les deux sous problèmes suivants: La détection d'éventuelles déconnexions, et l'estimation d'une éventuelle dégradation de l'information lors du transfert.

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/DPCommSousSystMesQualitConnexion.png "DP - surveiller la qualité des connexions")

Les capteurs peuvent être analogiques ou numériques, et bien qu'on suppose devoir numériser les quelques données analogiques au moyen de dispositifs d'acquisition, les deux problèmes restent entier car le signal peut-être altéré avant même d'avoir atteint ce dispositif.

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/1%20-%20Communication%20capteurs-site%20central/DPCommSousSystMesDTecterDCo.png "DP - détecter déconnexions")

Les mesures préventives visant à éviter les éventuelles pertes de connexion dépendent bien évidement des moyens de communication employés. Quels qu'ils soient, ces dispositifs sont faillibles, et il est alors nécessaire de pouvoir détecter un problème de connexion afin de réagir rapidement. Cette nécessité exige la mise en place d'un protocole de vérification entre les extrémités des différents canaux (les capteurs, hypothétiques cartes d'acquisition, et bien entendu le système embarqué).

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
![DP - Générer une alerte automatiquement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9n%C3%A9rer%20une%20alerte%20automatiquement%20.png)
![DA - Générer une alerte automatiquement](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20automatique.png)

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

7. Sauvegarde des événements sur le site isolé en cas de connexion défaillante
-------------------------------------------------------------------------------
Que se passe t'il en cas de non reception de donnée sur le site central?
D'où vient le problème? Perte de connexion? Capteur defectueux? Système embarqué du site distant défaillant?
![07 DP général lié aux pb de connexion](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/7%20-%20Sauvegarde%20evenements%20sur%20le%20site%20isole%20connexion%20defaillante/general.png "general")
Il faut s'adapter selon les cas.  
Si c'est la connexion qui est défaillante, le système embarqué du site distant 
doit déclencher une procedure de sauvegarde locale des données.

Si défaillance des capteurs, lever d'alerte selon importance du capteur et criticité du site.
Si la connexion se rétablit il s'agit de transmettre les données qui n'ont pas 
pu l'être et sur le site central gérer l'alerte qui avait été lancée par la perte
de connexion. (Faut il ignorer l'alerte? Envoyer quelqu'un malgré un retour à la
 normale?)
 ![sauver données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/7%20-%20Sauvegarde%20evenements%20sur%20le%20site%20isole%20connexion%20defaillante/sauvergarde-locale.png "sauvegarde locale" )
 ![transmettre données](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/7%20-%20Sauvegarde%20evenements%20sur%20le%20site%20isole%20connexion%20defaillante/transmettre-donnees.png "transmettre donnees" )
   
Une perte de connexion pourrait être tolérée momentanément. Lever une alerte en cas
 de problème persistant avec crititicité selon type du site et durée de défaillance.
Du point de vue du site central, comment différencier une perte de donnée due à 
un problème de connexion, d'un problème lié au système embarqué présent là bas?  
On ne peut pas. C'est pourquoi il faut lever une alerte selon le dernier état connu
 des capteurs, la criticité du site et la durée de "non réponse" du site.  
 
Il est possible d'identifier si le problème ne vient que d'un capteur. En effet 
la connexion existe toujours dans ce cas là, il s'agit d'une absence de donnée à
 transmettre. Cette fois encore il faut lever une alerte.
 
 
 
D. Transmission d'une demande de maintenance à une société de maintenance
-------------------------------------------------------------------------

#### 01 - Choix de la société de maintenance ####

Avant d'envoyer une demande de maintenance à une société, il faut s'assurer qu'elle sera en mesure de la traiter dans les meilleurs délais. Pour cela, le système mémorise les informations de toutes les sociétés de maintenance en contrat avec COPEVUE. Celles-ci doivent indiquer les sites qu'elles sont capables de desservir et leurs domaines de compétence mais aussi indiquer leurs indisponibilités.
![01 - Transmission d'une demande de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/01ChoixDeLaSocieteDeMaintenance.png "01 - Transmission d'une demande de maintenance")


#### 02 - Transmission d'une demande de maintenance ####
Lorsqu'une demande de maintenance est générée par le système de décision du serveur central, celle-ci est transmise à la société de maintenance.
![02 - Transmission d'une demande de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/02TransmissionDemandeMaintenance.png "01 - Transmission d'une demande de maintenance")

On peut imaginer que l'envoi de la demande se fait via une service de type tickets permettant de contacter la société, ou par email, fax, ou encore appel téléphonique effectué par un opérateur. Lorsque la maintenance a été effectuée, la société de maintenance le notifie et le système peut journaliser cette notification.