Ebauche de solution
==

Architecture
--

La solution est constituée de plusieurs installations réparties sur plusieurs sites:
- des sites distants: isolés (du point de vue des communications), difficiles d'accès, où sont relevées les mesures des capteurs
- un site central: fortement connecté (du point de vue des communications), facile d'accès, communiquant avec les sites isolés et les camions

Sites distants
--

Un système embarqué récupère les mesures du réseau de capteurs déployé sur le site distant et les transmet au site central.
Les capteurs communiquent avec le système embarqué, suivant différentes modalités, selon le nombre de capteurs et leur dispersion sur le site.

Les différentes modalités envisageables sont :
- un réseau filaire à base de RS232, (RJ45 + Ethernet), ou autre ?
- un réseau sans fil à base d’émetteurs/récepteurs radio courte/moyenne portée, de réseau Bluetooth, Wifi, Zigbee, ou autre ?
- un réseau hybride composé des deux réseaux précédents ?

### Peu de capteurs, sur une faible superficie
Pour un nombre limité de capteurs (moins d’une dizaine) sur une superficie faible (moins de 10 ha), un réseau filaire pourrait être le meilleur choix. (Même si le coût d’installation de l’infrastructure filaire sera sûrement plus élevé que celui d’une installation sans fil, la sécurité et la consommation énergétique de ces réseaux devraient être bien meilleures.)

blablabla...

Site central
--
Centre nerveux du système, compte des serveurs recevant les informations envoyées par les sites distants et un centre de décision déclenchant des alertes lorsque l’état des sites distants est nécessite une intervention.

De là, plusieurs solutions sont possibles :
- Établir un système de maintenance à distance pour effectuer des maintenances simples (ex ajuster la température d’une cuve, diffuser un produit pour ajuster le pH, etc).
- Former les responsables de site distant aux maintenances simples et les informer lorsque celles ci sont nécessaires
- Tout faire faire par la société de maintenance

Dans tous les cas, à la réception d’une alerte, des opérateurs d’astreinte au site central décident ou non d’une action à mener, et en informent le ou les acteurs concernés.

Le système d’informations du site central a donc pour fonctionnalités principales:
- Journalisation des événements et statistiques en provenance des sites distants
- Alerte en fonction des évènements en provenance des sites distants, avec différents niveaux de gravité (avertissement, maintenance urgente nécessaire, etc)
- (Maintenance à distance)
- Émission de demandes de maintenance
- Journalisation des actions commandées (alerte du responsable de site, maintenance à distance ou demande de maintenance à la société de maintenance)

Questions
-----
- Comment se fait la demande d’intervention auprès de la société de maintenance  (téléphone, email, autre...) ?
- Quelles sont les informations actuellement transmises à la société de maintenance ?
- La société de maintenance est-elle toujours la même pour toute l’UE ? (Il peut être nécessaire d’avoir des protocoles de demande d’intervention spécifiques pour chaque société de maintenance, à cause de la langue par exemple.)
- Quels sont les différents types de sites distants (en dehors de ceux cités dans le document d’appel d’offres) ?
- Quel est le type de contrat avec la société de maintenance (forfait ou facturé à l’intervention) ? &rarr; Intérêt de faire de la maintenance à distance ? Si forfait, non, si facturé à l’intervention, peut-être.
    * Avantages : Réduction des coûts de maintenance puisqu’on évite de faire une demande auprès de la société de maintenance pour les tâches simples ; Indépendance relative vis à vis des sociétés de maintenance
    * Inconvénients : Coût initial important : il faut installer tout un dispositif de maintenance automatique sur le site isolé. Il faut maintenir (à jour et en état de fonctionnement) le système de maintenance à distance
- Est-ce qu’il y a des contraintes (légales...) obligeant à maintenir un opérateur sur le site? (Si oui, on peut les former pour effectuer les maintenances simples, sinon on peut envisager de vider le site et de faire de la maintenance automatique)
