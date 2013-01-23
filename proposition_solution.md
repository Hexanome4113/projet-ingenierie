Proposition de solution
==

Architecture
--

La solution est constituée de plusieurs installations réparties sur plusieurs sites:
- des sites distants: isolés (du point de vue des communications), difficiles d'accès, où sont relevées les mesures des capteurs
- un site central: fortement connecté (du point de vue des communications), facile d'accès, communiquant avec les sites isolés et les camions

Sites isolés
--

Un système embarqué récupère les mesures du réseau de capteurs déployé sur le site distant et les transmet au site central.
Les capteurs communiquent avec le système embarqué, suivant différentes modalités, selon le nombre de capteurs et leur dispersion sur le site.

Les différentes modalités envisageables sont :
- un réseau filaire à base de RS232, (RJ45 + Ethernet), ou autre ?
- un réseau sans fil à base d’émetteurs/récepteurs radio courte/moyenne portée, de réseau Bluetooth, Wifi, Zigbee, ou autre ?
- un réseau hybride composé des deux réseaux précédents ?

### Peu de capteurs, sur une faible superficie
Pour un nombre limité de capteurs (moins d’une dizaine) sur une superficie faible (moins de 10 ha), un réseau filaire pourrait être le meilleur choix. (Même si le coût d’installation de l’infrastructure filaire sera sûrement plus élevé que celui d’une installation sans fil, la sécurité et la consommation énergétique de ces réseaux devraient être bien meilleures.)

### Même genre de blabla à redétailler dans d'autres cas

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

Société de maintenance
--

Chaque site isolé fait appel à une société de maintenance (la plus proche pouvant répondre à ses besoins) pour demander des interventions.
Ces demandes d'intervention vont être maintenant générées par un service du serveur central et transmises par celui-ci à la société de maintenance concernée.
Ces demandes d'intervention seront transmises par l'envoi d'un document par mail (ou par fax) pour donner les détails de l'intervention et par un appel téléphonique afin de vérifier la disponibilité de la société de maintenance et de connaître leur réponse quant à l'intervention.
Après lecture du document de demande d'intervention la société de maintenance enverra par mail (ou par fax) un document de réponse au serveur central.
Une fois que l'intervention est effectuée, le technicien ayant effectué la maintenance enverra un document de compte-rendu au serveur central.

Tous les documents sus-cités devront suivre un certain formalisme. Un listing détaillé des informations nécessaires que doivent contenir ces documents est présenté ci-dessous.

Document de demande d'intervention (envoyé par le serveur central vers la société de maintenance) :
 - Date et heure de la demande
 - Site isolé concerné (nom et adresse)
 - Coordonnées du propriétaire du site isolé
 - Coordonnées du serveur central
 - Liste des évènements à traiter avec leur degré de gravité
 - Description de l'alerte et son degré de gravité (l'association de plusieurs évènements ayant une gravité mineure peut engendrer une alerte de niveau élevée)


Exigences fonctionnelles
---

1. Communication entre les capteurs et le site central *PH Ya*
2. Détermination du niveau de gravité d'un évènement *Th*
3. Emission d'une alerte selon l'évènement *Th* 
4. Emission d'une demande de maintenance *Es*
5. Optimisation des coûts de maintenance (inclut maintenance automatique) *Ni*
6. Journalisation des évènements et des commandes *Fr*
7. Sauvegarde des évènements sur le site isolé en cas de connexion défaillante avec le serveur central *Co*
