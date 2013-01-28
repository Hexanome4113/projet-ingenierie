*consignes:*

*pour chaque aspect technique, proposer une ou plusieurs solutions (souhaitable) justifiées. Dans le cas de multiples possibilités, exprimer très clairement les critères de choix pour l'une ou l'autre des possibilités.*

*Quantifier les besoins en énergie du dispositif en [ampère-heure](http://fr.wikipedia.org/wiki/Amp%C3%A8re-heure), par unité (si nécessaire) et par jour.*

*Par exemple: Communication ponctuelle par wifi toutes les 2H, 200 mAH /borne/jour*


1. Site central
===============


2. Site isolé
=============

a. Capteurs
-----------

<dl>
  <dt>Introduction</dt>
  <dd>
  Pour permettre une transmission des informations au site central, les données récupérées par les capteurs devront tout d'abord être transmises 
   au système embarqué. Pour cela, il y a deux problématiques principales auxquelles il faut répondre : gérer la transmission des données, et s'assurer
   de l'apport en énergie aux différents appareils.
   
  Diverses contraintes rendent ces opérations difficiles : la taille des sites (faisant de 100m à 1km, ce qui fait une distance importante entre le système embarqué
   et les capteurs), le relief accidenté des sites, et le froid reignant dans le nord de la Norvège.
  </dd>
  <dd>
  Répondre à ces exigences peut se faire de plusieurs façon différentes, présentant chacun des avantages et inconvénients. Pour les différencier,
   nous allons notamment prioriser les tâches selon les exigences non-fonctionnelles auxquelles elles répondent. La COPEVUE ayant placé comme facteur
   primordial l'autonomie de notre installation, nous nous baserons donc sur ce facteur en priorité.
  </dd>
  
  <dt>Solution retenue</dt>
  <dd>
  La solution nous ayant paru la plus pertinente est la suivante :</dd>
</dl>
  
  ![Proposition retenue](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/Solution_retenue.png)
  
<dl>
  <dd>
  Cette solution consiste à installer un système embarqué sur le site et à le relier directement à chacune des cuves par des cables électriques
  </dd>
  <dd>
  Les principaux avantages de cette solution résident dans son utilisation peu coûteuse ; Ses capteurs étant directement reliés au réseau, 
   il n'y a pas besoin de source d'énergie autre que celle du système embarqué. De plus, son nombre limité d'appareils limite les risques de pannes 
   et donc de coupure du réseau et de frais de maintenance.
  </dd>
  <dd>
  L'énergie dépensée pour chaque cuve dans ce genre d'installation est minime : il suffit en effet d'avoir assez d'énergie pour faire fonctionner les capteurs, ce qui correspond 
   pour chacun à l'équivalent d'une pile AAA par an si on effectue une mesure par heure.
  </dd>
  <dd>
  Cette approche présente cependant un certain nombre de limites, notamment celle liées à la complexité d'installation. En effet, le système embarqué pouvant
   être assez éloigné des cuves, il faudra parfois tirer un cable de 1km, pouvant poser des difficultés d'installation (et des frais importants) en fonction
   des terrains. Ces frais résultent de deux facteurs : le premier est le coût matériel, c'est à dire le cable électrique, et le second vient du temps passé par
   des ouvriers qualifiés qui se traduit par un salaire à verser. Ces ouvriers (qu'on considère comme qualifiés, et auxquels on attribue un salaire de 13 euros l'heure)
   passeront en effet un temps fixe pour chaque cuve pour l'installation des capteurs et leur raccordement (on estime à 2 heures le temps passé par cuve), ce à quoi il faut rajouter
   un temps variable en fonction de la distance de la cuve au système embarqué qu'ils passeront pour tirer le cable et s'assurer qu'il ne risque rien.
  </dd>
</dl>
   __Par cuve__ : ~ 150€ + 100€/100m

  - phMètre : gamme moyenne 55€
  - thermomètre : gamme moyenne 40€
  - niveau : gamme moyenne 30€
  - cables : 10€ + 80€ / 100m _PH: je pense que cette valeur est exagérée, j'ai réussi à trouver du cable à 23&nbsp;€/100&nbsp;m&hellip;_
  - main-d'oeuvre : 2h/homme + 2h/homme/100m -> 25€ + 25€/100m
<dl>
  <dt>Solution alternative</dt>
  <dd>
  Pour palier au relatif manque d'efficacité de la solution retenue dans certains cas, nous pouvons proposer une solution alternation dont l'architecture serait la suivante :
  </dd>
</dl>

  ![Proposition alternative](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/Solution_alternative.png)
  
<dl>
  <dd>
  Cette solution consistant à installer une borne radio (reliée aux différents capteurs) par cuve permettant de communiquer avec le système embarqué et un récepteur du côté du système embarqué a l'avantage d'avoir des coûts fixes : on ne payera pas plus cher 
   pour une cuve éloignée de 1km que pour une éloignée de 20m. Cette solution présente un problème de consomation d'énergie : n'étant pas reliée au site, elle doit comporter avec l'émetteur et le microcontrôleur une batterie pour faire fonctionner 
   non seulement les capteurs mais aussi les appareils de communications. De plus, un peu d'énergie sera gaspillée pour réchauffer ces appareils afin d'éviter que le froid ne les empêche de fonctionner.
  </dd>
  <dd>
  Pour économiser l'énergie passant dans la communication, nous avons prévu de mettre en place des fenêtres de temps au cours desquelles la radio emettra les données des capteurs. Nous avons ainsi estimé que l'appareil ne devrait fonctionner
   que 2 minutes par heures pour pouvoir envoyer des données suffisantes au système embarqué. Au niveau du chauffage, l'économie se fera grâce à une isolation efficace des appareils : nous avons déterminé qu'un abri en polyuréthane serait suffisant pour que
   le chauffage ne doive fonctionner qu'une moyenne de 10 minutes par jour. Au vu de ces données, nous estimons le temps d'autonomie de chaque cuve munie d'une batterie adaptée à environ 1 an, ce qui laisse un délai résonnable pour le changement de batterie.
  </dd>
  <dd>
  L'avantage principal de cette solution est sa facilité d'installation et un coût relativement limité lors de la pose sur des cuves éloignées du système embarqué. Cependant, elle présente de nombreux points limitant son utilisation : pour commencer,
   elle n'est rentable qu'à partir d'une certaine distance, une communication par ondes n'étant bien évidement pas nécessaire pour des cuves situées à 10m du système embarqué. Ensuite, cette solution pose un problème d'autonomie des appareils : en effet,
    les capteurs n'étant plus reliés électriquement au site, il doivent trouver une source d'énergie autre. Pour celà, l'utilisation d'une batterie peut s'avérer concluante, mais nécessite tout de même un changement occasionnel. Cependant, des accords
	avec les sociétés de maintenance pourraient être trouvés : le système leur permettant d'économiser des trajets, celles-ci pourraient faire un geste et s'occuper du changement des batteries annuel sans modification du contrat. Le dernier problème de cette
	solution peut venir de la configuration du site : le terrain peut être accidenté et gêner la progression des ondes. Par ailleurs, le froid risque de geler les appareils de transmission, des mesures (assez coûteuses) devant être prises pour éviter cela.
  </dd>
  <dd>
  Pour ce type d'installation, le coût fixe de la main d'oeuvre sera plus élevé : en effet, en plus de l'installation des capteurs, il faudra du temps aux ouvriers pour s'assurer de l'isolation de l'émetteur (et du microcontroleur) et de leur bon fonctionnement. 
  </dd>
</dl>
__Par cuve__ : ~ 550€ + 30€/an

  - emetteur : longue portée 60€
  - MSP430 (ou équivalent) 10€ _PH: De même, on peut trouver des MSP430 à l'unité pour quelques dollars, alors en commande groupée de plusieurs centaines&hellip;_
  - phMètre : gamme moyenne 55€
  - thermomètre : gamme moyenne 40€
  - niveau : gamme moyenne 30€
  - cables : 10€
  - batterie : 30€/ an
  - isolation : 200€ (polyurethane) 
  - chauffage : 50€
  - main-d'oeuvre : 4h/homme -> 50€
  
__Site__ : ~ 50€
  - Récepteur radio : 30€
  - fil : 3€
  - main d'oeuvre : 1h/homme : 15€
<dl>
<dt>Conclusion</dt>
  <dd>Bien que la première solution semble plus intéressante, il peut être pertinent de la combiner dans certains cas à la seconde pour une plus grande souplesse et une économie conséquente.
</dl>

b. Energie
----------

 **Introduction**

Le système nécessite la mise en place d'une solution d'alimentation autonome pour les sites isolés n'ayant pas accès à une source d'énergie exterieure. Le système ayant besoin d'une alimentation continue et de faible puissance, il semble indispensable d'avoir recours à une batterie pour faire tampon, quelle que soit la source d'énergie utilisée. La principale contrainte de fonctionnement d'une batterie est la temperature ambiante, en l'occurence ici les températures sur site peuvent descendre jusqu'à des extrèmes de -40°C, ce qui limite drastiquement le rendement de n'importe quelle batterie du marché.


Le problème de la source d'énergie en elle-meme est contraint par les conditions géographiques et météorologiques du site. Une allimentation photovoltaïque est inenvisageable du fait de la très forte variabilité des durées d'ensoleillement des régions concernées. L'exploitation de la biomasse environnante est également innapropriée, car les régions concernées sont potentiellement désertiques et la mise en fonctionnement d'un tel dispositif nécessite l'intervention d'un opérateur. Finalement, les solutions hydroélectriques sont contraintes par la disposition géographique des sites qui sont pour la plupart éloignés des côtes. De plus, les puissances développées par les systèmes hydroélectriques sont largement supérieures aux besoins de notre système.

Après revue des différentes alternatives, la seule solution restante pour générer de l'énergie sur place est l'éolien. Cette solution est particulièrement bien adaptée à de faibles puissances comme en témoigne l'utilisation de plus en plus fréquente de ces technologies dans des contextes domestiques. De plus, la norvège possède un très fort potentiel éolien, avec des vents suffisament forts et réguliers. La carte ci-dessous montre que pour la majorité des sites envisageables, le vent est suffisant car superieur en moyenne au minimum de 4km/h que nécessite la plupart des éoliennes.


![windmap](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/windmap.png "carte des vents du nord de la Norvège")

On constate que quelques zones ne réunissent pas les conditions recquises par l'éolien: on proposera donc une solution de secours pour ces quelques cas particuliers.

**Solution standard: Eolien & Batterie tampon**

La solution standard s'appuie donc sur la génération d'énergie par l'intermédiaire d'une éolienne de capacité adaptée. Les aléas météorologiques ne permettant pas une alimentation continue, nous adjoindrons à cette source d'énergie une batterie de capacité limitée, supposée apte à subvenir seule aux besoins du système pendant 2 jours complets. Le rendement de cette batterie sera mauvais du fait des conditions de température, mais ce n'est pas un problème si l'on considère qu'elle n'a pour seul rôle que de faire tampon entre l'éolienne et le système. L'accent sera mis sur le choix d'une batterie adaptée à ces conditions.

Par ailleurs, l'éolienne devra être légèrement surdimentionnée afin de permettre un rechargement rapide de la batterie quand les conditions météo sont favorables.


**Solution alternative: Optimisation différentielle d'une batterie de forte capacité**

Dans le cas où la localisation d'un site n'offre aucune prise au vent suffisante pour y placer une éolienne, on propose la solution exceptionnelle décrite ci-dessous. Il est important de noter que cette solution est plus onéreuse, offre de moins bons rendements et une autonomie moins forte que la solution standard présentée précédemment. Sa mise en place doit donc se limiter exclusivement aux cas où la solution standard ne serait pas applicable.


![alternative](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/energie-sol-alternative.png "schéma de la solution alternative")

Le principe général de la solution est de maintenir la batterie à une température permettant un rendement acceptable, tout en limitant la consommation du dispositif de chauffage au minimum. Dans cette optique, on place l'ensemble des composants electroniques centraux (système embarqué notamment) dans une enceinte limitant les échanges de chaleur avec l'exterieur, le but étant également de rentabiliser la dissipation thermique de ces derniers. L'appoint de chauffage est rendu possible par l'intégration d'une résistance alimentée par la batterie elle-meme. L'activation de cette résistance est contrôlée par une brique logicielle fonctionnant sur le système embarqué, dont l'objectif est de déterminer la meilleure stratégie à adopter pour préserver l'énergie emmagasinée dans la batterie malgré les conditions de température. Pour que cette optimisation soit possible, il faut au préalable avoir caractérisé précisément le rendement de la batterie en fonction de la température, le rendement de la résistance, ainsi que les caractéristiques thermiques (inertie, fuites...) de l'enceinte. En se basant sur ces données initiales et sur les relevés de température à l'intérieur du boitier, la brique logicielle est capable, par la résolution d'un système différentiel complexe, de déterminer cette stratégie optimale de chauffage. L'implémentation de ce système dans son ensemble (choix des composants les plus adaptés, étalonnage, développement de la brique logicielle...) ne sera pas détaillé ici, mais nos équipes disposent de l'expertise nécessaire à la mise en place d'un tel dispositif.

Certaines contraintes apparaissent du fait de l'utilisation de cette solution alternative. Il faudra notamment surveiller à distance le niveau de la batterie afin d'anticiper les pannes d'énergie. Par ailleurs, l'autonomie n'étant que partielle, les intervenants des sociétés de maintenance devront être mis à partie pour remplacer les batteries vides par des batteries chargées lors des interventions. Cela implique une formation supplémentaire (succinte mais nécessaire) de ce personnel intervenant, et le developpement des aspects logistiques et techniques nécessaires au rechargement des batteries échangées.


c. Système embarqué et système de communication avec le site central
--------------------------------------------------------------------

### Introduction ###

Le système embarqué se doit d'assurer trois fonctions principales&nbsp;:

- recueillir les données envoyées par les capteurs, les regrouper par cuves, les dater, en bref, les identifier&nbsp;;

- envoyer les données vers le site central lorsque la liaison est disponible&nbsp;;

- stocker les données lorsque la liaison avec le site central n'est pas disponible.

Le système assurera également, dans certains cas, une fonction auxiliaire&nbsp;: le contrôle de la température de l'enceinte thermique.

Ces fonctionnalités sont prises en charge par les trois composants du système embarqué&nbsp;: le microcontrôleur, le système de liaison et la mémoire externe.

### Microcontrôleur ###

Il est important de noter que les données reçues par le microcontrôleur de la part des capteurs sont déjà toutes numériques. Sa tâche principale se résume donc à contextualiser des données (c'est-à-dire leur associer un identifiant), et rediriger l'information résultante vers l'un de ses deux périphériques, soit le système de liaison, soit la mémoire externe.

La régulation de la température est elle plus complexe. D'autre part, cette brique logicielle n'est nécessaire que lorsque le système embarqué est installé dans une enceinte thermique, c'est-à-dire dans le cas (considéré comme rare) où une source d'énergie éolienne n'est pas disponible (voir _Solution alternative_ dans _[b. Energie](#b-energie)_).

Pour cette raison, et parce que cette fonction, qui n'est pas liée à la satisfaction d'une exigence fonctionnelle, risque d'interférer avec la tâche principale du microcontrôleur, cette brique logicielle s'exécute sur un microcontrôleur dédié. La carte correspondant au système embarqué est donc déclinée en deux versions, selon la solution d'alimentation retenue, avec un ou deux microcontrôleurs.

#### Microcontrôleur de transmission des données ####
Comme dit précédemment, ce microcontrôleur assure une tâche simple. En s'appuyant sur la partie _[a. Capteurs](#a-capteurs)_, on peut déterminer que le débit de données que devra traiter ce microcontrôleur est de . En effet, la fréquence de mesure choisie est de une mesure par cuve par heure. On fait l'hypothèse ici que cette mesure engendre une transmission de huits octets vers le système embarqué et que les mesures ont toutes lieues à des instants différents (pas de phénomène de pic). En considérant un site isolé de 50 cuves (légère surrestimation par rapport aux plus grands sites) avec chacune 10 capteurs, cela représente donc un volume de 4000 octets à traiter par heure, soit 1,11 octets par seconde. Par sécurité, le traitement à appliquer à une mesure doit donc se faire dans tous les cas en moins d'une demi seconde. Compte tenu des performances actuelles des microcontrôleurs sur le marché, cette obligation n'est pas un facteur limitant, puisque virtuellement n'importe quel microcontrôleur convient pour remplir une tâche aussi peu demandeuse de performance.

Le choix du microcontrôleur ne peut donc reposer sur un critère de performance. Il doit donc reposer sur les critères suivants, identifiés comme les plus importants lors de l'analyse des besoins et du receuil des exigences&nbsp;: l'efficacité en terme de consommation de la solution proposée, afin de maximiser l'autonomie du système. Il s'agit là d'un objectif d'autant plus important qu'une solution très économe en énergie a déjà été trouvée pour les capteurs, et que dans le cas de l'alimentation alternative sur batterie uniquement, l'autonomie est un besoin encore plus crucial.

#### Microcontrôleur de régulation de la température ####

### Système de liaison ###

### Mémoire externe ###

d. ...
------


3. Communication avec les sociétés de maintenance
=================================================

À chaque site isolé correspond une société de maintenance (la plus proche pouvant répondre à ses besoins) pour demander des interventions.
Ces demandes d'intervention vont être maintenant générées par un service du serveur central et transmises par celui-ci à la société de maintenance concernée.
Ces demandes d'intervention seront transmises par l'envoi d'un document par mail (ou par fax) pour donner les détails de l'intervention et par un appel téléphonique afin de vérifier la disponibilité de la société de maintenance et de connaître leur réponse quant à l'intervention.
Après lecture du document de demande d'intervention la société de maintenance enverra par mail (ou par fax) un document de réponse au serveur central.
Une fois que l'intervention est effectuée, le technicien ayant effectué la maintenance enverra un document de compte-rendu au serveur central.

![Schéma Intervention par une société de maintenance](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/DiagrammeDActivitCommunicationAvecLesSociTSDeMaintenance.png "Schéma Intervention par une société de maintenance")

###Moyens de communication

Le service de demande d'intervention de maintenance doit gérer plusieurs demandes venant de différents sites isolés et donc à destination de différentes sociétés de maintenance.
Toutes les sociétés de maintenance ne fonctionnement pas forcément de la même manière avec les mêmes outils. Ici ce sont les moyens de communication de chaque société de maintenance qui sont à prendre en compte.
La communication privilégiée avec les sociétés de maintenance sera le mail et le téléphone, comme expliqué précédemment. Mais dans le cas où la société de maintenance ne peut pas être contactée par email, l'envoi des documents sera effectué par fax afin de garder l'avantage de la réception immédiate.
L'envoi par courrier n'est pas envisageable à cause des délais de livraison et les éventuelles difficultés d'acheminement.

Une seule et même personne du service d'intervention de maintenance s'occupera de créer le document de demande d'intervention, de l'envoyer et de contacter la société de maintenance par téléphone.
Si la société de maintenance n'est pas disponible cette personne recherchera une autre société de maintenance faisant partie du système, contactera la propriétaire du site isolé concerné pour lui demander l'accord de changer de société de maintenance ponctuellement, et ensuite effectuera la même procédure à destination de cette nouvelle société de maintenance.
Cependant si aucune société de maintenance faisant partie du système n'est présente dans un rayon de 100 km du site isolé, la personne chargée de cette demande d'intervention cherchera une nouvelle société de maintenance dans le secteur géographique si le niveau de gravité de l'intervention demandée est élevé, sinon la demande d'intervention sera reportée jusqu'à la disponibilité de la société de maintenance atitrée.

###Formalisme de communication

Tous les documents sus-cités devront suivre un certain formalisme. Un listing détaillé des informations nécessaires que doivent contenir ces documents est présenté ci-dessous.

**Document de demande d'intervention (envoyé par le serveur central vers la société de maintenance) :**
 - Date et heure de la demande
 - Coordonnées du site isolé concerné
 - Coordonnées du propriétaire du site isolé
 - Coordonnées du serveur central
 - Liste des évènements à traiter avec leur degré de gravité
 - Description de l'alerte et son degré de gravité (l'association de plusieurs évènements ayant une gravité mineure peut engendrer une alerte de niveau élevée)

**Document de réponse à la demande d'intervention (envoyé par la société de maintenance au serveur central avant l'intervention) :**
 - Date et heure du traitement de la demande
 - Date, heure et durée de l'intervention prévues
 - Coordonnées du site isolé concerné
 - Coordonnées de la société de maintenance
 - Liste des interventions à effectuer
 - Liste des évènements, parmi ceux de la demande d'intervention, qui seront traités
 - Liste des évènements, parmi ceux de la demande d'intervention, qui ne seront pas traités (peut être vide) et les raisons de ces non-maintenances
 - Coût de l'intervention prévu (s'il s'agit d'un contrat forfaitaire il faut préciser que cette intervention n'est pas facturée mais comprise dans le forfait, ou préciser les surcoûts)

**Document de compte-rendu de l'intervention (rédigée par le technicien de maintenance, envoyée par la société de maintenance vers le serveur central) :**
 - Date, heure et durée de l'intervention
 - Nom du technicien de maintenance ayant effectué l'intervention
 - Coordonnées du site isolé concerné
 - Coordonnées de la société de maintenance
 - Liste des interventions, parmi ceux prévus dans la réponse à la demande d'intervention, traitées
 - Liste des interventions, parmi ceux prévus dans la réponse à la demande d'intervention, non traitées et raisons de ces non-traitements
 - Liste des interventions traitées non prévues et raison de ces interventions
 - Observations et remarques (concernant l'état, l'entretien, la gestion et la maintenance du site isolé)
 - Coût de l'intervention final (augmentation possible si interventions effectuées non prévues)

