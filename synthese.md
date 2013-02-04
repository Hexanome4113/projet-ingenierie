#Synthèse#

#Rappel de l'appel d'offre#
L'appel d'offre que nous avons étudié a été lancé par la COPEVUE, (Comité pour la Protection de l'EnVironement de l'UE), qui souhaite pouvoir monitorer à distance un ensemble de sites difficilement accessibles. Ces différents sites, que nous apellerons sites isolés, sont actuellement surveillés directement par leur directeur, ce dernier passant de manière occasionnelle, estimé à une fois par mois. La mission proposée par l'appel d'offre consiste à automatiser cette surveillance en transmettant des données sur l'état du site automatiquement afin de permettre une réaction beaucoup plus rapide en cas d'accident et une optimisation des coûts de maintenance.

Dans l'exemple traité, les sites seront situés au nord de la Norvège et feront une taille variant d'un diamètre de 100m à 1km. L'appel d'offre restreint la surveillance de site à des stations/réservoir possédant des cuves nécessitant chacune jusqu'à 3 capteurs : un ph-mètre, un thermomètre et un contrôleur de niveau. Dans cette exemple, la contrainte la plus forte vient du froid qu'il règne souvent dans cette région, rendant inefficaces certaines solutions. De plus l'isolation des sites et le climat de la Norvège pose des questions énergétiques importantes.

Or l'exigence principale de cet appel d'offre est l'automie de la solution apportée. En effet, il faut qu'elle fonctionne (presque) sans intervention humaine, dans le cas contraire on perd rapidement l'interet de monitorer les sites à distance. La solution proposée devra aussi répondre à certains problèmes provoqués par l'environnement dans lequel ces sites sont situés. La solution apportée devra être générique et pouvoir s'adapter aussi bien à différents types de terrains et de sites, pour plus tard ne pas être appliqué qu'en Norvège ou que pour la surveillance de cuves ... 

#Recueil des exigences#

Afin d'avoir une vision plus précise des exigences de l'appel d'offre, nous avons effectué une analyse plus approfondie de ce dernier en se concentrant sur les problèmes soulevés par ces exigences. Les principaux problèmes identifiés sont les suivants :

##Acquisition des données sur le site isolé##
Pour récupérer les données, différents capteurs seront installés sur chacun des sites. Cependant, pour des raison de coût et d'économie d'énergie, il est évident que chaque capteur ne pourra être équipé d'un dispositif permettant de communiquer avec le site central. Il est donc nécessaire de regrouper les informations du site isolé dans une seule unité qui sera chargée de communiquer avec le site central. Cette unité sera composée d'un dispositif de communication et d'un système embarqué permettant de contrôler ces communications. Pour celà, il faut déterminer plusieurs choses : en premier lieu, réussir à trouver un matériel fonctionnant dans les conditions imposées (froid, éloignement entre la cuve et le système embarqué, topologie du terrain...) à la fois pour le système embarqué et pour les cuves; en second lieu, trouver une architecture et une stratégie de communication entre capteurs et système embarqué permettant de limiter leur dépense en énergie tout en ayant des mesures suffisamment fréquentes pour pouvoir être exploitées au niveau du site central.

##Transmission des données au serveur central##
Pour que les personnes présentes sur le site central puissent obtenir les données recueillies sur le site isolé, il faut pouvoir établir une communication entre les deux. Cet aspect englobe à la fois la communication en elle même (non seulement l'aspect matériel, mais aussi le protocole et la fréquence), la gestion des problèmes (reprise de communication en cas de rupture) et l'enregistrement de traces portants sur les mesures effectuées. La frequence à laquelle il est utile de recevoir des données doit aussi être un point de reflexion.

##Génération des demandes de maintenance##
L'intéret principal du dispositif demandé par l'appel d'offre est de pouvoir savoir très facilement si l'intervention d'une société de maintenance est nécessaire et si oui, les opérations à effectuer. Pour celà, chaque site dispose d'une base de règles qui lui est propre : ces règles identifient les différents problèmes et les réponses à y apporter selon leur gravité et leur nombre, certains problèmes n'étant pas critiques et ne nécessitant pas de maintenance dédiée. Pour déterminer quand une maintenance doit être effectuée, une solution consiste à générer des alertes lorsque des données anormales apparaissent. La génération d'alerte entrainerait les besoins suivants :

###Création de la stratégie d'alertes###
Une stratégie de gestion des alertes doit être définie une fois pour l'ensemble des sites. Elle devra définir plusieurs niveaux de gravité d'alerte, qui entraineront plus ou moins vite une demande de maintenance. Par la suite, un ensemble de règles devra être défini pour chaque site isolé, associant à chaque problème potentiel un niveau de gravité.

###Création d'une alerte###
La création automatique des alertes devra se faire au niveau du site central. C'est lui qui déclenchera une alerte en fonction des données transmises (ou de l'absence de données) par le site distant. Ces alertes génèreront ensuite une demande de maintenance si nécessaire. En parallèle des alertes automatiques, la possibilité de déclenchement d'une alerte manuelle par le directeur du site s'il constate une anomalie devra être prévue. Cette alerte devra être traitée et évaluée par un responsable du site central afin de déterminer si elle est valide ou non et de l'évaluer en cas de réponse positive.

###Transmission d'une demande de maintenance###
Une fois des alertes nécessitant une maintenance reçues, il reste à contacter la société de maintenance qui s'occupe du site isolé concerné. Il faudra prévoir les modalités de communication avec ces sociétés (par téléphone ou email, selon leurs préférences).


#Architecture de la solution#

##Site Isolé##

L'architecture du site isolé se devait répondre aux défis suivants:
 - permettre un relevé fiable des informations  
 - effectuer un premier contrôle sur les mesures, et prévenir le site central en cas d'anomalie  
 - faire remonter régulièrement l'ensemble des données collectées sur le site  
 - assurer l'autonomie énergétique du système  

###Capteurs et Communication intra-site###

On veut relever 3 grandeurs dans les cuves: le pH, la température, et le niveau de remplissage. Les capteurs sélectionnés sont en accord avec les contraintes propres aux sites isolés (températures de fonctionnement, consommation réduite...). La conception autour des capteurs doit répondre aux questions suivantes: leur consommation en énergie et la transmission des mesures vers un lieu où elles pourront être envoyé au site central.

Pour s'adapter aux différentes topologies des sites on propose deux solutions complémentaires. La première qu'on souhaite appliquer dans la majorité des cas : relier les capteurs en filaire. L'avantage de cette solution est qu'elle est simple, autonome en energie et peu couteuse, cependant le prix peut varier si les cuves sont éloignées les unes des autres, ou être difficile à installer dans les terrains escarpés.

L'autre solution a un cout fixe, mais plus élevé : elle consiste en l'installation de baterie pour alimenter les cuves et d'un système d'emetteur/recepteur pour la transmission.

<span style="color:#FF0000">A COMPLETER AVEC LES REFERENCES</span>

###Système Embarqué###

Le système embarqué a pour rôle de recueillir les mesures, les stocker temporairement avant de les transmettre au site central. Une première analyse visant à détecter d'importants sauts dans les valeurs est également souhaitable, un écart brutal vis-à-vis des valeurs précédentes étant souvent le symptôme d'une anomalie.  
Le micro-contrôleur sélectionné remplit parfaitement les besoins mentionnés ci-dessus même en envisageabnt une forte augmentation de la taille des sites, mais également les autres cas d'utilisation envisagés (micro-contrôleur dédié au calcul différentiel, micro-contrôleur de communications radio...). Il consomme par ailleurs très peu d'énergie et est proposé à moins de deux euros l'unité (si on envisage des commandes de 1000 exemplaires). Dans le cas du système embarqué, on adjoint à ce micro-contrôleur une mémoire externe, nécessaire au stockage temporaire des données relevées.

 * Micro-contrôleur générique à tout le système: [MSP430F2370](http://www.ti.com/product/msp430f2370)  
 * Mémoire externe: [Spansion S25FL512S](www.spansion.com/Support/Datasheets/S25FL512S_00_02_e.pdf)



###Communications###

Au vu de l'isolation des sites, nous avons opté pour le seul moyen de transmettre les données disposant d'une couverture géographique adéquate et de caractéristiques satisfaisantes, les communications satellitaires. L'antenne sélectionnée propose un compromis adapté à notre situation, car elle présente un diamètre important tout en ne nécessitant pas l'installation du socle en béton propre aux antennes de plus grandes dimensions. Les bonnes caractéristiques associées aux antennes de cette dimension permettent l'utilisation d'une unité de transmission/réception de 5W seulement.

Antenne sélectionnée [Prodelin 1,8m](à renseigner!) 
Émetteur / récepteur sélectionné: [Emm/recept 5W](à renseigner!) 

<span style="color:#FF0000">MODELE / LIEN à renseigner</span>

###Fréquence des communications###
Quand doit on faire un relevé de donnée? Quand doit on les envoyer et avec quelle granularité stocker ses informations? Commençons par le cas le plus simple, celui où tout se passe bien. Pour conserver un suivi de l'activité des sites on envisage de stocker une information (pour un capteur, pour une cuve, pour un site) par jour. Par conséquent envoyer plus d'une information par jour, lorsque tout va bien, semble raisonnable. Cependant que se passe t il en cas de données alarmantes? Nous avons estimé que relever les données des capteurs toutes les heures est envisageable d'un point de vue energetique et permet une bonne réactivite. Le système embarqué du site doit comparer les données reçues toutes les heures avec la donnée journalière envoyée correspondante. Si le système embarqué detecte une variation trop importante entre celles ci, il se charge d'en alerter le site central qui peut ainsi avoir un bon suivi en temps de crise. Le système sauvegarde alors la donnée envoyée comme donnée de référence pour la journée qu'il comparera avec les prochaines valeurs. L'interet de cette solution, outre de permettre un bon suivi, est qu'elle permet de limiter l'utilisation abusive de l'antenne, gourmande en energie. 

###Autonomie Énergétique###

L'autonomie énergétique est proposée sous deux formes différentes. La première, la solution applicable dans la plus part des cas, se base sur l'exploitation du potentiel éolien de la Norvège. On y associe une éolienne domestique modeste à une batterie tampon adaptée. Cette solution à été calibrée au regard de statistiques météorologiques afin d'assurer une autonomie totale et continue.

 * Éolienne sélectionnée: [Ultimate Aire One 600](http://toutlesolaire.com/p/Eolienne-24V-600W-Ultimate-Aire-One-/1500.html)  
 * Batterie sélectionnée: [GEL MOLL OPzV 1530Ah 2V](http://www.apb-energy.fr/boutique/fiche_produit.cfm?ref=MOLL-OPZV-1530&type=175&code_lg=lg_fr&num=181)


Du fait de la dépendance totale de cette première solution vis à vis des caractéristiques du site, on propose une seconde solution, générique, et pouvant être installée partout. Cette solution s'appuie sur l'optimisation différentielle d'une batterie de forte capacité. Cette dernière étant l'unique "source" d'énergie dans ce cas, on lui adjoint une résistance chauffante afin de réguler sa température, et ainsi maximiser sa rétention d'énergie tout en essayant de minimiser l'énergie gaspillée en chauffage. Dans l'optique de conserver au maximum la chaleur, on placera l'ensemble dans une enceinte thermique. Le tout est contrôlé par une brique logicielle spécifique qui fonctionne sur un micro-contrôleur qui lui est dédié.

 * Enceinte isotherme sur mesure, partenaire potentiel: [SMCI](http://www.klege-europ-smci.com/)  
 * Résistance chauffante: [HP04-1/04-24](http://fr.farnell.com/dbk/hp04-1-04-24/resistance-chauffante-ptc-20w/dp/4408329)  
 * Micro-contrôleur dédie: voir partie *Système Embarqué*  
 * Batterie sélectionnée au cas par cas.  
 * Developpement de la brique logicielle (approx 4000€)

##Site Central##
Le site central a pour rôle de centraliser les informations remontant des différents sites, et de programmer les visites des sociétés de maintenance après analyse de ces informations. L'architecture proposée privilégie la fiabilité et permet une solution générique personnalisable pour s'adapter aux futures évolutions du projet.

La solution proposée pour le stockage d'informations s'appuie sur une base de donnée relationnelle centralisant les données. Le support matériel de cette base de données est redondant, afin de palier à d'éventuelles pannes et/ou pertes de données.

<span style="color:#FF0000">A COMPLETER AVEC LES REFERENCES ET DETAILS</span>




#Sous système détaillé#
