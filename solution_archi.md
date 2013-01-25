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
<dl>
	<dt> Introduction </dt>
	<dd>
	Le système nécessite la mise en place d'une solution d'alimentation autonome pour les sites isolés n'ayant pas accès à une source d'énergie exterieure. Le système ayant besoin d'une alimentation continue et de faible puissance, il semble indispensable d'avoir recours à une batterie pour faire tampon, quelle que soit la source d'énergie utilisée. La principale contrainte de fonctionnement d'une batterie est la temperature ambiante, en l'occurence ici les températures sur site peuvent descendre jusqu'à des extrèmes de -40°C, ce qui limite drastiquement le rendement de n'importe quelle batterie du marché.
	</dd>
	<dd>
	Le problème de la source d'énergie en elle-meme est contraint par les conditions géographiques et météorologiques du site. Une allimentation photovoltaïque est inenvisageable du fait de la très forte variabilité des durées d'ensoleillement des régions concernées. L'exploitation de la biomasse environnante est également innapropriée, car les régions concernées sont potentiellement désertiques et la mise en fonctionnement d'un tel dispositif nécessite l'intervention d'un opérateur. Finnalement, les solutions hydroélectriques sont contraintes par la disposition géographique des sites qui sont pour la pluspart éloignés des cotes. De plus les puissances développées par les systèmes hydroélectriques sont largement suppérieures aux besoins de notres sytème.
	</dd>
	<dd>
	Après revue des différentes alternatives, la seule solution restante pour générer de l'énergie sur place est l'éolien. Cette solution est particulièrement bien adaptée à de faibles puissances comme en témoigne l'utilisation de plus en plus fréquente de ces technologies dans des contextes domestiques. De plus, la norvège possède un très fort potentiel éolien, avec des vents suffisament forts et réguliers. La carte ci-dessous montre que pour la majorité des sites envisageables, le vent est suffisant car superieur en moyenne au minimum de 4km/h que nécessitent la plus part des éoliennes.
	</dd>
</dl>

c. Système central
------------------

d. ...
------


3. Communication inter-sites
============================
