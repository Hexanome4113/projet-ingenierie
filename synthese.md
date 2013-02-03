#Synthèse#
Ceci est une synthèse, donc on ne crée pas d'information.
Elle doit faire au max 6 pages.
On doit avoir à peu pres 3 fois ça dans le git, donc pas besoin de faire du pipeau : on veut des info pertinentes justifiées et interessantes
#Rappel de l'appel d'offre#
Thibaut : _Bon allez j'me charge de cette partie_

L'appel d'offre que nous allons étudier dans ce projet a été effectué par la COPEVUE, (un organisme regroupant des propriétaires de sites distants (à corriger quand j'aurai le sujet)), qui souhaite pouvoir monitorer à distance un ensemble de sites difficilement accessibles.
Ces différents site sont actuellement surveillés directement par leur directeur, ce dernier passant de manière occasionnelle quand il en a le temps, ce qui reste assez rare en raison de l'innaccessibilité de ces sites. La mission 
proposée par l'appel d'offre consiste donc à automatiser cette surveillance en transmettant des données automatiquement à un site central afin de permettre une réaction beaucoup plus rapide en cas d'accident et une optimisation des coûts de maintenance.

L'exigence principale de cet appel d'offre est l'automie de la solution apportée. En effet, il faut qu'elle fonctionne sans (presque) aucune intervention humaine. La solution proposée devra aussi répondre à certains problèmes provoqués par l'environnement dans lequel ces sites sont situés, c'est à dire le nord de la Norvège. La plus importante vient du froid qu'il règne souvent dans cette région,
rendant innefficaces certaines solutions.

#Recueil des exigences#
Thibaut : _Bon allez de celle là aussi_

Afin d'avoir une vision plus précise des exigences de l'appel d'offre, nous avons effectué une analyse plus approfondie de ce dernier en se concentrant sur les problèmes soulevés par ces exigences. Les principaux problèmes identifiés sont les suivants :
##Acquisition des données sur le site central##
Afin de récupérer les données enregistrées par les différents capteurs installés sur les sites distants, une transmission devra être effectuée entre ces capteurs et un système embarqué présent sur le site. Pour celà, il faut déterminer plusieurs choses : en premier lieu, réussir à trouver un matériel fonctionnant dans les conditions imposées (froid, éloignement par rapport au système embarqué, topologie du terrain...); en second lieu, trouver une stratégie de communication des capteurs permettant de limiter leur temps de fonctionnement (pour économiser l'énergie) tout en ayant des mesures suffisamment fréquentes pour pouvoir être exploitées au niveau du site central.

##Transmission des données au serveur central##
Pour que les personnes présentes sur le site central puissent obtenir les données recueillies sur le site distant, il faut pouvoir établir une communication entre les deux. Cet aspect englobera à la fois la communication en elle même (non seulement l'aspect matériel, mais aussi le protocole et la fréquence), la gestion des problèmes (reprise de communication en cas de rupture) et l'enregistrement de traces portants sur les mesures effectuées.

##Génération des demandes de maintenance##
L'intéret principal du dispositif demandé par l'appel d'offre est de pouvoir savoir très facilement si l'intervention d'une société de maintenance est nécessaire et si oui, les opérations à effectuer. Pour celà, une base de règles sera générée pour chaque site. Ces règles identifieront les différents problèmes et les réponses à y apporter selon leur gravité et leur nombre, certains problèmes n'étant pas critiques et ne nécessitant pas de maintenance dédiée.

###Création de la stratégie d'alertes###
La stratégie de gestion des alertes sera définie une fois pour l'ensemble des sites. Elle consistera à définir plusieurs niveaux de gravité d'alerte, qui entraineront plus ou moins vite une demande de maintenance. Par la suite, un ensemble de règles devra être défini pour chaque site distant, associant à chaque problème potentiel un niveau de gravité.

###Création d'une alerte###
La création automatique des alertes se fera au niveau du site central. C'est lui qui déclenchera une alerte en fonction des données transmises (ou de l'absence de données) par le site distant. Ces alertes génèreront ensuite une demande de maintenance si nécessaire. En parallèle des alertes automatiques, une alerte manuelle pourra être soulevée par le directeur du site s'il constate une anomalie. Cette alerte sera traitée et évaluée par un responsable du site central, et enregistrée si elle est valide, entraînant le même traitement qu'une alerte automatique.

###Transmission d'une demande de maintenance###
Une fois des alertes nécessitant une maintenance reçu, il reste à contacter la société de maintenance qui s'occupe du site distant concerné. Ce contact s'effectuera humainement par téléphone ou email, selon les préférences des sociétés de maintenance, même si un système centralisé pourrait être envisagé lors d'une version future.


#Architecture de la solution#
Yann s'en occupe

##Site Central##
Le site central a pour rôle de centraliser les informations remontant des différents sites, et de superviser les sociétés de maintenance après analyse de ces informations. L'architecture proposée privilégie la fiabilité et anticipe sur les besoins non fonctionnels de scalabilité de la solution.

La solution proposée pour le stockage d'informations s'appuie sur une base de donnée relationnelle centralisant les données. Le support matériel de cette base de données est redondant, afin de palier à d'éventuelles pannes et/ou pertes de données.

<span style="color:#FF0000">A COMPLETER AVEC LES REFERENCES ET DETAILS</span>


##Site Isolé##


L'architecture du site central se devait répondre aux défis suivants:
 * assurer l'autonomie énergétique du système
 * permettre un relevé fiable des informations
 * effectuer un premier contrôle sur les mesures, et prévenir le site central en cas d'anomalie
 * faire remonter régulièrement l'ensemble des données collectées sur le site

###Autonomie Énergétique###

L'autonomie énergétique est proposée sous deux formes différentes. La première, la solution applicable dans la plus part des cas, se base sur l'exploitation du potentiel éolien de la Norvège. On y associe une éolienne domestique modeste à une batterie tampon adaptée. Cette solution à été calibrée au regard de statistiques météorologiques afin d'assurer une autonomie totale et continue.

 * Éolienne sélectionnée: [Ultimate Aire One 600](http://toutlesolaire.com/p/Eolienne-24V-600W-Ultimate-Aire-One-/1500.html)  
 * Batterie sélectionnée: [GEL MOLL OPzV 1530Ah 2V](http://www.apb-energy.fr/boutique/fiche_produit.cfm?ref=MOLL-OPZV-1530&type=175&code_lg=lg_fr&num=181)


Du fait de la dépendance totale de cette première solution vis à vis des caractéristiques du site, on propose une seconde solution, générique, et pouvant être installée partout. Cette solution s'appuie sur l'optimisation différentielle d'une batterie de forte capacité. Cette dernière étant l'unique "source" d'énergie dans ce cas, on lui adjoint une résistance chauffante afin de réguler sa température, et ainsi maximiser sa rétention d'énergie tout en essayant de minimiser l'énergie gaspillée en chauffage. Dans l'optique de conserver au maximum la chaleur, on placera l'ensemble dans une enceinte thermique. Le tout est contrôlé par une brique logicielle spécifique qui fonctionne sur un micro-contrôleur qui lui est dédié.

 * Enceinte isotherme sur mesure, partenaire potentiel: [SMCI](http://www.klege-europ-smci.com/)  
 * Résistance chauffante: [HP04-1/04-24](http://fr.farnell.com/dbk/hp04-1-04-24/resistance-chauffante-ptc-20w/dp/4408329)  
 * Micro-contrôleur dédie: voir partie *Système Embarqué*  
 * Batterie sélectionnée au cas par cas.  

###Capteurs et Communication intra-site###

On veut relever 3 grandeurs dans les cuves: le pH, la température, et le niveau de remplissage. Les capteurs sélectionnés sont en accord avec les contraintes propres aux sites isolés (températures de fonctionnement, consommation réduite...).

<span style="color:#FF0000">A COMPLETER AVEC LES REFERENCES</span>

###Système Embarqué###

Le système embarqué a pour rôle de recueillir les mesures, les stocker temporairement avant de les transmettre au site central. Une première analyse visant à détecter d'importants sauts dans les valeurs est également souhaitée, un écart brutal vis-à-vis des valeurs précédentes étant souvent le symptôme d'une anomalie.  
Le micro-contrôleur sélectionné remplit parfaitement les besoins mentionnés ci-dessus quelle que soit la dimension du site considéré, mais également les autres cas d'utilisation envisagés (micro-contrôleur dédié au calcul différentiel, micro-contrôleur de communications radio...). Il consomme par ailleurs très peu d'énergie et est proposé à un prix négligeable. Dans le cas du système embarqué, on adjoint à ce micro-contrôleur une mémoire externe, nécessaire au stockage temporaire des données relevées.

 * Micro-contrôleur générique à tout le système: [MSP430F2370](http://www.ti.com/product/msp430f2370)  
 * Mémoire externe: [Spansion S25FL512S](www.spansion.com/Support/Datasheets/S25FL512S_00_02_e.pdf)



###Communications###

Au vu de l'isolement des sites, nous avons opté pour le seul moyen de transmettre les données disposant d'une couverture géographique adéquate et de caractéristiques satisfaisantes, les communications satellitaires. L'antenne sélectionnée propose un compromis adapté à notre situation, car elle présente un diamètre important tout en ne nécessitant pas l'installation du socle en béton propre aux antennes de plus grandes dimensions. Les bonnes caractéristiques associées aux antennes de cette dimension permettent l'utilisation d'une unité de transmission/réception de 5W seulement.

Antenne sélectionnée [Prodelin 1,8m](à renseigner!) 
Émetteur / récepteur sélectionné: [Emm/recept 5W](à renseigner!) 

<span style="color:#FF0000">MODELE / LIEN à renseigner</span>



#Sous système détaillé#
