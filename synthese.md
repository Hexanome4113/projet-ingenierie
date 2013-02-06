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

##Site Isolé##

L'architecture du site isolé se devait répondre aux défis suivants:  
 - permettre un relevé fiable des informations;  
 - effectuer un premier contrôle sur les mesures, et prévenir le site central en cas d'anomalie,  
 - faire remonter régulièrement l'ensemble des données collectées sur le site,  
 - assurer l'autonomie énergétique du système.
 
###Acquisition des données sur le site isolé###

Les cuves sont surveillées par 3 relevés: le pH, la température, et le niveau de remplissage. Les capteurs sélectionnés doivent être en accord avec les contraintes propres aux sites isolés : températures de fonctionnement,facilité d'installation mais aussi celle liés au projet: consommation réduite. Un moyen de communication avec le système embarqué du site doit aussi être étudié.

Pour s'adapter aux différentes topologies des sites on propose deux solutions complémentaires. La première qu'on souhaite appliquer dans la majorité des cas est de relier les capteurs en filaire. L'avantage de cette solution est qu'elle est simple, autonome en énergie et peu coûteuse, cependant le prix peut varier si les cuves sont éloignées les unes des autres, ou être difficile à installer dans les terrains escarpés.

####Par cuve : ~170€ + 39€/100m

  -  [__PH-mètre / thermomère : 109€__](http://www.electronique-diffusion.fr/product_info.php?products_id=61403)    
  Précision:+-0.01 pH /+-0.1°C    
  Consommation : 3 piles AAA ( approximativement 1200 heures d'utilisation continue)  
  -  [__Niveau : 31.50€__](http://www.directindustry.fr/prod/endress-hauser/capteurs-de-niveau-hydrostatiques-4726-745459.html)    
  Précision:+-0.2%    
  Consommation : 3V, 50mA   
  Résistance au froid    
  -  [Câbles](http://r.twenga.fr/g3.php?pg=VDszNTAxMjk2OTkzNDAzODEyMzI1OzQxNTg2MDE7aHR0cDovL2dvLmxlZ3VpZGUuY29tL25hdi90d2VuZ2FfcHRfZnIucGhwP2lkX21hZz0yOTAyNzU4MiZpZHg9NTA2MDMwNSZpZGxnPTI5MDI3NTgyODA2MSZpZF9yZWNoPSZtcz1LRVlXT1JEX0lOUFVUJmxhbmc9ZnImdmFycz10YzpwOzc1YTMwNDRjMGRkMDJkMzA4MjQ1OWE5ZTVhMmFmMzMz&dac=1): 15,49€ / 100m
  - Main-d'œuvre : 25€ + 25€/100m 
  
L'autre solution a un coût fixe, mais plus élevé : elle consiste en l'installation de batterie pour alimenter les cuves et d'un système d'émetteur/récepteur pour la transmission.
####Par cuve : ~425€
  - Capteurs identiques
  - [Émetteur](http://www.controle-sans-fil.com/index.php?main_page=product_info&cPath=173&products_id=582&zenid=8qps2f0od1pr1vc28bmhlfavu3): (longue portée) 29.23€     
  Consommation : 0.5W    
  Résistance au froid: faible, d'où l'isolation
  - [MSP430](http://hackspark.fr/fr/ti-msp430-launchpad.html) : 5.98€
  - [Batterie](http://www.absolutesport.fr/batterie-/126-batterie-haute-capacite-drift.html) : 29€     
  Capacité : 1400mAH  (Rechargement prévu une fois par an)   
  Garantie 2 ans
  - Main-d'œuvre : 50€ 4h/homme -> 50€
  - Caisson isolant : 80€
  
####Site : ~45€
  - Récepteur radio : ~30€
  - Main d'œuvre : 1h/homme : 15€


###Fréquence des communications###
Quand doit on faire un relevé de donnée? Quand doit on les envoyer et avec quelle granularité stocker ses informations? Commençons par le cas le plus simple, celui où tout se passe bien. Pour conserver un suivi de l'activité des sites on envisage de stocker une information (pour un capteur, pour une cuve, pour un site) par jour. Par conséquent envoyer plus d'une information par jour, lorsque tout va bien, semble raisonnable. Cependant que se passe t il en cas de données alarmantes? Nous avons estimé que relever les données des capteurs toutes les heures est envisageable d'un point de vue énergétique et permet une bonne réactivité. Le système embarqué du site doit comparer les données reçues toutes les heures avec la donnée journalière envoyée correspondante. Si le système embarqué détecte une variation trop importante entre celles ci, il se charge d'en alerter le site central qui peut ainsi avoir un bon suivi en temps de crise. Le système sauvegarde alors la donnée envoyée comme donnée de référence pour la journée qu'il comparera avec les prochaines valeurs. L'intérêt de cette solution, outre de permettre un bon suivi, est qu'elle permet de limiter l'utilisation abusive de l'antenne, gourmande en énergie. 


###Système Embarqué###

Le système embarqué a pour rôle de recueillir les mesures, les stocker temporairement avant de les transmettre au site central. Il doit aussi envoyer des alertes au site central lorsqu'un capteur cesse d'envoyer des données, et stocker les données des capteurs lorsque la connexion ne fonctionne plus. Lors de la reprise de connexion, les données qui n'ont pas pu être envoyées, le sont, ainsi il n'y a pas de perte d'information. Le micro-contrôleur sélectionné remplit parfaitement les besoins mentionnés ci-dessus même en envisageant une forte augmentation de la taille des sites.. Il consomme par ailleurs très peu d'énergie et est proposé à des prix avantageux si les commandes dépassent la centaine. Cette commande importante est envisageable car on peut réutiliser ce microcontrôleur dans d'autres parties de la solution comme on le verra plus tard. Dans le cas du système embarqué, on adjoint à ce micro-contrôleur une mémoire externe, nécessaire au stockage temporaire des données relevées. L'intérêt de ce microcontrôleur est qu'il reste relativement puissant, si les besoins évoluent: 
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

 - 3 590€ : Éolienne sélectionnée: [Ultimate Aire One 600](http://toutlesolaire.com/p/éolienne-24V-600W-Ultimate-Aire-One-/1500.html)  
 - 9 000€ : Installation de l'éolienne  
 - 708€ : Batterie sélectionnée: [GEL MOLL OPzV 1530Ah 2V](http://www.apb-energy.fr/boutique/fiche_produit.cfm?ref=MOLL-OPZV-1530&type=175&code_lg=lg_fr&num=181)  

Prix par site: 13 298€

Du fait de la dépendance totale de cette première solution vis à vis des caractéristiques du site, on propose une seconde solution, générique, et pouvant être installée partout. Cette solution s'appuie sur l'optimisation différentielle d'une batterie de forte capacité. Cette dernière étant l'unique "source" d'énergie dans ce cas, on lui adjoint une résistance chauffante afin de réguler sa température, et ainsi maximiser sa rétention d'énergie tout en essayant de minimiser l'énergie gaspillée en chauffage. Dans l'optique de conserver au maximum la chaleur, on placera l'ensemble dans une enceinte thermique. Le tout est contrôlé par une brique logicielle spécifique qui fonctionne sur un micro-contrôleur qui lui est dédié.

 - 700€ : Enceinte isotherme sur mesure, partenaire potentiel: [SMCI](http://www.klege-europ-smci.com/)  
 - 12€26 : Résistance chauffante [HP04-1/04-24](http://fr.farnell.com/dbk/hp04-1-04-24/resistance-chauffante-ptc-20w/dp/4408329)  
 - 1€45 : Micro-contrôleur dédie: voir partie *Système Embarqué*  
 - 5 000€ min : Batterie sélectionnée au cas par cas.  

Frais fixes:
10 000€ : Développement de la brique logicielle approximativement  

Prix par site 5 713€71.
Les coûts sont peut être deux fois moins cher que la solution générique, mais la solution n'est pas autonome puisque la batterie nécessite d'être rechargée, et qu'une augmentation de la taille d'un site ou sa modification peut entraîner l'achat d'une nouvelle batterie. 

##Site Central##
Le site central a pour rôle de centraliser les informations remontant des différents sites, et de programmer les visites des sociétés de maintenance après analyse de ces informations. L'architecture proposée privilégie la fiabilité et permet une solution générique personnalisable pour s'adapter aux futures évolutions du projet.

###Réception et Journalisation des données###
On met en place un [serveur](http://www.ldlc-pro.com/fiche/PB00140367.html) accédé par les systèmes embarqués des sites distants, a priori très peu gourmand en ressources mais devant assurer un service fiable et continu. Il sera donc doublé et protégé par le pare feu grâce à des règles strictes : 2500€.  
Le stockage des données est important non seulement pour assurer un suivi de l'activité du site mais aussi car il permet, lors de prendre de meilleur décision lorsqu'il s'agit de faire appel à une société de maintenance. En effet un historique des interventions, des différents état du site ou l'observation de certains motifs dans les données peut influencer les choix en matière de programmation de visite des sites. La solution proposée pour le stockage d'informations s'appuie sur une base de donnée relationnelle centralisant les données. Le support matériel de cette base de données est redondant, afin de palier à d'éventuelles pannes et/ou pertes de données. Le [serveur](http://www.ldlc-pro.com/fiche/PB00125969.html) pour la base de données dispose d’importantes ressources ([RAM](http://www.ldlc-pro.com/fiche/PB00131422.html), [stockage](http://www.ldlc-pro.com/fiche/PB00140386.html)). Les deux coûtent un total de 5000€.

###Un système de règle###
L'intérêt principal du dispositif demandé par l'appel d'offre est de pouvoir savoir très facilement si l'intervention d'une société de maintenance est nécessaire et si oui, les opérations à effectuer. Pour cela, chaque site dispose d'une base de règles qui lui est propre : ces règles identifient les différents problèmes et les réponses à y apporter selon leur gravité et leur nombre, certains problèmes n'étant pas critiques et ne nécessitant pas de maintenance dédiée. Les données des sites et leur historique permettent de générer des alertes plus ou moins graves. En pratique, ce système se traduia par un [serveur](http://www.pc-look.com/boutik/62908.html) web et d’application accédé par des clients légers sur les postes des employés. Celui ci doit périodiquement effectuer des calculs complexes (aide à la décision), par conséquent il sera doté de ressources conséquentes, ce qui garantira sa faible charge et sa forte réactivité la majorité du temps. (5000€)
Cette solution intégrera notamment de puissants algorithmes d'aide à la décision adaptés à nos grandes quantités de données. Son coût de développement, mise en production et maintenance corrective et évolutive (sur 5 ans) est estimé à environ 30 000 euros. 
###Création de la stratégie d'alertes###
Une stratégie de gestion des alertes doit être définie une fois pour l'ensemble des sites. Elle devra définir plusieurs niveaux de gravité d'alerte, qui entraîneront plus ou moins vite une demande de maintenance. Une stratégie générale sera établie lors de la configuration initiale du projet à l'aide des techniciens des sociétés de maintenance traitant actuellement les sites. Les propriétaires n'étant pas forcément ceux qui possèdent le plus de connaissance sur les sites isolés. Par la suite, ces règles pourront être modifiés, par exemple si on observe à l'utilisation un signe précurseur dans les données d'une panne, programmer une règle demandant l'intervention à l'apparition de ce signe.
 

###Création d'une alerte###
La possibilité de déclenchement d'une alerte manuelle par le directeur du site s'il constate une anomalie devra être prévue. Cette alerte devra être traitée et évaluée par un responsable du site central afin de déterminer si elle est valide ou non et de l'évaluer en cas de réponse positive.

###Transmission d'une demande de maintenance###
Une fois des alertes nécessitant une maintenance reçues, il reste à contacter la société de maintenance qui s'occupe du site isolé concerné. Il faudra prévoir les modalités de communication avec ces sociétés (par téléphone ou email, selon leurs préférences).
Une fois l'opération demandée effectuée les techniciens peuvent remplir les détail de l'intervention via une interface web. Le [serveur web](http://www.ldlc-pro.com/fiche/PB00096757.html) nécessaire ne requiert pas de performances accrues, 1000€.

###Personnel sur place###
Pour faire fonctionner le site central, nous avons prévu une équipe de cinq personnes :
 - Un agent en charge de faire la maintenance logicielle et matérielle du site, comme il est nécessaire dès l'installation d'informatique dans une entreprise.  
 - Un(e) secrétaire qui s'occupera de la relation avec les propriétaires mais aussi les sociétés de maintenances  
 - Un Comptable  
 - Un donneur d’ordres aux sociétés de maintenance, pour traiter toutes les alertes non automatisées  
 - Un directeur responsable de la coordination site central/site distant, travail de management (coordination des équipes, réunions, planifications diverses)  
  
##Budget prévisionnel pour la mise en place de la solution ##
Estimation des coûts du site central : 
 - Le [serveur](http://www.pc-look.com/boutik/62908.html) web et d’application accédé par tous les clients légers des postes des employés, effectuant les calculs complexes d'aide à la décision 5000€  
 - Coûts développement de cette solution de création d'alerte: 30 000€  
 - Un [pare-feu](http://www.ldlc-pro.com/fiche/PB00135486.html) permettant de faire respecter la politique de sécurité du réseau de l’entreprise 1500€  
 - Le serveur web hébergeant l'application accessible aux entreprises de maintenance permettant de saisir les détails des opérations de maintenance effectuées 1000€  
 - Les deux serveurs pour la base de données, disposant d’importantes ressources 5000€  
 - Les deux serveurs accédé par les systèmes embarqués des sites distants 2 500€   
 - Création d'un poste par employer (mobilier, ordinateur,...) 1 500€ par membre du personnel  
 - Onduleurs, câbles, imprimante réseau, périphériques... (3000€)  
  
Frais mensuels:  
 - Salaires: 15 000€ par personne  
 - Location de locaux : 2 000€ par mois (70m²).  

Frais liés à la création d'un site central:  
Installation 55 500€  
Frais de fonctionnement (salaire 15 000€ par personne et loyer 2 000€ par mois): 77 000€  

Frais liés à l'installation des sites:  
Solution 1 : 13 300€ par site (éolienne prix+pose)  
15 sites de 30 cuves 200€ / cuve  
25 sites de 20 cuves 250€ /cuve  
10 sites de 10 cuves 300€ /cuve  

Solution 2 : 5 700€ par site (batterie+ émetteur/récepteur) :  
5 sites de 20 cuves 425€/cuve   
Frais liés au développement de la solution 2 :10 000€  
 
Coût total estimé : 1 046 000€  


