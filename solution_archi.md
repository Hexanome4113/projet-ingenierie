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
  Présentation des problématiques et des contraintes. Problématique : réussir à faire en sorte que les sites soient autonomes.
  Contraintes : sites de 100m à 1km, jusqu'à une cinquantaine de cuves, froids, accidentés...
  
  </dd>
  <dd>
  Priorisation des exigences non-fonctionnelles : Autonomie d'abord (expliquer un peu les conséquences), puis...
  </dd>
  
  <dt>Solution retenue</dt>
  <dd>
  Explication de la solution (schéma) : Capteurs des cuves reliés par cable au site,
  </dd>
  <dd>
  Avantages (pas de maintenance, fiabilité (robustesse)), raisons du choix
  </dd>
  <dd>
  limites (installation : coûts et difficultées en fonction du terrain)
  </dd>
  <dd>
  coûts
  </dd>

  <dt>Solution alternative</dt>
  <dd>
  explication de la solution (schéma) : Une borne radio par cuve, reliée aux différents capteurs, et un récepteur sur le site
  </dd>
  <dd>
  endroits pertinents ( , si plusieurs cuves sont proches...)
  </dd>
  <dd>
  avantages (coûts limités d'installation, pas de problèmes d'installation)
  </dd>
  <dd>
  inconvénients (isolation, lieux fortement accidentés, société de maintenance ne coopérant pas),
  </dd>
  <dd>
  coûts
  </dd>
  
</dl>


b. Energie
----------

 **Introduction**

Le système nécessite la mise en place d'une solution d'alimentation autonome pour les sites isolés n'ayant pas accès à une source d'énergie exterieure. Le système ayant besoin d'une alimentation continue et de faible puissance, il semble indispensable d'avoir recours à une batterie pour faire tampon, quelle que soit la source d'énergie utilisée. La principale contrainte de fonctionnement d'une batterie est la temperature ambiante, en l'occurence ici les températures sur site peuvent descendre jusqu'à des extrèmes de -40°C, ce qui limite drastiquement le rendement de n'importe quelle batterie du marché.


Le problème de la source d'énergie en elle-meme est contraint par les conditions géographiques et météorologiques du site. Une allimentation photovoltaïque est inenvisageable du fait de la très forte variabilité des durées d'ensoleillement des régions concernées. L'exploitation de la biomasse environnante est également innapropriée, car les régions concernées sont potentiellement désertiques et la mise en fonctionnement d'un tel dispositif nécessite l'intervention d'un opérateur. Finnalement, les solutions hydroélectriques sont contraintes par la disposition géographique des sites qui sont pour la pluspart éloignés des cotes. De plus les puissances développées par les systèmes hydroélectriques sont largement suppérieures aux besoins de notres sytème.

Après revue des différentes alternatives, la seule solution restante pour générer de l'énergie sur place est l'éolien. Cette solution est particulièrement bien adaptée à de faibles puissances comme en témoigne l'utilisation de plus en plus fréquente de ces technologies dans des contextes domestiques. De plus, la norvège possède un très fort potentiel éolien, avec des vents suffisament forts et réguliers. La carte ci-dessous montre que pour la majorité des sites envisageables, le vent est suffisant car superieur en moyenne au minimum de 4km/h que nécessitent la plus part des éoliennes.


![windmap](http://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/windmap.png "carte des vents du nord de la Norvège")

On constate que quelques zones ne réunissent pas les conditions recquises par l'éolien: on proposera donc une solution de secours pour ces quelques cas particuliers.

**Solution standard: Eolien & Batterie tampon**

**Solution alternative: Optimisation différentielle d'une batterie de forte capacité**

Dans le cas où la localisation d'un site n'offre aucune prise au vent suffisante pour y placer une éolienne, on propose la solution exceptionnelle décrite ci-dessous. Il est important de noter que cette solution est plus onéreuse, offre de moins bons rendements et une autonomie moins forte que la solution standard présentée précédement. Sa mise en place doit donc se limiter exclusivement aux cas où la solution standard ne serait pas applicable.


![windmap](http://raw.github.com/Hexanome4113/projet-ingenierie/master/images/misc/windmap.png "schéma de la solution alternative")

Le principe général de la solution est de maintenir la batterie à une température permettant un rendement acceptable, tout en limitant la consommation du dispositif de chauffage au minimum. Dans cette optique, on place l'ensemble des composants electroniques centraux (système embarqué nottament) dans une enceinte limitant les échanges de chaleur avec l'exterieur, le but étant également de rentabiliser la dissipation thermique des ces derniers. L'appoint de chauffage est rendu possible par l'intégration d'une résistance allimentée par la batterie elle-meme. L'activation de cette résistance est controlée par une brique logicielle fonctionant sur le système embarqué, dont l'objectif est de déterminer la meilleure stratégie à adopter pour préserver l'énergie emagasinée dans la batterie malgré les conditions de température. Pour que cette optimisation soit possible, il faut au préalable avoir carractérisé précisément le rendement de la batterie en fonction de la température, le rendement de la résistance, ainsi que les carractéristiques thermiques (inertie, fuites...) de l'enceinte. En se basant sur ces données initiales et sur les relevés de température à l'interrieur du boitier, la brique logicielle est capable, par la résolution d'un système différentiel complexe, de déterminer cette stratégie optimale de chauffage. Le développement de ce système dans son ensemble (choix des composants les plus adaptés, étalonnage, développement de la brique logicielle...) ne sera pas détaillé ici, mais nos équipes disposent de l'expertise nécessaire au développement d'un tel dispositif.


c. Système central
------------------

d. ...
------


3. Communication inter-sites
============================
