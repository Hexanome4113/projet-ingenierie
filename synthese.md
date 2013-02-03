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
Afin de récupérer les données enregistrées par les différents capteurs installés sur les sites distants, une transmission devra être effectuée entre ces capteurs et un système embarqué présent sur le site.
##Transmission des données au serveur central##
Pour que les personnes présentes sur le site central puissent obtenir les données recueillies sur le site distant, il faut pouvoir établir une communication entre les deux. 
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
#Sous système détaillé#
