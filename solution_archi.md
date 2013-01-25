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
   au serveur du site. Pour celà, il y a deux problématiques principales auxquelles il faut répondre : gérer la transmission des données, et s'assurer
   de l'apport en énergie aux différents appareils.
   
  Diverses contraintes rendent ces opérations difficiles : la taille des sites (faisant de 100m à 1km, ce qui fait une distance importante entre le serveur
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
  Cette solution consiste à installer un serveur sur le site et à le relier directement à chacune des cuves par des cables électriques
  </dd>
  <dd>
  Les principaux avantages de cette solution résident dans son utilisation peu coûteuse ; Ses capteurs étant directement reliés au réseau, 
   il n'y a pas besoin de source d'énergie autre que celle du serveur. De plus, son nombre limité d'appareil limite les risques de pannes 
   et donc de coupure du réseau et de frais de maintenance.
  </dd>
  <dd>
  Cette approche présente cependant un certain nombre de limites, notamment celle liées à la complexité d'installation. En effet, le serveur pouvant
   être assez éloigné des cuves, il faudra parfois tirer un cable de 1km, pouvant poser des difficultés d'installation (et des frais importants) en fonction
   des terrains.
  </dd>
  <dd>
  Par cuve : ~ 150€ + 100€/100m
  phMètre : gamme moyenne 55€
  termomètre : gamme moyenne 40€
  niveau : gamme moyenne 30€bha
  cables : 10€ + 80€ / 100m
  main-d'oeuvre : 2h/homme + 2h/homme/100m -> 25€ + 25€/100m
  </dd>

  <dt>Solution alternative</dt>
  <dd>
  Pour palier au relatif manque d'efficacité de la solution retenue dans certains cas, nous pouvons proposer une solution alternation dont l'architecture serait la suivante :
  </dd>
</dl>

  ![Proposition alternative](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/Solution_alternative.png)
  
<dl>
  <dd>
  Cette solution consistant à installer une borne radio (reliée aux différents capteurs) par cuve permettant de communiquer avec le serveur et un récepteur du côté du serveur a l'avantage d'avoir des coûts fixes : on ne payera pas plus cher 
   pour une cuve éloignée de 1km que pour une éloignée de 20m.
  </dd>
  <dd>
  L'avantage principal de cette solution est sa facilité d'installation et un coût relativement limité lors de la pose sur des cuves éloignées du serveur. Cependant, elle présente de nombreux points limitant son utilisation : pour commencer,
   elle n'est rentable qu'à partir d'une certaine distance, une communication par onde n'étant bien évidement pas nécessaire pour des cuves situées à 10m du serveur. Ensuite, cette solution pose un problème d'autonomie des appareils : en effet,
    les capteurs n'étant plus reliés électriquement au site, il doivent trouver une source d'énergie autre. Pour celà, l'utilisation d'une batterie peut s'avérer concluante, mais nécessite tout de même un changement occasionnel. Cependant, des accords
	avec les sociétés de maintenance pourraient être trouvés : le système leur permettant d'économiser des trajets, celles-ci pourraient faire un geste et s'occuper du changement des batteries annuel sans modification du contrat. Le dernier problème de cette
	solution peut venir de l'endroit du site : le terrain peut être accidenté et empêcher les ondes de passer. Par ailleurs, le froid risque de geler les appareils de transmission, des mesures (assez coûteuses) devant être prises pour éviter cela.
  </dd>
  <dd>
  Par cuve : ~ 550€ + 30€ an
  emetteur : longue portée 60€
  msp430 (ou équivalent) 10€
  phMètre : gamme moyenne 55€
  termomètre : gamme moyenne 40€
  niveau : gamme moyenne 30€
  cables : 10€
  batterie : 30€/ an
  isolation : 200€ (polyurethane) 
  chauffage : 50€
  main-d'oeuvre : 4h/homme -> 50€
  
  Site : ~ 50€
  Récepteur radio : 30€
  fil : 3€
  main d'oeuvre : 1h/homme : 15€
  </dd>

<dt>Conclusion</dt>
  <dd>Bien que la première solution semble plus intéressante, il peut être pertinent de la combiner dans certains cas à la seconde pour une plus grande souplesse et une économie conséquente.
</dl>

b. Energie
----------

 **Introduction**

Le système nécessite la mise en place d'une solution d'alimentation autonome pour les sites isolés n'ayant pas accès à une source d'énergie exterieure. Le système ayant besoin d'une alimentation continue et de faible puissance, il semble indispensable d'avoir recours à une batterie pour faire tampon, quelle que soit la source d'énergie utilisée. La principale contrainte de fonctionnement d'une batterie est la temperature ambiante, en l'occurence ici les températures sur site peuvent descendre jusqu'à des extrèmes de -40°C, ce qui limite drastiquement le rendement de n'importe quelle batterie du marché.


Le problème de la source d'énergie en elle-meme est contraint par les conditions géographiques et météorologiques du site. Une allimentation photovoltaïque est inenvisageable du fait de la très forte variabilité des durées d'ensoleillement des régions concernées. L'exploitation de la biomasse environnante est également innapropriée, car les régions concernées sont potentiellement désertiques et la mise en fonctionnement d'un tel dispositif nécessite l'intervention d'un opérateur. Finnalement, les solutions hydroélectriques sont contraintes par la disposition géographique des sites qui sont pour la pluspart éloignés des cotes. De plus les puissances développées par les systèmes hydroélectriques sont largement suppérieures aux besoins de notres sytème.

Après revue des différentes alternatives, la seule solution restante pour générer de l'énergie sur place est l'éolien. Cette solution est particulièrement bien adaptée à de faibles puissances comme en témoigne l'utilisation de plus en plus fréquente de ces technologies dans des contextes domestiques. De plus, la norvège possède un très fort potentiel éolien, avec des vents suffisament forts et réguliers. La carte ci-dessous montre que pour la majorité des sites envisageables, le vent est suffisant car superieur en moyenne au minimum de 4km/h que nécessitent la plus part des éoliennes.


![windmap](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/windmap.png "carte des vents du nord de la Norvège")

On constate que quelques zones ne réunissent pas les conditions recquises par l'éolien: on proposera donc une solution de secours pour ces quelques cas particuliers.

**Solution standard: Eolien & Batterie tampon**

La solution standard s'appuie donc sur la génération d'énergie par l'intermédiaire d'une éolienne de capacité adaptée. Les aléas météorologiques ne permettant pas une alimentation continue, nous adjoindrons à cette source d'énergie une batterie de capacité limitée, supposée apte à subvenir seule aux besoins du système pendant 2 jours complets. Le rendement de cette batterie sera mauvais du fait des conditions de température, mais ce n'est pas un problème si l'on considère qu'elle n'a pour seul rôle que de faire tampon entre l'éolienne et le système. L'accent sera mis sur le choix d'une batterie adaptée à ces conditions.

Par ailleurs, l'éolienne devra être légerement surdimentionnée afin de permettre un rechargement rapide de la batterie quand les conditions météo sont favorables.


**Solution alternative: Optimisation différentielle d'une batterie de forte capacité**

Dans le cas où la localisation d'un site n'offre aucune prise au vent suffisante pour y placer une éolienne, on propose la solution exceptionnelle décrite ci-dessous. Il est important de noter que cette solution est plus onéreuse, offre de moins bons rendements et une autonomie moins forte que la solution standard présentée précédement. Sa mise en place doit donc se limiter exclusivement aux cas où la solution standard ne serait pas applicable.


![windmap](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/energie-sol-alternative.png "schéma de la solution alternative")

Le principe général de la solution est de maintenir la batterie à une température permettant un rendement acceptable, tout en limitant la consommation du dispositif de chauffage au minimum. Dans cette optique, on place l'ensemble des composants electroniques centraux (système embarqué nottament) dans une enceinte limitant les échanges de chaleur avec l'exterieur, le but étant également de rentabiliser la dissipation thermique des ces derniers. L'appoint de chauffage est rendu possible par l'intégration d'une résistance allimentée par la batterie elle-meme. L'activation de cette résistance est controlée par une brique logicielle fonctionant sur le système embarqué, dont l'objectif est de déterminer la meilleure stratégie à adopter pour préserver l'énergie emagasinée dans la batterie malgré les conditions de température. Pour que cette optimisation soit possible, il faut au préalable avoir carractérisé précisément le rendement de la batterie en fonction de la température, le rendement de la résistance, ainsi que les carractéristiques thermiques (inertie, fuites...) de l'enceinte. En se basant sur ces données initiales et sur les relevés de température à l'interrieur du boitier, la brique logicielle est capable, par la résolution d'un système différentiel complexe, de déterminer cette stratégie optimale de chauffage. Le développement de ce système dans son ensemble (choix des composants les plus adaptés, étalonnage, développement de la brique logicielle...) ne sera pas détaillé ici, mais nos équipes disposent de l'expertise nécessaire au développement d'un tel dispositif.

Certaines contraintes sont apparaissent du fait de l'utilisation de cette soltion alternative. Il faudra notamment surveiller à distance le niveau de la batterie afin d'anticiper les pannes d'énergie. Par ailleurs, l'autonomie n'étant que partielle, les intervennants des sociétés de maintenance devront être mis à partie pour remplacer les batteries vides par des batteries pleinnement chargées lors des interventions. Celà implique une formation supplémentaire (succinte mais nécessaire) de ce personnel intervenant, et le developpement des aspects logistiques et techniques nécessaires au rechargement des batteries échangées.


c. Système central
------------------

d. ...
------


3. Communication inter-sites
============================
