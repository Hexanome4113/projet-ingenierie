Rédaction et Gestion de configurations
========

Rédaction
------

### Format des documents ###

Les documents seront rédigés en Markdown. La documentation de Markdown peut être trouvée sur cette page: [Syntaxe Markdown](http://daringfireball.net/projects/markdown/syntax)

Les éditeurs suivants pourront être utilisés dans la rédaction des documents: 

- Editeurs en ligne avec aperçu instantané: [Online Markdown Editor](http://www.ctrlshift.net/project/markdowneditor/) ou [Dillinger](http://dillinger.io/)
- Editeur collaboratif: [The File Tree](https://thefiletree.com/) est fait par des INSAliens et offre un mode aperçu lorsqu'on crée un fichier avec l'extension ``.md``. Tous les fichiers sont publics, il suffit de donner l'url à quelqu'un pour qu'il puisse éditer en direct le fichier. Pensez à le vider une fois le travail fini.
- Editeur desktop: [Sublime Text 2](http://www.sublimetext.com/2) fait nativement de la coloration syntaxique (assez basique) du Markdown.  Des plugins sont très facilement installables pour rajouter un meilleur support et des fonctionnalités plus avancés comme le pliage des sections, l'aperçu, etc.


### Recommandations de rédaction ###
* Nommage du fichier: Pas d'espaces. Des underscores ``_`` peuvent être utilisés à la place.
* Eviter le plus possible les hiérarchies de titres profondes. Les différences de niveau de titre ne sont pas flagrantes et ne rendraient donc par très bien.
* Se reporter à la section [Gestion des configurations](#gestion-de-configurations) pour les instructions relatives à la validation du document et au marquage du numéro de version.

### Images ###
Les images seront ajoutées dans le dossier image sur github pour pouvoir être intégrées aux documents. Le format recommandé est le PNG

### Impression ###

Elle se fera systématiquement à partir de github pour garder la cohérence d'interprétation du Markdown. Pour obtenir le document imprimable sans tous les éléments d'interface de github, il est possible d'utiliser ce bookmarklet pour obtenir une page épurée et ensuite imprimer en faisant ``Ctrl+P``

Code:
```javascript
javascript:(function(e,a,g,h,f,c,b,d)%7Bif(!(f=e.jQuery)%7C%7Cg%3Ef.fn.jquery%7C%7Ch(f))%7Bc=a.createElement(%22script%22);c.type=%22text/javascript%22;c.src=%22http://ajax.googleapis.com/ajax/libs/jquery/%22+g+%22/jquery.min.js%22;c.onload=c.onreadystatechange=function()%7Bif(!b&&(!(d=this.readyState)%7C%7Cd==%22loaded%22%7C%7Cd==%22complete%22))%7Bh((f=e.jQuery).noConflict(1),b=1);f(c).remove()%7D%7D;a.documentElement.childNodes%5B0%5D.appendChild(c)%7D%7D)(window,document,%221.3.2%22,function($,L)%7B$('%23header,%20.pagehead,%20.breadcrumb,%20.commit,%20.meta,%20%23footer,%20%23footer-push,%20.wiki-actions,%20%23last-edit,%20.actions,%20.header').remove();%20$('%23files,%20.file').css(%7B%22background%22:%22none%22,%20%22border%22:%22none%22%7D);%20$('link').removeAttr('media');%7D);
```

Rappels sur l'utilisation des bookmarklets :

>**Ajouter un bookmarklet:** Créer un nouveau favori, puis coller le code javascript ci-dessus dans le champ URL

>**Utiliser un bookmarklet:** Il suffit de cliquer dessus. Au vu des fonctionnalités attendues de celui ci, il est évident qu'il faut d'abord aller sur une page github affichant un markdown avant de l'utiliser.


Gestion de configurations
--------

### Contrôle des modifications ###

La plateforme de gestion des documents choisie est GIT. Ainsi, les fonctionnalités suivantes sont disponibles nativement
- Gestion de l'historique, avec un traçage du responsable, de la date, de la description des changements, etc
- Visualisation des modifications entre différentes versions
- Récupération de versions précédentes
- etc.

En parallèle, une identification des versions significatives est faite grâce à un [document tableur](https://docs.google.com/spreadsheet/ccc?key=0AsECmMGkrcOvdEg2aWI0RzZZYXBHeXBxN2tIbU9iS3c#gid=0).
Ainsi, à chaque version significative, les informations suivantes doivent être renseignées:
- Nom du document
- Lien vers le document: ``=hyperlink("lien";"nom_document.md")``
- Numéro de version
- Date
- Identifiant de commit
- Responsable


### Suppression ou renommage d'un fichier ###

Il faut éviter tant que possible toute suppression ou renommage d'un fichier, en particulier en raison des liens pouvant exister entre les documents. Suppression et renommage doivent donc faire l'objet d'une demande auprès du responsable qualité. Il sera chargé de s'assurer de l'intégrité des autres documents pouvant référencer le document à modifier.


### Conventions d'identification ###

L'attribution des numéros de version se fait sous la supervision du Responsable Qualité, après validation du document.
Chaque document, à sa création, a pour version 0.1
La numéro de version majeure du document est incrémentée à la validation du document en prévision d'une présentation au client, ou lorsqu'un objectif majeur est atteint (fin d'itération).
Les changements intermédaires (travail d'une séance par ex) incrémentent le numéro de version mineure.


### Livraison des articles de configuration ###

A chaque livraison, le document de [traçage des livraisons](https://docs.google.com/spreadsheet/ccc?key=0AsECmMGkrcOvdEg2aWI0RzZZYXBHeXBxN2tIbU9iS3c#gid=1) doit être mis à jour.
Il associe à chaque livraison la liste des documents concernés et leur version respective
