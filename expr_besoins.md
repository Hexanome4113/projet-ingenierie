Epression des Besoins
===

1. Communication entre les capteurs et le site central
--
La communication des données des capteurs/actionneurs au site central est nécessaire à la satisfaction de nombreux besoins fonctionnels du système. Ainsi, les différentes étapes de cette communication doivent répondre à des exigences de qualité et de fiabilité. Cette communication est divisée en deux parties successives: le relevé des mesures par un système sur le site distant, que l'on nommera "système embarqué", et le rapatriement de ces informations jusqu'au site central. Par ailleurs, la communication de commandes remontant du site central jusqu'aux actionneurs devra être envisagée au moyen du même dispositif.


2. Détermination du niveau de gravité de l'évènement
--

3. Emission d'une alerte
--
Afin de permettre d'informer la société de maintenance des problèmes nécessitant correction, il est important d'avoir une trace de leur apparition. Pour cela, une alerte sera générée à chaque problème rencontré, et remontée au serveur central.
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9rer%20la%20g%C3%A9n%C3%A9ration%20des%20alertes%20%28Diagramme%20p%C3%A8re%29.png "DP - Gérer de la génération des problèmes")

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20D%C3%A9terminer%20la%20gravit%C3%A9%20des%20probl%C3%A8mes.png "DP - Déterminer la gravité des problèmes")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20D%C3%A9termination%20de%20la%20gravit%C3%A9%20des%20probl%C3%A8mes.png "DA - Déterminer la gravité des problèmes")

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9n%C3%A9rer%20une%20alerte%20automatiquement%20.png "DP - Générer une alerte automatiquement")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20automatique.png "DA - Générer une alerte automatiquement")

![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/3%20-%20Emission%20alerte/DP%20Gestion%20Des%20Alertes%20-%20G%C3%A9n%C3%A9rer%20une%20alerte%20manuellement.png "DP - Générer une alerte manuellement")
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ActivityDiagrams/3%20-%20Emission%20alerte/DA%20Gestion%20Des%20Alertes%20-%20Cr%C3%A9ation%20d%27une%20alerte%20manuelle.png "DA - Générer une alerte manuellement")


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

7. Sauvegarde des événements sur le site isolé en cas de connexion défaillante
-------------------------------------------------------------------------------
Que se passe t'il en cas de non reception de donnée sur le site central?
D'où vient le problème? Perte de connexion? Capteur defectueux? Système embarqué du site distant défaillant?
![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/7%20-%20Sauvegarde%20evenements%20sur%20le%20site%20isole%20connexion%20defaillante/general.png "general")
Il faut s'adapter selon les cas.  
Si c'est la connexion qui est défaillante, le système embarqué du site distant 
doit déclencher une procedure de sauvegarde locale des données.

Si défaillance des capteurs, lever d'alerte selon importance du capteur et criticité du site.
Si la connexion se rétablit il s'agit de transmettre les données qui n'ont pas 
pu l'être et sur le site central gérer l'alerte qui avait été lancée par la perte
de connexion. (Faut il ignorer l'alerte? Envoyer quelqu'un malgré un retour à la
 normale?)
 ![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/7%20-%20Sauvegarde%20evenements%20sur%20le%20site%20isole%20connexion%20defaillante/sauvergarde-locale.png "sauvegarde locale" )
 ![Portal](https://raw.github.com/Hexanome4113/projet-ingenierie/master/images/ProblemDiagrams/7%20-%20Sauvegarde%20evenements%20sur%20le%20site%20isole%20connexion%20defaillante/transmettre-donnees.png "transmettre donnees" )
   
Une perte de connexion pourrait être tolérée momentanément. Lever une alerte en cas
 de problème persistant avec crititicité selon type du site et durée de défaillance.
Du point de vue du site central, comment différencier une perte de donnée due à 
un problème de connexion, d'un problème lié au système embarqué présent là bas?  
On ne peut pas. C'est pourquoi il faut lever une alerte selon le dernier état connu
 des capteurs, la criticité du site et la durée de "non réponse" du site.  
 
Il est possible d'identifier si le problème ne vient que d'un capteur. En effet 
la connexion existe toujours dans ce cas là, il s'agit d'une absence de donnée à
 transmettre. Cette fois encore il faut lever une alerte.
 
