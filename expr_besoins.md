Expression des Besoins
===

Après une étude de l'appel d'offre présenté nous avons défini un recueil des exigences en réfléchissant également aux problèmes qui pourraient survenir.
Le schéma ci-dessous est une représentation générale de ces besoins. Des descriptions plus détaillées sont disponibles à la suite.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/schemaGeneral.png "schéma général")

1. Communication entre les capteurs et le site central
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

2. Détermination du niveau de gravité de l'évènement
--

3. Emission d'une alerte
--
Afin de permettre d'informer la société de maintenance des problèmes nécessitant correction, il est important d'avoir une trace de leur apparition. Pour cela, une alerte sera générée à chaque problème rencontré, et remontée au serveur central.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9rer%20la%20g%C3%A9n%C3%A9ration%20des%20alertes%20%28Diagramme%20p%C3%A8re%29.png "DP - Gérer de la génération des problèmes")

Pour pouvoir filtrer les alertes selon leur gravité (et ainsi pouvoir économiser des coûts de maintenance), nous devons pouvoir établir différents niveaux de gravité. Cette priorisation sera décidée par le directeur du site distant, ou un expert engagé par ses soins.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20D%C3%A9terminer%20la%20gravit%C3%A9%20des%20probl%C3%A8mes.png "DP - Déterminer la gravité des problèmes")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20D%C3%A9termination%20de%20la%20gravit%C3%A9%20des%20probl%C3%A8mes.png "DA - Déterminer la gravité des problèmes")

Les alertes configurées par le directeur seront enregistrées dans la base du site central et levées quand une donnée transmise dépasse le seuil fixé, ou quand une erreur matériel ou de communication surgit. La création de ces alertes sera automatique, mais pourra nécessiter un traitement humain en aval.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9n%C3%A9rer%20une%20alerte%20automatiquement%20.png "DP - Générer une alerte automatiquement")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20automatique.png "DA - Générer une alerte automatiquement")

Même si l'objectif de la solution proposée est de limiter les interventions humaines, il peut arriver que des alertes soient créées manuellement. C'est notamment le cas lorsque le directeur constate une anomalie (soit dans les données transmises, soit parce qu'il s'est rendu sur place) : il doit dans ce cas remplir un formulaire et le transmettre au site central où il sera étudié.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9n%C3%A9rer%20une%20alerte%20manuellement.png "DP - Générer une alerte manuellement")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20manuelle.png "DA - Générer une alerte manuellement")


4. Emission d'une demande d'intervention d'une société de maintenance
--
Après identification de(s) évènement(s) à traiter une demande d'intervention est transmise à la société de maintenance.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/01DemandeDIntervention.png "01 - Demande d'intervention")
Pour assurer le bon fonctionnement de cette transmission il faut que cette demande d'intervention soit envoyée par un moyen de communication fonctionnel et efficace et que l'(es) évènement(s) à traiter soit(ent) connu(s) et gérable(s) par la société de maintenance.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/02MoyenDeCommunicationETEvenements.png "02 - Moyen de communication et évènements")
Afin de garantir que le moyen de communication utilisé soit fonctionnel et efficace, il faut qu'il permette de mettre en place un formalisme de communication commun entre le serveur central et la société de maintenance, formalisme que chaque demande d'intervention devra ensuite suivre. Mais il faut aussi s'assurer que la société de maintenance soit disponible et puisse se déplacer au moment de la demande d'intervention (nuit, vacances, problèmes internes, ..., peuvent toujours survenir, il faut donc gérer ces cas).
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/03MoyenDeCommunication.png "03 - Moyen de communication")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/04DisponibilitDesActeurs.png "04 - Disponibilité des Acteurs")
En ce qui concerne la gestion de l'indisponibilité de la société de maintenance désignée par défaut pour le site isolé en question un solution peut être envisageable. Il serait avantageux pour les sociétés de maintenance (relativement) proche du site isolé et capables d'intervenir sur celui-ci de collaborer. Elle pourraient former une association de société de maintenance qui permettrait de gérer les problèmes d'indisponibilité d'une seule société de maintenance en affectant la demande d'intervention à une autre société alors disponible.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/05SociTSDeMaintenance.png "05 - Association de sociétés de maintenance")

5. Optimisation des coûts de la maintenance et de la maintenance automatique
--

L'optimisation des coûts de la maintenance est l'une des exigences principales pour le projet. On prévoir ici l'existence d'un système de maintenance automatique qui permettra d'effectuer des interventions immédiates et précises pour intervenir avant qu'une anomalie n'évolue en problème nécessitant de contacter la société de maintenance. Dans les faits, ce système pourra être implémenté par des équipements spécifiques. Il pourra également être remplacé par le propriétaire du site si il réside à proximité du site, après une montée en compétence appropriée. A terme, les trajets effectués par les employés de la société de maintenance devraient être réduits au minimum, et donc, avec un contrat approprié, permettre de réduire les coûts de maintenance tout en garantissant un taux de disponibilité des équipements supérieur.

![01-Problème](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance%20ET%20automatique/DP1-1.png "01 - Problème")

![02-Génération et journalisation](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance%20ET%20automatique/DP1-2.png "02-Génération et journalisation")
Ici, lorsqu'il émet une alerte, le système de surveillance considère qu'une action doit être menée.

![03-Génération des demandes](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance%20ET%20automatique/DP2-1.png "03-Génération des demandes")
Si l'alerte est traitable par le système de maintenance auto, une demande est générée directement. Sinon, si sa priorité est mineure, elle est ajoutée à une liste de problèmes à reporter à la société de maintenance pour le site. Lorsque le seuil de problèmes pour le site est atteint, ou qu'une erreur grave survient, une demande à destination de la société de maintenance est générée.

![04-Automate de déclenchement d'une demande](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance%20ET%20automatique/DP2-2.png "04-Automate de déclenchement d'une demande")

![05-Déclenchement d'une maintenance auto](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/5%20-%20Optimisation%20couts%20maintenance%20ET%20automatique/DP2-3.png "05-Déclenchement d'une maintenance auto")

![06-Diagramme d'activité](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/5%20-%20Optimisation%20couts%20maintenance%20ET%20automatique/OptimisationDemandesMaintenance.png "01 - Diagramme d'activité")


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
 

