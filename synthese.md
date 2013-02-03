#Synthèse#
Ceci est une synthèse, donc on ne crée pas d'information.
Elle doit faire au max 6 pages.
On doit avoir à peu pres 3 fois ça dans le git, donc pas besoin de faire du pipeau : on veut des info pertinentes justifiées et interessantes
#Rappel de l'appel d'offre#
Thibaut : _Bon allez j'me charge de cette partie_

L'appel d'offre que nous allons étudier dans ce projet a été lancé par la COPEVUE, (un organisme regroupant des propriétaires de sites distants (à corriger quand j'aurai le sujet)), qui souhaite pouvoir monitorer à distance un ensemble de sites difficilement accessibles. Ces différents sites distants sont actuellement surveillés directement par leur directeur, ce dernier passant de manière occasionnelle quand il en a le temps, ce qui reste assez rare en raison de l'innaccessibilité de ces sites. La mission proposée par l'appel d'offre consiste donc à automatiser cette surveillance en transmettant des données automatiquement à un site central afin de permettre une réaction beaucoup plus rapide en cas d'accident et une optimisation des coûts de maintenance.

L'exigence principale de cet appel d'offre est l'automie de la solution apportée. En effet, il faut qu'elle fonctionne sans (presque) aucune intervention humaine. La solution proposée devra aussi répondre à certains problèmes provoqués par l'environnement dans lequel ces sites sont situés. La solution apportée devra être générique et pouvoir s'adapter à différents types de terrains. Dans l'exemple traité, les sites seront situés au nord de la Norvège et feront une taille variant d'un diamètre de 100m à 1km. Ces sites comporteront un nombre variable de cuves de liquide nécessitant chacune jusqu'à 3 capteurs : un ph-mètre, un thermomètre et un contrôleur de niveau. Dans cette exemple, la contrainte la plus forte vient du froid qu'il règne souvent dans cette région, rendant inefficaces certaines solutions.

#Recueil des exigences#
Thibaut : _Bon allez de celle là aussi_

Afin d'avoir une vision plus précise des exigences de l'appel d'offre, nous avons effectué une analyse plus approfondie de ce dernier en se concentrant sur les problèmes soulevés par ces exigences. Les principaux problèmes identifiés sont les suivants :

##Acquisition des données sur le site distant##
Pour récupérer les données, différents capteurs seront installés sur chacun des sites. Cependant, pour des raison de coût et d'économie d'énergie, il est évident que chaque capteur ne pourra être équipé d'un dispositif permettant de communiquer avec le site central. Il est donc nécessaire de regrouper les informations du site distant dans une seule unité qui sera chargée de communiquer avec le site central. Cette unité sera composée d'un dispositif de communication et d'un système embarqué permettant de contrôler ces communications. Pour celà, il faut déterminer plusieurs choses : en premier lieu, réussir à trouver un matériel fonctionnant dans les conditions imposées (froid, éloignement entre la cuve et le système embarqué, topologie du terrain...) à la fois pour le système embarqué et pour les cuves; en second lieu, trouver une architecture et une stratégie de communication entre capteurs et système embarqué permettant de limiter leur dépense en énergie tout en ayant des mesures suffisamment fréquentes pour pouvoir être exploitées au niveau du site central.

##Transmission des données au serveur central##
Pour que les personnes présentes sur le site central puissent obtenir les données recueillies sur le site distant, il faut pouvoir établir une communication entre les deux. Cet aspect englobe à la fois la communication en elle même (non seulement l'aspect matériel, mais aussi le protocole et la fréquence), la gestion des problèmes (reprise de communication en cas de rupture) et l'enregistrement de traces portants sur les mesures effectuées.

##Génération des demandes de maintenance##
L'intéret principal du dispositif demandé par l'appel d'offre est de pouvoir savoir très facilement si l'intervention d'une société de maintenance est nécessaire et si oui, les opérations à effectuer. Pour celà, chaque site dispose d'une base de règles qui lui est propre : ces règles identifient les différents problèmes et les réponses à y apporter selon leur gravité et leur nombre, certains problèmes n'étant pas critiques et ne nécessitant pas de maintenance dédiée. Pour déterminer quand une maintenance doit être effectuée, une solution consiste à générer des alertes lorsque des données anormales apparaissent. La génération d'alerte entrainerait les besoins suivants :

###Création de la stratégie d'alertes###
Une stratégie de gestion des alertes doit être définie une fois pour l'ensemble des sites. Elle devra définir plusieurs niveaux de gravité d'alerte, qui entraineront plus ou moins vite une demande de maintenance. Par la suite, un ensemble de règles devra être défini pour chaque site distant, associant à chaque problème potentiel un niveau de gravité.

###Création d'une alerte###
La création automatique des alertes devra se faire au niveau du site central. C'est lui qui déclenchera une alerte en fonction des données transmises (ou de l'absence de données) par le site distant. Ces alertes génèreront ensuite une demande de maintenance si nécessaire. En parallèle des alertes automatiques, la possibilité de déclenchement d'une alerte manuelle par le directeur du site s'il constate une anomalie devra être prévue. Cette alerte devra être traitée et évaluée par un responsable du site central afin de déterminer si elle est valide ou non et de l'évaluer en cas de réponse positive.

###Transmission d'une demande de maintenance###
Une fois des alertes nécessitant une maintenance reçues, il reste à contacter la société de maintenance qui s'occupe du site distant concerné. Il faudra prévoir les modalités de communication avec ces sociétés (par téléphone ou email, selon leurs préférences).


#Architecture de la solution#
Yann s'en occupe
#Sous système détaillé#
