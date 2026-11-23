# TD1 : Basic Git

> [!Warning]
> A chaque fois, dans mes documents, que vous voyez des éléments entre chevrons `<>`,
> cela signifie qu'il faut remplacer cet élément, **chevrons compris**, par l'information indiquée.  
> Par exemple, `<username>` sera à remplacer par votre nom d'utilisateur, comme `esirem-chassel` et non `<esirem-chassel>` !

## Vérification : Installation

Documentation Git avec support d'installation : https://git-scm.com/

Une fois Git installé, vérifiez sa version : `git --version`
Une version 2 ou plus est suffisante.

Configurons Git de manière globale pour indiquer votre nom d'utilisateur et votre email.
Ces informations seront reprises automatiquement à chaque commit.

`git config --global user.name "<username>"`  
`git config --global user.email "<email>"`  

Depuis la fin des années 2010, l'ensemble des acteurs ont commencé à stopper l'usage de termes tels que `master`.  
Dans cette optique, Gitlab, Github et la majorité des outils informatiques ont arrêté l'usage de `master` en branche par défaut pour `main`.  
Git, parce qu'utilisé par de nombreux outils de manière automatique, a prévu ce changement depuis 2025 pour la fin 2026. Mais vous pouvez de suite effectuer les changements pour que votre Git initialise une branche `main` au lieu de `master` par défaut :

`git config --system init.defaultbranch main`

Cette configuration est à réaliser avant même la création de votre premier dépôt.

## Créer un dépôt

Pour créer un dépôt, vous avez deux choix principaux : le faire depuis un hébergement distant (`remote`) pour le rapatrier ensuite, ou le faire en local pour le lier à un hébergement distant par la suite.

> [!Info]
> Chaque méthode a ses avantages et inconvénients.
> Vous devez donc les connaître.

### Version distante

Allez directement sur votre hébergement distant (Github, Gitlab...) et créez votre dépôt.
Puis, en local, effectuez un clone du dépôt en utilisant l'URI communiquée par votre hébergement.

`git clone <URI> <path>` va cloner le dépôt `<URI>` dans le dossier `<path>`.
Si `<path>` est omis, un dossier va être automatiquement créé avec le nom du dépôt.

Pour rappel, le clone fait automatiquement le lien entre votre dépôt local et le remote, généralement nommé `origin` par défaut.

### Version locale

Dans le dossier de votre projet, effectuez un `git init`.
Votre dépôt git est créé !

Attention, il est créé en local, mais ne possède aucun remote.
Une fois votre dépôt créé sur votre hébergement distant, il faudra le lier, en ajoutant le remote.

`git remote add origin <URI>`

Ici, on ajoute un `remote` nommé `origin` situé à l'URI `<URI>`. Pour rappel, cette URI est donnée par votre hébergement distant.

> [!Caution]
> Lors de la création de votre dépôt sur votre hébergement distant,
> il est déconseillé d'activer les options ajoutant des fichiers (README.md, licences, ignore...).
> Cela pourrait créer des conflits dès votre première opération et vous compliquer singulièrement la vie trop rapidement !

### A vous de jouer !

Créez un dossier `test` dans votre répertoire personnel,
dans lequel vous allez placer un fichier "README.md" dans lequel vous allez simplement écrire "Bonjour !".

Créez votre dépôt en local.

Observez vos fichiers (y compris les fichiers et dossiers cachés); que remarquez-vous ?

Créez votre dépôt sur Github, en le nommant "first-test". **Attention à ne pas cocher d'options de création de fichiers !**  

Liez vos dépôt via `git remote` comme indiqué dans la page de Github.

## Vos premières modifications

Les cinq commandes basiques à connaître dans Git pour une utilisation des plus basiques sont les suivantes :
- `status` : affiche le statut du dépôt
- `add` : ajoute un chemin au prochain commit
- `commit` : effectue un commit
- `push` : envoie tous les commits sur le remote
- `pull` : rapatrie tous les commits depuis le remote et les applique

### Statut

Effectuez un `git status`. Que constatez-vous sur votre dépôt ?

### Ajout

La commande `git add <path>` permet d'ajouter un chemin `<path>` au prochain commit.  
Cette commande est récursive; tous les chemins descendants de ce `<path>` seront ajoutés.

Ajoutons donc votre fichier `README.md` à votre prochain commit : `git add README.md`.

Visualisez à nouveau le statut de votre dépôt. Que constatez-vous ?

### Commit

La commande `git commit` permet de créer un commit. Lancez donc la commande. Que se passe-t-il ?

Eh oui, un commit DOIT posséder certains éléments :
- un auteur, identifié par un nom et un email; vous avez déjà rempli cela !
- une date, automatiquement
- un identifiant, automatique également
- un message, identifiant le "pourquoi" ce commit

Or, il manque ce dernier élément.
Git vous ouvre donc votre éditeur textuel par défaut pour que vous puissiez saisir votre message de commit.

> [!Tip]
> Si vous avez de la chance, cet éditeur est `nano`. Auquel cas, vos raccourcis (avec `Ctrl+`) sont indiqués en bas.  
> Si vous avez moins de chance, il s'agit de `vi`, auquel cas la tocuhe de raccourci est `:` (mais une fois que vous avez utilisé `Echap`) suivi de la commande (par exemple, `wq!` pour quitter après écriture sans confirmation). 

> [!Tip]
> Vous pouvez zapper cette ouverture déplaisante en indiquant un argument `-m` dans votre commande, pour indiquer votre message de commit :
> `git commit -m "<message>"`

Créez donc un commit `Premier commit !`.

### Push

Effectuez donc un `git status` à nouveau. Que constatez-vous ?

Votre commit est bien présent, en local, mais il n'a pas été *poussé* sur le *remote*.
Il est temps de le faire : effectuez un `git push`.

Félicitation !

### Pull

Le pendant de `push` pour envoyer est `pull` pour recevoir.

Allez donc sur votre dépôt Github, puis modifiez, directement dans l'interface, votre fichier `README.md` pour remplacer "Bonjour !" par "Bonjour le monde !".

Revenez sur votre dépôt local, et lancez un `git status`. Que se passe-t-il ?

> [!Important]
> De manière générale, tant que vous n'effectuez aucune opération de rapatriement d'informations (fetch, pull...), Git n'aura aucune idée que quelque chose a changé.

La bonne pratique est de systèmatiquement `pull` un projet avant de développer. On verra les branches par la suite, mais d'abord, afin d'éviter un conflit, nous allons rapatrier l'ensemble des commits et les appliquer.

Effectuer un `git pull`. Que constatez-vous ?

## Et plus !

Maintenant que vous êtes capables de réaliser le strict minimum coté Git, passons à des notions plus larges dont vous aurez besoin dans tout projet avec plus d'une personne.

Ce joli site vous accompagnera sur cette excursion : https://learngitbranching.js.org/?locale=fr_FR

**Appellez bien votre enseignant pour valider chaque "grande" partie ("Séquence d'introduction", "Montée en puissance" ...).**
