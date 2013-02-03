#Synthèse#
Ceci est une synthèse, donc on ne crée pas d'information.
Elle doit faire au max 6 pages.
On doit avoir à peu pres 3 fois ça dans le git, donc pas besoin de faire du pipeau : on veut des info pertinentes justifiées et interessantes
#Rappel de l'appel d'offre#
Thibaut : _Bon allez j'me charge de cette partie_

L'appel d'offre que nous allons étudier dans ce projet a été effectué par la COPEVUE, (un organisme regroupant des propriétaires de sites distants (à corriger quand j'aurai le sujet)), qui souhaite pouvoir monitorer à distance un ensemble de sites difficilement accessibles.
Ces différents site sont actuellement surveillés directement par leur directeur, ce dernier passant de manière occasionnelle quand il en a le temps, ce qui reste assez rare en raison de l'innaccessibilité de ces sites. La mission 
proposée par l'appel d'offre consiste donc à automatiser cette surveillance en transmettant des données automatiquement à un site central afin de permettre une réaction beaucoup plus rapide en cas d'accident et une optimisation des coûts de maintenance.

L'exigeance principale de cet appel d'offre est l'automie de la solution apportée. En effet, il faut qu'elle fonctionne sans (presque) aucune intervention humaine. La solution proposée devra aussi répondre à certains problèmes provoqués par l'environnement dans lequel ces sites sont situés, c'est à dire le nord de la Norvège. La plus importante vient du froid qu'il règne souvent dans cette région,
rendant innefficaces certaines solutions.

#Recueil des exigences#
Thibaut : _Bon allez de celle là aussi_

Afin d'avoir une vision plus précise des exigences de l'appel d'offre, nous avons effectué une analyse plus approfondie de ce dernier en se concentrant sur les problèmes soulevés par ces exigences. Les principaux problèmes identifiés sont les suivants :
##Acquisition des données sur le site central##
Afin de récupérer les données enregistrées par les différents capteurs installés sur les sites distants, une transmission devra être effectuée entre ces capteurs et un système embarqué présent sur le site.
##Transmission des données au serveur central##
Pour que les personnes présentes sur le site central puissent obtenir les données recueillies sur le site distant, il faut pouvoir établir une communication entre les deux. 

##Génération des demandes de maintenance##
###Création d'une alerte###
###Transmission d'une demande de maintenance###
#Architecture de la solution#
#Sous système détaillé#
