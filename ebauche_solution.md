Ebauche de solution
==

Architecture
--

L'installation est partagée sur plusieurs sites:
- des sites distants: isolés, difficiles d'accès, où sont relevées les mesures des capteurs
- un site central: fortement connecté, facile d'accès, d'où seront envoyées les commandes et qui recevra les informations des sites isolés


Sites distants
--

Récupèrent les mesures des capteurs environnants. Les capteurs communiquent avec un système, par différents moyens suivant la configuration du site:
pour un nombre limités de capteurs sur une superficie faible: en filaire, etc.

blablabla...


Site central
--



Prise de décision : Le système central devra être capable de décider (soit automatiquement, soit par décision d’un opérateur) les cas nécessitant l’intervention d’un agent de maintenance sur le site distant touché par un problème. Pour cela, nous pourrions définir un niveau de criticité pour chaque critère, le définissant comme nécessitant une intervention ou pouvant attendre.
Base de données : Les différentes données récupérées par les capteurs devront être stockées. Nous avons fait le choix de centraliser ces données sur le serveur du site central, à la fois pour limiter le nombre de bases de données et pour pouvoir permettre l’accès à l’historique des données enregistrées en cas de rupture de communication.

Besoins rattachés aux sites distants


Installation et identification des capteurs : Les différents capteurs présents sur chacun des sites devront être relié au serveur correspondant, et être correctement identfiés (le serveur doit savoir quel capteur correspond à quelle mesure)
Système de communication (fiable) entrée / sortie : En plus de communiquer avec chaque capteur, le serveur devra également communiquer avec le site central, certainement par satellite, les autres solutions n’étant pas assez longue portée ou trop coûteuses. Le serveur devra être capable d’envoyer les données des capteurs, mais aussi de recevoir des ordres (par exemple le changement d’un seuil de criticité)
Enregistrement des données lors de coupures : Les données étant enregistrées sur le site central, nous risquerions de perdre des données en cas de rupture de communication. Nous avons donc décider d’attribuer une petite mémoire à chaque site distant afin de pouvoir stocker les données enregistrées et les envoyer lors de la reprise des échanges.
