
1. Site central
===============

Traffic attendu
---
Au niveau du serveur central, on s’attend à faire face à 40 gros sites (surestimation de la situation actuelle) ce qui représentera un flux de 10,4 mo de trafic pour un mois (calcul effectué sur la base décrite dans la suite du document).

En configurant les sites distants pour qu’ils ne se connectent par tous au même instant au site central, on évite les pics de transferts et de connections simultanées.

Également, le site central échangera des données avec les sociétés de maintenance (pour des demandes de maintenance ainsi que pour en recevoir les rapports). Ces échanges sont assez peu fréquents et peu gourmands en masse de données.

Pour ces raisons, le site central peut tout à fait se contenter d’une simple connexion ADSL, même si pour des raisons pratiques, un accès fibré est à privilégier.

Base de données
---

En supposant qu’on stocke en base de données une valeur de 4 octet pour chaque message de capteur reçu, cela nous donne environ 10 mo par mois à stocker, auxquelles il faut rajouter toutes les informations d’ID, de relations, d’indexation, etc, ainsi que les données issues des échanges avec les sociétés de maintenance.

D’autres données métiers peuvent être amenées à être stockées en base de données, mais ne représentent qu’une fraction de la masse des données précédentes.

Avec une grande marge, un téraoctet de stockage paraît suffisants pour le stockage et la redondance. Cela représente en fin de compte très peu de données en comparaison de ce que les SGBD actuels sont capables de gérer (les performances étant grandement liées à son schéma et à sa configuration). Pour garantir des performances encore meilleures, il est envisageable d’utiliser des disques durs SSD.

Les principales opérations qui seront effectuées seront :
  - insertion d’une valeur d’un capteur en base de données
  - extraction des valeurs les plus récentes des capteurs pour vérifier l’état global des sites distants sur un tableau de bord
  - calculs intensifs sur l’ensemble de l’historique des valeurs de la base de donnée afin de :
    - déceler des défaillances fréquentes
    - évaluer l’intérêt d’intervenir sur certains sites afin de corriger des problèmes récurrents ou ayant de forts risques de se produire
    - renégocier des contrats concernant des opérations de maintenance inutilisées en pratique ou au contraire trop souvent utilisées

⇒ Car l’application requiert des opérations très complexes par moments, une base de donnée relationnelle est toute indiquée. Pour les dernières valeurs reçues pour chaque capteur, un stockage en RAM suffit (système de cache type Redis).

Architecture matérielle
---
![site central](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/Site_Central.png)

Au niveau de l’équipement matériel du site central, nous aurons besoin de :
  - un poste par employé (tour 175€, écran 75€)
  - un pare-feu permettant de faire respecter la politique de sécurité du réseau de l’entreprise (1000€)
  - un serveur web accessible depuis l’extérieur permettant aux entreprises de maintenance de saisir les détails des opérations de maintenance effectuées. Ne requiert pas de performances accrues. (200€)
  - un serveur pour la base de données, disposant d’importantes ressources (RAM, stockage), et d’un système de redondance pour éviter une perte de données. (2500€)
  - un serveur accédé par les systèmes embarqués des sites distants, a priori très peu gourmand en ressources mais devant assurer un service fiable et continu. Il sera donc doublé et protégé par le pare feu grâce à des règles strictes. (1000€)
  - un serveur web et d’application accédé par tous les clients légers des postes des employés, devant périodiquement effectuer des calculs complexes (aide à la décision) et par conséquent doté de ressources conséquentes, ce qui garantira sa faible charge et sa forte réactivité la majorité du temps. (2500€)
  - onduleurs, câbles, imprimante réseau, périphériques... (2000€)

Architecture applicative
---
Notre solution au niveau du site central se présente sous la forme d’un intranet auxquels se connectent les employés, leur offrant :
  - des tableaux de bord
  - un système de notification en temps réel des alertes remontées des sites distants ou des interventions sur site
  - des indicateurs
  - une visualisation des interventions demandées aux sociétés de maintenance
  - des demandes des propriétaires
  - la modification des règles de maintenance automatisée
  - la réalisation d’une action de maintenance manuelle
  - l’affichage de  statistiques sur la fiabilité, les interventions sur sites, sur les sociétés de maintenance, sur les propriétaires

Nous proposons également aux entreprises de maintenance partenaires de remplir les informations relatives à leurs interventions directement sur une interface web accessible depuis l’extérieur, plutôt que de les communiquer par mail ou téléphone à un agent du site central. Cette possibilité leur reste néanmoins accessible. C’est alors à l’agent lui même de remplir les informations sur l’intervention.

Cette solution intègrera notamment de puissantrs algorithmes d'aide à la décision adaptés à nos grandes quantités de données. Son coût de développement, mise en production et maintenance corrective et évolutive (sur 5 ans) est estimé à environ 30 000 euros.


Autres frais
---
### Fixes
  - fournitures diverses (300€)
  - mobilier (chaises, bureaux, luminaires, rangements) : (300€ + 100€/poste)
  - cafetière (100€)

### Forfaits
  - de jolis locaux à Limoges (70m², 600€/mois)
  - connexion internet haut débit (50€/mois)
  - nom de domaine (12€/an)
  - impôts et taxes divers et variés
  - salaires (1500€/employé)
  - edf, eau courante


Personnel
---
Sur le site central, nous aurons besoin d'employer le personnel suivant :
  - Un agent de maintenance sur place (peut-être deux, ou un vacataire, à voir), en charge de faire la maintenance logicielle (bd, site web, appel à une société en informatique externe pour les tâches les plus complexes, etc.) et matérielle (postes de travail, du parc informatique du site, commande de matériel, premier diagnostic en cas défaillance, appel à une société informatique externe pour la maintenance matérielle, suivi des réparations, etc.), responsable de la sécurité, de la gestion des comptes utilisateurs, aide et formation des utilisateurs aux outils.
  - Un agent de maintenance pour les sites distants pour assurer les mêmes fonctions de maintenance logicielle et matérielle que l’agent sur place, mais pour les sites distants
  - Une personne sur place pour prendre les appels/envoyer/répondre au(x) mails/courrier des propriétaires, des sociétés de maintenance, d’autres personnes (suivi de la relation)
  - Un Comptable/Responsable du service achat/approvisionnement/Suivi de la facturation des sociétés de maintenance/des propriétaires de sites
  - Des donneurs d’ordres aux sociétés de maintenance, pour traiter toutes les alertes non automatisées
  - Un directeur (peut-être avec une toute petite équipe de direction derrière lui de une ou deux personnes supplémentaires), responsable de la coordination site central/site distant, travail de management (coordination des équipes, réunions, planifications diverses)

Système des gestion des alertes
---
Un système d'aide à la décision pour la gestion des alertes est aussi présent dans le site central.
Ce système est un système à règles conditionnelles.
Il est primordial de renseigner les règles à considérer lors de la mise en place de notre système pour chaque site isolé.
Il est donc important de réunir les cadres et agents, de la société de maintenance comme du propriétaire du site, qui interviennent sur le site isolé en question afin de collecter toutes ces règles.

Ces règles seront de la forme :
SI _donnée dans un certain état_ ALORS EMETTRE UNE ALERTE POUR DEMANDER UNE INTERVENTION DANS UN DELAI DE _x à y jours_

Exemples de règles possibles :
- SI le niveau de liquide a baissé de 10 cm (depuis la dernière mesure donc la veille) ALORS émettre une alerte pour demander une intervention dans un délai de 0 à 6 jours.
- SI le degré pH du liquide est de 2 ALORS demander émettre une alerte pour une intervention dans un délai de 0 à 10 jours.

Certaines règles indispensables seront définies par l'architecture technique choisie sur le site isolé :
- SI une batterie du site est faible ou épuisée ALORS émettre une alerte pour demander une intervention immédiate.
- SI la communication satellite avec le système embarqué est coupée ALORS émettre une alerte pour demander une intervention immédiate.
- SI un capteur n'envoie plus de données ALORS émettre une alerte pour demander une intervention immédiate
- SI l'éolienne présente un défaut ALORS émettre une alerte pour demander une intervention immédiate
- ...

A la réception de nouvelles données venant d'un site isolé, ce système de gestion des alertes va appliquer toutes les règles établies aux données reçues.
Si une seule règle est rencontrée, le système demandera une intervention dans les délais demandés.
Mais si le système rencontre plusieurs règles, le système d'aide à la décision choisira de demander une intervention dans des délais convenants à toutes les règles activées.
Ce système considère aussi les alertes précédemment émises qui n'ont pas encore été rétablies par une intervention.
Si une telle alerte avait été émise avant la nouvelle le système vérifie la date d'intervention prévue pour cette précédente alerte.
Si cette date est entre dans les délais calculés pour la nouvelle alerte alors les deux alertes seront traitées dans la même intervention, sinon le système choisira la date la plus proche pour demander une intervention pour les deux alertes.

Ces alertes sont ensuite transmises au service de demande d'intervention de maintenance quelques jours avant la date d'intervention calculée.

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
   et les capteurs), le relief accidenté des sites, et le froid régnant dans le nord de la Norvège.
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
  Cette solution consiste à installer un système embarqué sur le site et à le relier directement à chacune des cuves par des câbles électriques
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
   être assez éloigné des cuves, il faudra parfois tirer un câble de 1km, pouvant poser des difficultés d'installation (et des frais importants) en fonction
   des terrains. Ces frais résultent de deux facteurs : le premier est le coût matériel, c'est à dire le câble électrique, et le second vient du temps passé par
   des ouvriers qualifiés qui se traduit par un salaire à verser. Ces ouvriers (qu'on considère comme qualifiés, et auxquels on attribue un salaire de 13 euros l'heure)
   passeront en effet un temps fixe pour chaque cuve pour l'installation des capteurs et leur raccordement (on estime à 2 heures le temps passé par cuve), ce à quoi il faut rajouter
   un temps variable en fonction de la distance de la cuve au système embarqué qu'ils passeront pour tirer le câble et s'assurer qu'il ne risque rien.
  </dd>
</dl>
   __Par cuve__ : ~ 325€ + 39€/100m

  - pH-mètre / thermomère : 260€ (Phmètre : Précision:+-0.02 pH )(Thermomètre : Précision:+-0.5°C)(Résistance: -20°C (pas trouvé mieux) / Consommation : 3 piles AAA / approximativement 1200 heures d'utilisation continue)
  - niveau : 31.50€ (consommation : 3V, 50mA)(Garantie : 3ans)(Résistance: pas réussi à en trouver un avec résistance au froid)
  - câbles : £11.76 (= 13,73€) / 100m : 
  - main-d'œuvre : nous avons estimé à environ 2h la moyenne de temps passé par un technicien pour tirer 100m de cable. Ces deux heures seront passées à tirer le cable de 100m, le raccorder à l'extrémité précédente, et le protéger / signaler. Comme dit précédemment, ce technicien sera payé aux alentours de 13€ de l'heure, d'où le calcul : 2h/homme + 2h/homme/100m -> 25€ + 25€/100m
<dl>
  <dt>Solution alternative</dt>
  <dd>
  Pour palier au relatif manque d'efficacité de la solution retenue dans certains cas, nous pouvons proposer une solution alternative dont l'architecture serait la suivante :
  </dd>
</dl>

  ![Proposition alternative](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/Solution_alternative.png)
  
<dl>
  <dd>
  Cette solution consistant à installer une borne radio (reliée aux différents capteurs) par cuve permettant de communiquer avec le système embarqué et un récepteur du côté du système embarqué a l'avantage d'avoir des coûts fixes : on ne payera pas plus cher 
   pour une cuve éloignée de 1km que pour une éloignée de 20m. Cette solution présente un problème de consommation d'énergie : n'étant pas reliée au site, elle doit comporter avec l'émetteur et le microcontrôleur une batterie pour faire fonctionner 
   non seulement les capteurs mais aussi les appareils de communications. De plus, un peu d'énergie sera gaspillée pour réchauffer ces appareils afin d'éviter que le froid ne les empêche de fonctionner.
  </dd>
  <dd>
  Pour économiser l'énergie passant dans la communication, nous avons prévu de mettre en place des fenêtres de temps au cours desquelles la radio émettra les données des capteurs. Nous avons ainsi estimé que l'appareil ne devrait fonctionner
   que 2 minutes par heures pour pouvoir envoyer des données suffisantes au système embarqué. Au niveau du chauffage, l'économie se fera grâce à une isolation efficace des appareils : nous avons déterminé qu'un abri en polyuréthane serait suffisant pour que
   le chauffage ne doive fonctionner qu'une moyenne de 10 minutes par jour. Au vu de ces données, nous estimons le temps d'autonomie de chaque cuve munie d'une batterie adaptée à environ 1 an, ce qui laisse un délai raisonnable pour le changement de batterie.
  </dd>
  <dd>
  L'avantage principal de cette solution est sa facilité d'installation et un coût relativement limité lors de la pose sur des cuves éloignées du système embarqué. Cependant, elle présente de nombreux points limitant son utilisation : pour commencer,
   elle n'est rentable qu'à partir d'une certaine distance, une communication par ondes n'étant bien évidement pas nécessaire pour des cuves situées à 10m du système embarqué. Ensuite, cette solution pose un problème d'autonomie des appareils : en effet,
    les capteurs n'étant plus reliés électriquement au site, il doivent trouver une source d'énergie autre. Pour cela, l'utilisation d'une batterie peut s'avérer concluante, mais nécessite tout de même un changement occasionnel. Cependant, des accords
	avec les sociétés de maintenance pourraient être trouvés : le système leur permettant d'économiser des trajets, celles-ci pourraient faire un geste et s'occuper du changement des batteries annuel sans modification du contrat. Le dernier problème de cette
	solution peut venir de la configuration du site : le terrain peut être accidenté et gêner la progression des ondes. Par ailleurs, le froid risque de geler les appareils de transmission, des mesures (assez coûteuses) devant être prises pour éviter cela.
  </dd>
  <dd>
  Pour ce type d'installation, le coût fixe de la main d'œuvre sera plus élevé : en effet, en plus de l'installation des capteurs, il faudra du temps aux ouvriers pour s'assurer de l'isolation de l'émetteur (et du microcontrôleur) et de leur bon fonctionnement. 
  </dd>
</dl>
__Par cuve__ : ~ 510€

  - émetteur : (longue portée) 89.99$ = 66.78€ (Consommation : 0.5W)(1 Year Common Sense Warranty on Transmitter, Lifetime Guarantee on Power Supply & Antenna)(Résistance au froid: c'est pour ça qu'il faut isoler)
  - MSP430 : 1.95€.
  - pH-mètre / thermomère : 260€ (Phmètre : Précision:+-0.02 pH )(Thermomètre : Précision:+-0.5°C)(Résistance: -20°C (pas trouvé mieux) / Consommation : 3 piles AAA / approximativement 1200 heures d'utilisation continue)
  - niveau : 31.50€ (consommation : 3V, 50mA)(Garantie : 3ans)(Résistance: pas réussi à en trouver un avec résistance au froid)
  - batterie : 22.90€ ((Capacité : 1400mAH)(on la recharge une fois par an)(Garantie 2 ans)
  - main-d'œuvre : 4h/homme -> 50€
  - caisson isolant : 80€ 
  
__Site__ : ~ 50€
  - Récepteur radio : 30€
  - main d'œuvre : 1h/homme : 15€
<dl>
<dt>Conclusion</dt>
  <dd>Bien que la première solution semble plus intéressante, il peut être pertinent de la combiner dans certains cas à la seconde pour une plus grande souplesse et une économie conséquente.
</dl>

b. Énergie
----------

 **Introduction**

Le système nécessite la mise en place d'une solution d'alimentation autonome pour les sites isolés n'ayant pas accès à une source d'énergie extérieure. Le système ayant besoin d'une alimentation continue et de faible puissance, il semble indispensable d'avoir recours à une batterie pour faire tampon, quelle que soit la source d'énergie utilisée. La principale contrainte de fonctionnement d'une batterie est la température ambiante, en l'occurrence ici les températures sur site peuvent descendre jusqu'à des extrêmes de -40°C, ce qui limite drastiquement le rendement de n'importe quelle batterie du marché.


Le problème de la source d'énergie en elle-même est contraint par les conditions géographiques et météorologiques du site. Une alimentation photovoltaïque est inenvisageable du fait de la très forte variabilité des durées d'ensoleillement des régions concernées. L'exploitation de la biomasse environnante est également inappropriée, car les régions concernées sont potentiellement désertiques et la mise en fonctionnement d'un tel dispositif nécessite l'intervention d'un opérateur. Finalement, les solutions hydroélectriques sont contraintes par la disposition géographique des sites qui sont pour la plupart éloignés des côtes. De plus, les puissances développées par les systèmes hydroélectriques sont largement supérieures aux besoins de notre système.

Après revue des différentes alternatives, la seule solution restante pour générer de l'énergie sur place est l'éolien. Cette solution est particulièrement bien adaptée à de faibles puissances comme en témoigne l'utilisation de plus en plus fréquente de ces technologies dans des contextes domestiques. De plus, la Norvège possède un très fort potentiel éolien, avec des vents suffisamment forts et réguliers. La carte ci-dessous montre que pour la majorité des sites envisageables, le vent est suffisant car supérieur en moyenne au minimum de 4km/h que nécessite la plupart des éoliennes.


![windmap](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/windmap.png "carte des vents du nord de la Norvège")

On constate que quelques zones ne réunissent pas les conditions recquises par l'éolien: on proposera donc une solution de secours pour ces quelques cas particuliers.


**Evaluation des besoins en énergie**

Afin de dimensionner correctement les équipements relatifs à l'énergie, il convient d'avoir une idée précise des besoins de notre système. Les deux carractéristiques principales à considérer sont la consommation moyenne, et la puissance maximale que l'on doit être capable de développer ponctuellement pour permettre, notamment, les communications satelitaires. La consommation moyenne dépend bien évidement de l'échelle du site considéré, car le principal besoin d'énergie provient de l'allimentation des capteurs. En effet le micro-controleur sélectionné nécessite entre 0,7µA (idle) et 270µA (on load) sous une tension de 2,2V, soit une consomation 0,594mW si l'on considère pour simplifier que ce dernier est solicité en permanence. Pour comparaison, un triplet de capteurs pH-niveau-température consomme 155mW (voir calcul ci-dessous) ce qui justifie que l'on puisse considérer la consommation du système embarqué comme négligeable.

*micro-controleur* - calcul ci-dessus, **0,594mW**.

*équipement satellitaire* - détaillé dans la partie en question, **5 W**

*capteur pH + temperature* - 3 piles AAA pour 1200h d'utilisation. 1250mAh/pile soit 3750mAh à 1,5V c'est à dire une consommation de **4,6875 mW**.

*capteur de niveau* - 50mA sous 3V, soit **150 mW**.


Si l'on considère:  
que toutes les cuves sont équipées des trois types de capteurs qui fonctionnement environ 1 minute par heure,  
que l'on néglige les pertes en ligne (qui sont proches de zero aux intensités considérées),  
que l'on ouvre 3 fenêtres de communication satellitaire de 2 minutes chaque jour,  
nous obtenons la consommation moyenne d'un site par l'approximation suivante:

Consomation journalière = (155.nbCuves + 2.3.5000).60 (mW.s)

Soit environ 630 Wh/jour pour les sites les plus grands (50 cuves) que l'on prendra comme référence.





**Solution standard: Éolien & Batterie tampon**


La solution standard s'appuie donc sur la génération d'énergie par l'intermédiaire d'une éolienne de capacité adaptée. Les aléas météorologiques ne permettant pas une alimentation continue, nous adjoindrons à cette source d'énergie une batterie de capacité limitée, supposée apte à subvenir seule aux besoins du système pendant 2 jours complets. Le second rôle de la batterie tampon est de permettre le développement de la puissance nécessaire aux fenêtres de communication satellitaires, puissance qui n'est pas forcément délivrée en sortie d'une petite éolienne. Le rendement de cette batterie sera mauvais du fait des conditions de température, mais ce n'est pas un problème si l'on considère qu'elle n'a pour seul rôle que de faire tampon entre l'éolienne et le système. L'accent sera mis sur le choix d'une batterie adaptée à ces conditions.

Par ailleurs, l'éolienne devra être légèrement surdimensionnée afin de permettre un rechargement rapide de la batterie quand les conditions météo sont favorables. De nombreuses solutions d'éoliennes domestiques conviennent parfaitement aux besoins de notre système, et présentent généralement des tarifs attractifs. C'est le cas de la [Ultimate Air One 600](http://toutlesolaire.com/p/Eolienne-24V-600W-Ultimate-Aire-One-/1500.html) sélectionnée, qui replit parfaitement les critères ci-dessus et présente l'avantage de fonctionner même lors de vents faibles (jusqu'à 2,5m/s). Il est important, lors de l'usage d'une source d'énergie inconstante telle qu'une éolienne, de favoriser les batteries qui ne sont pas sujetes à l'effet mémoire. Ainsi les batteries au plomb par exemple, sont a exclure. On choisit la batterie [GEL MOLL OPzV 1530Ah 2V](http://www.apb-energy.fr/boutique/fiche_produit.cfm?ref=MOLL-OPZV-1530&type=175&code_lg=lg_fr&num=181) qui pour un prix de 708€, devrait couvrir une autonomie de minimum 2 jours avec sa capacité de 3000Wh malgré la perte de performances en cas de faibles températures.

Prix unitaire de la solution:  
9000€	installation  
3590€	éolienne  
708€	batterie  

durée de vie éolienne: ~10 ans  
durée de vie batterie: 4-5 ans

durée d'installation: 1-2 jours



**Solution alternative: Optimisation différentielle d'une batterie de forte capacité**

Dans le cas où la localisation d'un site n'offre aucune prise au vent suffisante pour y placer une éolienne, on propose la solution exceptionnelle décrite ci-dessous. Il est important de noter que cette solution est plus onéreuse, offre de moins bons rendements et une autonomie moins forte que la solution standard présentée précédemment. Sa mise en place doit donc se limiter exclusivement aux cas où la solution standard ne serait pas applicable.


![alternative](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/energie-sol-alternative.png "schéma de la solution alternative")

Le principe général de la solution est de maintenir la batterie à une température permettant un rendement acceptable, tout en limitant la consommation du dispositif de chauffage au minimum. Dans cette optique, on place l'ensemble des composants électroniques centraux (système embarqué notamment) dans une enceinte limitant les échanges de chaleur avec l'extérieur, le but étant également de rentabiliser la dissipation thermique de ces derniers. L'appoint de chauffage est rendu possible par l'intégration d'une résistance alimentée par la batterie elle-même. L'activation de cette résistance est contrôlée par une brique logicielle fonctionnant sur le système embarqué, dont l'objectif est de déterminer la meilleure stratégie à adopter pour préserver l'énergie emmagasinée dans la batterie malgré les conditions de température. Pour que cette optimisation soit possible, il faut au préalable avoir caractérisé précisément le rendement de la batterie en fonction de la température, le rendement de la résistance, ainsi que les caractéristiques thermiques (inertie, fuites...) de l'enceinte. En se basant sur ces données initiales et sur les relevés de température à l'intérieur du boitier, la brique logicielle est capable, par la résolution d'un système différentiel complexe, de déterminer cette stratégie optimale de chauffage. L'implémentation de ce système dans son ensemble (choix des composants les plus adaptés, étalonnage, développement de la brique logicielle...) ne sera pas détaillé ici, mais nos équipes disposent de l'expertise nécessaire à la mise en place d'un tel dispositif.

Certaines contraintes apparaissent du fait de l'utilisation de cette solution alternative. Il faudra notamment surveiller à distance le niveau de la batterie afin d'anticiper les pannes d'énergie. Par ailleurs, l'autonomie n'étant que partielle, les intervenants des sociétés de maintenance devront être mis à partie pour remplacer les batteries vides par des batteries chargées lors des interventions. Cela implique une formation supplémentaire (succinte mais nécessaire) de ce personnel intervenant, et le développement des aspects logistiques et techniques nécessaires au rechargement des batteries échangées.


Le caisson isotherme sera conçu sur mesure afin d'obtenir des carractéristiques thermiques optimales malgré le passage des cables au travers de la parroi isolante. La société française SAINTE MARIE CONSTRUCTIONS ISOTHERMES dispose de l'expérience nécessaire à la sous-traitance de la fabrication (cf. auto-description de l'entreprise ci-dessous). Le prix exact par caisson est impossible à déterminer sans avoir recours à un devis, cependant au vu des prix du marché on peut envisager un tarif aux alentours de 700€/pièce.

*"Le savoir faire dans la conception de cellules isothermes, a permis à SMCI, le lancement d'une gamme de caissons isothermes capables de répondre aux attentes des métiers high tech, tel que les télécommunications, l'exploration pétrolière, l'industrie aéronautique et les services aéroportuaires. Des caissons conçus et fabriqués selon le cahier des charges de nos clients, répondant ainsi aux exigences les plus poussées, assurant fiabilité, résistance et protection des équipements les plus sensibles contre les variations de température ou une forte hygrométrie."*

Pour faire l'appoint de température, on sélectionne un composant de puissance limitée car l'inertie thermique de l'ensemble ainsi que les excellentes carractéristiques d'isolation du caisson laissent supposer qu'il ne sera nécessaire de chauffer que de manière très ponctuelle. La résistance chauffante [DBK - HP04-1/04-24](http://fr.farnell.com/dbk/hp04-1-04-24/resistance-chauffante-ptc-20w/dp/4408329) présente un bon compromis en termes de consommation électrique (10W), elle est disponible au prix de 12,26€ au dela de 50 unités achetées.

Au vu de la complexité d'un tel dispositif, il serrait malhonnête d'annoncer à ce stade du développement une consommation effective du système de régulation, et donc de pouvoir dimentionner précisément la batterie qui lui sera associée. Cependant sans entrer dans les détails, on considère qu'une autonomie de 3 mois minimum est nécessaire pour qu'un tel système soit rentable. Les batteries à considérer pour de telles exigences, et au vu de la consommation réduite du système d'autre part, sont généralement situées dans des gammes de prix au dela de 5000€. Bien évidement, la taille du site est également un critère important pour le choix de la capacité nominale de la batterie.

Frais fixes:
~4.000€		Développement de la carte  
~8.000€		Infrastructure de recharge des batteries  
~200€/per	journée de formation au remplacement des batteries  


Prix unitaire de la solution:  
700€	caisson  
12,26€	résistance  
10.000€	batterie  
800€	assemblage

durée de vie de la batterie ~10ans

durée d'installation: 1 jour


c. Système embarqué et système de communication avec le site central
--------------------------------------------------------------------

### Introduction ###

Le système embarqué se doit d'assurer trois fonctions principales&nbsp;:

- recueillir les données envoyées par les capteurs, les regrouper par cuves, les dater, en bref, les identifier&nbsp;;
- envoyer les données vers le site central lorsque la liaison est disponible&nbsp;;
- stocker les données lorsque la liaison avec le site central n'est pas disponible.

Le système assurera également, dans certains cas, une fonction auxiliaire&nbsp;: le contrôle de la température de l'enceinte thermique.

Ces fonctionnalités sont prises en charge par les trois composants du système embarqué&nbsp;: le microcontrôleur, le système de liaison et la mémoire externe.

_N.B.&nbsp;: Dans la suite, les coûts sont exprimés en euros, et n'incluent ni main d'œuvre, ni coûts liés à un développement spécifique (logiciel ou matériel), sauf mention contraire explicite. Les coûts donnés n'incluent donc que les prix des pièces détachés et des prestations fournies._

### Microcontrôleur ###

Il est important de noter que les données reçues par le microcontrôleur de la part des capteurs sont déjà toutes numériques. Sa tâche principale se résume donc à contextualiser des données (c'est-à-dire leur associer un identifiant), et rediriger l'information résultante vers l'un de ses deux périphériques, soit le système de liaison, soit la mémoire externe.

La régulation de la température est elle plus complexe. D'autre part, cette brique logicielle n'est nécessaire que lorsque le système embarqué est installé dans une enceinte thermique, c'est-à-dire dans le cas (considéré comme rare) où une source d'énergie éolienne n'est pas disponible (voir _Solution alternative_ dans _[b. Énergie](#b-energie)_).

Pour cette raison, et parce que cette fonction, qui n'est pas liée à la satisfaction d'une exigence fonctionnelle, risque d'interférer avec la tâche principale du microcontrôleur, cette brique logicielle s'exécute sur un microcontrôleur dédié. La carte correspondant au système embarqué est donc déclinée en deux versions, selon la solution d'alimentation retenue, avec un ou deux microcontrôleurs.

Il faudra donc assurer le développement d'une carte spécifique pour le système embarqué.

_Coût approximatif de la carte&nbsp;: &nbsp;€ pour le développement/prototypage/test de la carte + y&nbsp;€ (par carte, hors microcontrôleur et mémoire externe) pour la production._

#### Microcontrôleur de transmission des données ####
Comme dit précédemment, ce microcontrôleur assure une tâche simple. En s'appuyant sur la partie _[a. Capteurs](#a-capteurs)_, on peut déterminer que le débit de données que devra traiter ce microcontrôleur est de 2 octets par seconde. En effet, la fréquence de mesure choisie est de une mesure par cuve par heure. On fait l'hypothèse ici que cette mesure engendre une transmission de huit octets vers le système embarqué et que les mesures ont toutes lieues à des instants différents (pas de phénomène de pic). En considérant un site isolé de 50 cuves (légère surestimation par rapport aux plus grands sites) avec chacune 10 capteurs, cela représente donc un volume de 4000 octets à traiter par heure, soit 1,11 octets par seconde. Par sécurité, le traitement à appliquer à une mesure doit donc se faire dans tous les cas en moins d'une demi seconde. Compte tenu des performances actuelles des microcontrôleurs sur le marché, cette obligation n'est pas un facteur limitant, puisque virtuellement n'importe quel microcontrôleur convient pour remplir une tâche aussi peu demandeuse de performance.

Le choix du microcontrôleur ne peut donc reposer sur un critère de performance. Il doit donc reposer sur les critères suivants, identifiés comme les plus importants lors de l'analyse des besoins et du recueil des exigences&nbsp;: l'efficacité en terme de consommation de la solution proposée, afin de maximiser l'autonomie du système. Il s'agit là d'un objectif d'autant plus important qu'une solution très économe en énergie a déjà été trouvée pour les capteurs, et que dans le cas de l'alimentation alternative sur batterie uniquement, l'autonomie est un besoin encore plus crucial.

Pour cette raison, nous avons choisi d'utiliser un MSP430 pour le traitement et la transmission des données. Cette gamme de microcontrôleur de Texas Instruments est focalisée sur des produits très économes en énergie. Compte tenu du (très) faible besoin de performance et de la simplicité algorithmique du travail à effectuer, un microcontrôleur d'entrée de gamme (appartenant à la famille _MSP430 1 Series_, par exemple) devrait être utilisable. Toutefois, afin d'anticiper de futures évolutions de la solution, et pour ne pas être limité par un matériel qui s'avèrerait alors trop peu performant, un microcontrôleur plus puissant (appartenant à la famille _MSP430 2 Series_) a été choisi.

Le microcontrôleur choisi permettant également de réaliser des conversions analogiques/numériques, celui peut aussi être employé au niveau des cuves, pour envoyer les mesures au système embarqué par ondes radio (voir _[a. Capteurs](#a-capteurs)_). De même, ce microcontrôleur est assez puissant pour assurer le contrôle de la température (voir _Microcontrôleur de régulation de la température_, ci-après. Au final, nous n'utilisons qu'un seul type de microcontrôleur pour répondre à tous nos besoins, ce qui présente plusieurs avantages. On peut notamment citer une même plateforme de développement, donc une réduction des coûts de programmation, ainsi que la possibilité de commander le nombre minimum d'exemplaires (bien souvent 1&thinsp;000) pour bénéficier du tarif le plus bas.

_Bref, dans le paragraphe qui précède, les valeurs peuvent changer&nbsp;: passer de_ MSP430 2 Series _à_ MSP430 Low Voltage Series _mais les idées restes les mêmes._

Le microcontrôleur choisi (MSP430F2370) à les caractéristiques suivantes&nbsp;:

- Fréquence&nbsp;: 16&nbsp;MHz
- Taille de la mémoire Flash&nbsp;: 32&nbsp;ko
- Taille de la RAM&nbsp;: 2048 octets
- Nombre de broches GPIO&nbsp;: 32
- Convertisseur analogique/numérique&nbsp;: Oui
- Multiplicateur matériel&nbsp;: Oui
- Support matériel de protocoles de communication série&nbsp;: Oui 
- Prix (à l'unité)&nbsp;: 1,95&nbsp;$ (pour 1&thinsp;000 exemplaires)

_Autre chose très intéressante avec ce microcontrôleur, c'est que la [page](http://www.ti.com/product/msp430f2370) de Texas Instruments le décrivant porte une référence sur cette page, intitulée [Energy Harvesting](http://www.ti.com/solution/energy_harvesting). À lire absolument. Coralie et Yann (pour la partie alimentation) dites moi ce que vous en pensez&nbsp;!_

#### Microcontrôleur de régulation de la température ####

Pour les raisons citées précédemment, le choix de ce microcontrôleur a déjà été fait. En effet, le microcontrôleur utilisé pour la partie transmission des données dispose de toutes les caractéristiques matérielles nécessaires (présence d'un multiplicateur matériel, cadence "élevée" de 16 MHz, RAM de taille suffisante) pour effectuer tous les calculs liés à la régulation de la température.

Le microcontrôleur qui est utilisé pour assurer la régulation de la température, dans le cas d'un système embarqué en enceinte thermique, est du même modèle que le microcontrôleur utilisé pour la transmission des données.

### Système de liaison ###

Au niveau du microcontrôleur de chaque site distant, on aggrège les données des capteurs envoyées chaque heure, en les envoyant au moins une fois par jour.

Un capteur transmet toutes les 60 minutes son ID et sa valeur (deux entiers sur 4 octets), ce qui fait 2*4*24 = 192 octets de données par jour et par capteur, compressible à 100 octets en évitant la répétition de l’ID.

De manière réaliste, sur un gros site (30 cuves) où chaque cuve aurait 3 capteurs, (pH, niveau et température), on aurait donc 9000 octets de générés chaque jour, auxquels il faut rajouter les différentes en-têtes nécessaires à la transmission :
  - Ethernet : 18 octets
  - IP : 24 octets
  - TCP : 24 octets

Soit +66 octets.

Pour un gros site, on s’attend donc à consommer 9066 octets/jour, soit 265,6 ko/mois.

Pour un petit site (5 cuves) : ((5*3*100)+66)*30 octets/mois = 45,9 ko/mois.

En supposant que les sites peuvent être amenés à grossir de manière raisonnable en nombre de cuves, on peut fixer un plafond de trafic allant de 1 mo à 2 mo par mois pour un gros site, si un ou deux capteurs venaient à s’ajouter. Quand au débit maximal, il apparaît être vraiment peu significatif, les offres les plus lentes d’Internet par satellite conviendraient. Avec la gamme que nous avons choisies (quelques centaines de kilobits/s), la communication des données quotidiennes se ferait en moins d’une seconde.

_Système de transmission composé de&nbsp;:_

- _Antenne Prodelin de 1,8&nbsp;m de diamètre_
- _Unité de transmission/réception de 5 W (C-Band)_
- _Équipement divers nécessaire à l'installation de l'antenne sur le site_

_Le tout pour environ 300&nbsp;€ (hors frais d'abonnement)._

### Mémoire externe ###

_Spansion S25FL512S_

- _Taille de la mémoire&nbsp;: 64&nbsp;Mo_
- _Alimentation électrique&nbsp;: 3&nbsp;V, 100&nbsp;mA en fonctionnement, 0,07&nbsp;mA à l'arrêt_
- _Prix (à l'unité)&nbsp;: 6,78&nbsp;€ (pour 1&thinsp;000), 7,34&nbsp;€ (pour 100)_

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

