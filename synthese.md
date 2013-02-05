#Synthèse#

#Rappel de l'appel d'offre#
La société COPEVUE, (Comité pour la Protection de l'EnVironement de l'UE) a lancé un appel d'offre afin de pouvoir monitorer à distance un ensemble de sites difficilement accessibles. Ces différents sites, que nous appellerons sites isolés, sont actuellement surveillés directement par leur directeur, ce dernier passant de manière occasionnelle, estimé à une fois par mois. La mission proposée par l'appel d'offre consiste à automatiser cette surveillance en transmettant des données sur l'état du site automatiquement afin de permettre une réaction beaucoup plus rapide en cas d'accident et une optimisation des coûts de maintenance.

Dans l'exemple traité, les sites seront situés au nord de la Norvège et feront une taille variant d'un diamètre de 100m à 1km. L'appel d'offre restreint la surveillance de site à des stations/réservoir possédant des cuves nécessitant chacune jusqu'à 3 capteurs : un PH-mètre, un thermomètre et un contrôleur de niveau. Dans cet exemple, la contrainte la plus forte vient du froid qu'il règne souvent dans cette région, rendant inefficaces certaines solutions. De plus l'isolation des sites et le climat de la Norvège posent des questions énergétiques importantes.

Or l'exigence principale de cet appel d'offre est l'autonomie de la solution apportée. En effet, il faut qu'elle fonctionne (presque) sans intervention humaine, dans le cas contraire on perd rapidement l'intérêt de monitorer les sites à distance. La solution proposée devra aussi répondre à certains problèmes provoqués par l'environnement dans lequel ces sites sont situés. La solution apportée devra être générique et pouvoir s'adapter aussi bien à différents types de terrains et de sites, pour plus tard ne pas être appliqué qu'en Norvège ou que pour la surveillance de cuves ... 

Lors du recueil des exigences, nous avons effectué une analyse plus approfondie des besoins et des exigences et des problèmes soulevés par ceux ci. Les points clés que nous avons identifié sont :
- l'autonomie de la solution;  
- sa fiabilité,  
- sa généricité  
- sa capacité à évoluer facilement  

Ces exigences nous ont conduit aux choix d'architectures suivants:
##Présentation générale de la solution##
Chaque site isolé possède son lot de capteurs, ceux ci transmettent leur information au système embarqué propre au site isolé. C'est ce dernier qui se charge d'envoyer ces données, lorsque c'est nécessaire, au lieu où toutes les données seront traitées: le site central. Là, les données des capteurs sont stockées, traitées et analysées pour programmer, selon la gravité des données, le passage de technicien. Les sociétés de maintenance contactées, interviennent puis effectuent un retour sur leur intervention sur le site isolé.



##Génération des demandes de maintenance##
L'intéret principal du dispositif demandé par l'appel d'offre est de pouvoir savoir très facilement si l'intervention d'une société de maintenance est nécessaire et si oui, les opérations à effectuer. Pour celà, chaque site dispose d'une base de règles qui lui est propre : ces règles identifient les différents problèmes et les réponses à y apporter selon leur gravité et leur nombre, certains problèmes n'étant pas critiques et ne nécessitant pas de maintenance dédiée. Pour déterminer quand une maintenance doit être effectuée, une solution consiste à générer des alertes lorsque des données anormales apparaissent. La génération d'alerte entrainerait les besoins suivants :

###Création de la stratégie d'alertes###
Une stratégie de gestion des alertes doit être définie une fois pour l'ensemble des sites. Elle devra définir plusieurs niveaux de gravité d'alerte, qui entraineront plus ou moins vite une demande de maintenance. Par la suite, un ensemble de règles devra être défini pour chaque site isolé, associant à chaque problème potentiel un niveau de gravité.

###Création d'une alerte###
La création automatique des alertes devra se faire au niveau du site central. C'est lui qui déclenchera une alerte en fonction des données transmises (ou de l'absence de données) par le site distant. Ces alertes génèreront ensuite une demande de maintenance si nécessaire. En parallèle des alertes automatiques, la possibilité de déclenchement d'une alerte manuelle par le directeur du site s'il constate une anomalie devra être prévue. Cette alerte devra être traitée et évaluée par un responsable du site central afin de déterminer si elle est valide ou non et de l'évaluer en cas de réponse positive.

###Transmission d'une demande de maintenance###
Une fois des alertes nécessitant une maintenance reçues, il reste à contacter la société de maintenance qui s'occupe du site isolé concerné. Il faudra prévoir les modalités de communication avec ces sociétés (par téléphone ou email, selon leurs préférences).

##Site Isolé##

L'architecture du site isolé se devait répondre aux défis suivants:
 - permettre un relevé fiable des informations  
 - effectuer un premier contrôle sur les mesures, et prévenir le site central en cas d'anomalie  
 - faire remonter régulièrement l'ensemble des données collectées sur le site  
 - assurer l'autonomie énergétique du système
 
###Acquisition des données sur le site isolé###

Les cuves sont surveillées par 3 relevés: le pH, la température, et le niveau de remplissage. Les capteurs sélectionnés doivent être en accord avec les contraintes propres aux sites isolés : températures de fonctionnement,facilité d'installation mais aussi celle liés au projet: consommation réduite. Un moyen de communication avec le système embarqué du site doit aussi être étudié.

Pour s'adapter aux différentes topologies des sites on propose deux solutions complémentaires. La première qu'on souhaite appliquer dans la majorité des cas est de relier les capteurs en filaire. L'avantage de cette solution est qu'elle est simple, autonome en energie et peu couteuse, cependant le prix peut varier si les cuves sont éloignées les unes des autres, ou être difficile à installer dans les terrains escarpés.

L'autre solution a un cout fixe, mais plus élevé : elle consiste en l'installation de baterie pour alimenter les cuves et d'un système d'emetteur/recepteur pour la transmission.



###Fréquence des communications###
Quand doit on faire un relevé de donnée? Quand doit on les envoyer et avec quelle granularité stocker ses informations? Commençons par le cas le plus simple, celui où tout se passe bien. Pour conserver un suivi de l'activité des sites on envisage de stocker une information (pour un capteur, pour une cuve, pour un site) par jour. Par conséquent envoyer plus d'une information par jour, lorsque tout va bien, semble raisonnable. Cependant que se passe t il en cas de données alarmantes? Nous avons estimé que relever les données des capteurs toutes les heures est envisageable d'un point de vue energetique et permet une bonne réactivite. Le système embarqué du site doit comparer les données reçues toutes les heures avec la donnée journalière envoyée correspondante. Si le système embarqué detecte une variation trop importante entre celles ci, il se charge d'en alerter le site central qui peut ainsi avoir un bon suivi en temps de crise. Le système sauvegarde alors la donnée envoyée comme donnée de référence pour la journée qu'il comparera avec les prochaines valeurs. L'interet de cette solution, outre de permettre un bon suivi, est qu'elle permet de limiter l'utilisation abusive de l'antenne, gourmande en energie. 


###Système Embarqué###

Le système embarqué a pour rôle de recueillir les mesures, les stocker temporairement avant de les transmettre au site central. Il doit aussi envoyer des alertes au site central lorsqu'un capteur cesse d'envoyer des données, et stocker les données des capteurs lorsque la connexion ne fonctionne plus. Lors de la reprise de connexion, les données qui n'ont pas pu être envoyées, le sont, ainsi il n'y a pas de perte d'information. Le micro-contrôleur sélectionné remplit parfaitement les besoins mentionnés ci-dessus même en envisageant une forte augmentation de la taille des sites.. Il consomme par ailleurs très peu d'énergie et est proposé à des prix avantageux si les commandes dépassent la centaine. Cette commande importante est envisageable car on peut réutiliser ce microcontroleur dans d'autres parties de la solution comme on le verra plus tard. Dans le cas du système embarqué, on adjoint à ce micro-contrôleur une mémoire externe, nécessaire au stockage temporaire des données relevées. L'intérêt de ce microcontroleur est qu'il reste relativement puissant, si les besoins évoluent: 
- Taille de la mémoire Flash&nbsp;: 32&nbsp;ko
- Taille de la RAM&nbsp;: 2048 octets
- Nombre de broches GPIO&nbsp;: 32
- Convertisseur analogique/numérique&nbsp;
- Multiplicateur matériel

- 1€45 : Micro-contrôleur générique à tout le système: [MSP430F2370](http://www.ti.com/product/msp430f2370)  
- 6€78 : Mémoire externe 64Mo [Spansion S25FL512S](www.spansion.com/Support/Datasheets/S25FL512S_00_02_e.pdf)



###Communications###

Au vu de l'isolation des sites, nous avons opté pour le seul moyen de transmettre les données disposant d'une couverture géographique adéquate et de caractéristiques satisfaisantes, les communications satellitaires. L'antenne sélectionnée propose un compromis adapté à notre situation, car elle présente un diamètre important tout en ne nécessitant pas l'installation du socle en béton propre aux antennes de plus grandes dimensions. Les bonnes caractéristiques associées aux antennes de cette dimension permettent l'utilisation d'une unité de transmission/réception de 5W seulement.

Antenne sélectionnée [Prodelin 1,8m](à renseigner!)   
Émetteur / récepteur sélectionné: [Emm/recept 5W](à renseigner!)  
Prix : 300€ ( abonnement non inclu )  

###Autonomie Énergétique###

L'autonomie énergétique est proposée sous deux formes différentes. La première, la solution applicable dans la plus part des cas, se base sur l'exploitation du potentiel éolien de la Norvège. On y associe une éolienne domestique modeste à une batterie tampon adaptée. Cette solution à été calibrée au regard de statistiques météorologiques afin d'assurer une autonomie totale et continue.

 - 3 590€ : Éolienne sélectionnée: [Ultimate Aire One 600](http://toutlesolaire.com/p/Eolienne-24V-600W-Ultimate-Aire-One-/1500.html)  
 - 9 000€ installation de l'eolienne  
 - 708€ : Batterie sélectionnée: [GEL MOLL OPzV 1530Ah 2V](http://www.apb-energy.fr/boutique/fiche_produit.cfm?ref=MOLL-OPZV-1530&type=175&code_lg=lg_fr&num=181)  

Prix par site: 13 298€

Du fait de la dépendance totale de cette première solution vis à vis des caractéristiques du site, on propose une seconde solution, générique, et pouvant être installée partout. Cette solution s'appuie sur l'optimisation différentielle d'une batterie de forte capacité. Cette dernière étant l'unique "source" d'énergie dans ce cas, on lui adjoint une résistance chauffante afin de réguler sa température, et ainsi maximiser sa rétention d'énergie tout en essayant de minimiser l'énergie gaspillée en chauffage. Dans l'optique de conserver au maximum la chaleur, on placera l'ensemble dans une enceinte thermique. Le tout est contrôlé par une brique logicielle spécifique qui fonctionne sur un micro-contrôleur qui lui est dédié.

 - 700€ : Enceinte isotherme sur mesure, partenaire potentiel: [SMCI](http://www.klege-europ-smci.com/)  
 - 12€26 : Résistance chauffante [HP04-1/04-24](http://fr.farnell.com/dbk/hp04-1-04-24/resistance-chauffante-ptc-20w/dp/4408329)  
 - 2€ : Micro-contrôleur dédie: voir partie *Système Embarqué*  
 - 5 000€ min : Batterie sélectionnée au cas par cas.  

Frais fixes:
10 000€ : Developpement de la brique logicielle approximativement  

Prix par site 5 712€26, ce qui est deux fois moins cher que la solution générique, mais pas autonome puisque la batterie nécéssite d'être rechargée, et qu'une augmentation de la taille d'un site ou sa modification peut entrainer l'achat d'une nouvelle batterie. 

##Site Central##
Le site central a pour rôle de centraliser les informations remontant des différents sites, et de programmer les visites des sociétés de maintenance après analyse de ces informations. L'architecture proposée privilégie la fiabilité et permet une solution générique personnalisable pour s'adapter aux futures évolutions du projet.

La solution proposée pour le stockage d'informations s'appuie sur une base de donnée relationnelle centralisant les données. Le support matériel de cette base de données est redondant, afin de palier à d'éventuelles pannes et/ou pertes de données.

<span style="color:#FF0000">A COMPLETER AVEC LES REFERENCES ET DETAILS</span>




#Sous système détaillé#
