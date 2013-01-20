Epression des Besoins
===

1. Communication entre les capteurs et le site central
--

2. Détermination du niveau de gravité de l'évènement
--

3. Emission d'une alerte
--

4. Emission d'une demande d'intervention d'une société de maintenance
--
Après identification de(s) évènement(s) à traiter une demande d'intervention est transmise à la société de maintenance.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/01DemandeDIntervention.png "01 - Demande d'intervention")
Pour assurer le bon fonctionnement de cette transmission il faut que cette demande d'intervention soit envoyée par un moyen de communication fonctionnel et efficace et que l'(es) évènement(s) à traiter soit(ent) connu(s) et gérable(s) par la société de maintenance.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/02MoyenDeCommunicationETEvenements.png "02 - Moyen de communication et évènements")
Afin de garantir que le moyen de communication utilisé soit fonctionnel et efficace, il faut qu'il permette de mettre en place un formalisme de communication commun entre le serveur central et la société de maintenance, formalisme que chaque demande d'intervention devra ensuite suivre. Mais il faut aussi s'assurer que la société de maintenance soit disponible et puisse se déplacer au moment de la demande d'intervention (nuit, vacances, problèmes internes, ..., peuvent toujours survenir, il faut donc gérer ces cas).
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/03MoyenDeCommunication.png "03 - Moyen de communication")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/04DisponibilitDesActeurs.png "04 - Disponibilité des Acteurs")
En ce qui concerne la gestion de l'indisponibilité de la société de maintenance désignée par défaut pour le site isolé en question un solution peut être envisageable. Il serait avantageux pour les sociétés de maintenance (relativement) proche du site isolé et capables d'intervenir sur celui-ci de collaborer. Elle pourraient former une association de société de maintenance qui permettrait de gérer les problèmes d'indisponibilité d'une seule société de maintenance en affectant la demande d'intervention à une autre société alors disponible.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/4%20-%20Emission%20demande%20societe%20maintenance/05SociTSDeMaintenance.png "05 - Association de sociétés de maintenance")

5. Optimisation des coûts de la maintenance et de la maintenance automatique
--

6. Journalisation des données
--

7. Sauvegarde des évènements sur le site isolé en cas de connexion défaillante
--