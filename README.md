# esgi-git-3iwj-2022

## Pré-requis

- Terminal de commande
- OpenSSH
- Git

## Contrôles continus

- Premier contrôle continu : date à prévoir
- Deuxième contrôle continu : date à prévoir

## Examen

- Date à prévoir

## Cours

### GitHub

#### Introduction

GitHub est une plateforme en ligne permettant d'héberger un projet Git. Un
projet Git est un projet de développement d'une application qui est historisé,
c'est-à-dire que ses changements sont enregistré dans un fichier qui est
lisible par un client Git. Un client Git est un programme capable de comprendre
et modifier un projet Git.

#### Création d'un compte

Pour pouvoir utiliser la plateforme GitHub, il est nécessaire de se créer un
compte si ce n'est pas déjà fait. Pour cela, il suffit de se rendre sur le site
internet https://github.com/

#### Connexion à un compte

Une fois le compte créer, il suffit de se connecter à la même adresse
https://github.com/

#### OpenSSH

Il sera nécessaire d'avoir une paire de clé publique et privée pour utiliser le
client Git et nous authentifier à la plateforme GitHub. Pour cela, il suffit
d'exécuter la commande suivante.

```bash
ssh-keygen
```

Il vous sera demandé de taper un mot de passe pour pouvoir utiliser cette clé.
Si vous êtes la seule personne à utiliser votre ordinateur, vous pouvez taper
entrée directement pour ne pas avoir à taper de mot de passe à chaque
utilisation de votre clé. Copiez ensuite le contenu de la clé publique.

```bash
cat ~/.ssh/id_rsa.pub
```

#### Clé OpenSSH GitHub

Une fois le compte créé, il faut paramétrer une clé publique OpenSSH qui nous
permettra de nous authentifier lorsque l'on utilisera le client Git. Pour cela,
il suffit d'aller dans ses [paramètres](https://github.com/settings/keys). Il
suffit de séléctionner l'option `New SSH key`, puis de renseigner un nom pour
la clé ainsi que le contenu de la clé. C'est le contenu de la clé publique que
vous avez déjà copié.

#### Création d'un nouveau projet

Nous pouvons désormais créer un nouveau projet depuis l'interface graphique de
GitHub. Pour cela, il faut se rendre [ici](https://github.com/new). Une fois
que l'on a renseigné un nom pour notre dépôt ainsi qu'une déscription et une
visibilité, on peut cliquer sur `create repository` afin de créer le projet
Git. Nous verrons ensuite comment publier des modification sur ce projet.

### Git

#### Initialisation

Pour pouvoir initialiser un dépôt, Il faut tout d'abord créer un dossier de
travail.

```bash
mkdir project
```

Remplacez `project` par n'importe quel nom qui permet de représenter rapidement
votre projet à versionner. Ensuite, il vous suffit de vous déplacer dans ce
dossier.

```bash
cd project
```

Enfin, nous pouvons initialiser le projet Git dans ce dossier.

```bash
git init
```

Un dossier `.git` devrait apparaître à la racine du dossier de votre projet.
C'est dans ce dossier que Git stocke tous ses fichiers de travail afin
d'historiser votre projet. Ne touchez jamais à ce dossier et ne le supprimez
jamais, sauf si vous savez ce que vous faites.

#### Documentation

Pour pouvoir commencer à historiser un fichier, nous allons créer un fichier
Markdown.

```bash
echo "# project" > README.md
```

Le fichier `README.md` est un fichier spécial pour GitHub puisqu'il sera
reconnue comme étant votre documentation de projet.

#### Affichage du status du projet

Il est possible à tout moment de savoir à si des fichiers ont été modifiés ou
créés.

```bash
git status
```

C'est la commande `git` avec l'option `status` qui nous permet de voir l'état
de chaque fichiés historisés qui sont à ajouter, en cours d'ajout, modifiés,
etc...

#### Ajout d'un fichier à enregistrer

Avant de pouvoir historiser notre documentation, il faut d'abord le passer dans
la liste des fichiers à enregistrer.

```bash
git add README.md
```

C'est l'option `add` de la commande `git` qui nous permet de le faire. Elle
prend en paramètre un nom de fichier, en l'occurrence dans notre cas
`README.md`.

#### Historisation du fichier

Nous pouvons maintenant historiser le fichier.

```bash
git commit --message "Initial commit"
```

En utilisant la commande `git` avec l'option `commit`, il est possible
d'enregistrer tous les fichiers qui sont en attente d'historisation. Elle prend
en paramètre une option `--message` qui permet d'attacher un message de log à
notre fichier modifié. À chaque fois que nous changerons le fichier, il sera
possible de l'ajouter de nouveau et de l'historiser.

#### Affichage des historiques

Il est possible d'afficher un historique des changements effectués sur un
projet Git.

```bash
git log
```

Cette commande liste tous les changements qui ont été effectués avec leur hash
et leur message. Les changements sont affichés dans l'ordre du plus récent au
plus ancien. L'auteur ainsi que la date y sont renseignés dans le cas où le
projet est utilisé par plusieurs personnes.

#### Ajout d'une origine distante.

Afin de savoir où publier notre code, il est nécessaire de renseigner une
origine à notre projet Git. Chaque dépôt est décentralisé, c'est-à-dire que
notre projet en local est un dépôt, mais il est possible de synchroniser notre
projet Git à plusieurs endroits afin d'avoir des copies de sauvegardes dans le
cas où notre ordinateur ne serait plus en état de marche par exemple.

```bash
git remote add origin git@github.com:aminnairi/esgi-git-3iw-2022.git
```

La commande `git` ainsi que l'option `remote` nous permettent de manipuler les
origines de notre projet. l'option `add` nous permet d'ajouter une nouvelle
origine. Cette option prend deux paramètres : le nom de l'origine ainsi que son
URL. Ici, nous avons décidé d'appeler notre origine `origin` qui est un nom
classique pour ce genre de cas. L'URL qui suit est l'URL sur le site GitHub,
mais il est aussi possible d'utiliser d'autres sites d'hébergement de projet
Git comme GitLab ou BitBucket. Il est également courant d'avoir plusieurs
origines et ainsi synchroniser son code sur plusieurs dépôts distants
différents.

#### Publier ses changements

Bien que nous ayons correctement configurer une origine, il n'est pas encore
possible de voir nos changements sur la plateforme GitHub. Pour cela, nous
allons publier nos changements.

```bash
git push --set-upstream origin development
```

Pour pouvoir le faire, on utilise la commande `git` ainsi que l'option `push`
cette option prend elle même une option qui est `--set-upstream` qui nous
permet de renseigner une origine ainsi qu'une branche. Généralement, le nom de
la branche fait référence à la branche par défaut qui a été créée par la
commande `git` au moment de l'initialisation de notre dépôt. Si l'on est pas
sûr du nom de la branche, il suffit d'exécuter la commande suivante.

```bash
git branch -v
```

La liste des branches devrait apparaître. Le nom de la branche avec une étoile
sur le côté nous indique la branche actuellement en cours d'utilisation et qui
peut être utilisée pour synchroniser le dépôt distant.

#### Ajout d'une nouvelle branche

Les branches sont un système très puissant car elles permettent de travailler
sur plusieurs dossiers virtuels à la fois, ce qui permet de travailler sur une
nouvelle version du projet, tout en continuant à permettre aux utilisateurs
d'utiliser une ancienne version.

```bash
git branch new-documentation
```

Dans ce cas là, on utilisera la commande `git` avec l'option `branch`. Cette
option prend en paramètre le nom de la branche à créer, ici
`new-documentation`.

#### Changement de branche

Créer une branche n'est pas suffisant puisqu'il sera nécessaire de changer la
branche en cours d'utilisation.

```bash
git checkout new-documentation
```

En utilisant la commande `git` ainsi que l'option `checkout` nous pouvons
changer de branche à tout moment, en l'occurrence ici `new-documentation`.

#### Fusion de branches

Une fois que nous avons fini de travailler sur notre branche, nous pouvoir
fusionner les changements de l'une des branches vers une autre.

```bash
git checkout development
git merge new-documentation
git branch --delete new-documentation
```

Ici, nous utilisons la commande `git checkout` afin de nous déplacer vers notre
branche principale qui est ici `development`. Puis, nous utilisons la commande
`git merge` afin de fusionner notre branche courante depuis une autre branche,
en l'occurrence la branche `new-documentation`. Enfin, puisque nous avons
terminé les changements et que notre branche de travail n'est plus nécessaire,
nous pouvons la supprimer en utilisant la commande `git branch` avec l'option
`--delete` afin de supprimer la branche souhaitée, ici `new-documentation`.

#### Modifier l'historique

Il peut arriver que certains commit fait par erreur entraîne une fuite de
données sensible comme des mots de passes par exemple. Une fois historisés et
publiés, ils ne suffit pas de modifier de nouveau le fichier puisque les
changements fait par le passés sont toujours visibles par les personnes ayant
accès au dépôt. Néanmoins, il est toujours possible de modifier complètement
l'historique.

```bash
git rebase --interactive --root
```

La commande `git rebase` permet de rejouer des enregistrements de modification
de fichier. Il est possible de modifier des messages si l'on s'est trompé, de
supprimer des fichiers historisés, de réunir un ensemble de changements en un
seul enregistrement, et bien d'autres possibilités encore. L'option `--root`
permet de rejouer l'ensemble des enregistrments depuis le début de l'historique
et l'option `--interactive` permet d'afficher de manière interactive l'ensemble
des options disponibles pour manipuler l'historique.

#### Versions

Parfois, nos utilisateurs ont besoin d'utiliser une certaines version de notre
projet, à un point précis de l'historique de ce dernier. Pour faire cela, il
est possible d'apposer des identifiants à notre historiques, comme des
marque-pages.

```bash
git tag --annotate 0.1.0 --message 0.1.0
```

En utilisant la commande `git tag`, il est possible d'ajouter une version
précise à un point de notre historique. Cela est particulièrement pratique dans
le cadre du développement d'une application par exemple. On peut ajouter une
annotation avec l'option `--annotate` ainsi qu'un message de description avec
l'option `--message`.

#### Changements temporaires

Parfois, tout ce que nous souhations faire c'est tester rapidements des choses
sans forcément les enregistrer. C'est pratique notamment si nous sommes en
train de modifier quelque chose, mais que nous avons besoin de rapidement
revenir sur notre branche initiale sans changements.

```bash
git stash
```

Après avoir effectué des modifications sur un fichier historisé, il suffit
d'utiliser la commande `git stash`. Une fois fait, les changements sont ajouter
à un espace temporaire, ce qui nous permet de faire toutes les opérations
nécessaire sur la branche à l'état initial, c'est-à-dire sans modifications. Il
est également possible de faire revenir les changements avec l'option `pop`.

```bash
git stash pop
```

Ceci est particulièrement pratique si nous nous sommes trompés de branche de
travail par exemple.

#### Récupérer des changements depuis une origine

Lorsque l'on travaille à plusieurs, il peut être intéressant de pouvoir
récupérer le travail de chacun lorsque c'est le cas.

```bash
git pull origin development
```

La commande `git pull` permet de récupérer les changements. Optionnellement, il
est possible de lui préciser une origine ainsi qu'une branche à récupérer.

#### Récupérer un dépôt

Les plateformes comme GitHub et GitLab regorgent de projets tous plus
intéressants les uns que les autres. Il peut être intéressant de les récupérer
sur notre ordinateur afin de pouvoir les utiliser localement.

```bash
git clone git@github.com:aminnairi/collatz.git
```

Dans ce cas là, nous utiliserons la commande `git clone` suivi d'une URL nous
permettant de récupérer le projet. Le projet sera créé dans un dossier
contenant le nom du dépôt sans le nom de l'utilisateur et l'extension `.git`.
Il est également possible de donner un chemin spécifique afin de récupérer le
projet dans un autre dossier.

```bash
git clone git@github.com:aminnairi/collatz.git collatz-conjecture-test
```

Dans ce cas-ci, on clone le dépôt dans un nouveau dossier appelé
`collatz-conjecture-test`. Dans tous les cas, si le dossier existe déjà, la
commande echouera.

#### Résolution de conflits

Git permet de travailler à plusieurs sur un projet, néanmoins, il peut arriver
que plusieurs personnes aient besoin de travailler sur un même fichier. Dans ce
cas là, les historiques d'une branche peuvent venir en conflit avec celles
d'une autre. Pour résoudre les conflits, il suffit de séléctionner les
changements à conserver, et supprimer les changements à supprimer. C'est aussi
simple que de modifier un fichier avec son éditeur de texte. Git affiche d'une
certaine façon les changements en provenance d'une branche externe et les
changements fait sur notre propre branche afin de permettre de les identifier
facilement.

```
<<<<< HEAD
# Conflict Test
=======
# Test Conflict
>>>>>>> title-update-2
```

Ici, nous pouvons voir que dans ce fichier, il y a un conflit entre deux développeur qui ont modifiés la même ligne avec deux textes différents. Nous pouvons modifier le fichier afin d'appliquer les bons changements.

```
# Conflict Test
```

Après réflexion avec le développeur, nous nous mettons d'accord pour adopter ce titre. Nous avons résolu le conflit, il ne nous reste plus qu'à apporter les modification dans notre historique.

```bash
git add README.md
git commit --message "resolved conflict for the title"
git push
```

Nous venons d'enregistrer les modification après résolution du conflit et nous avons poussé les changements sur notre dépôt distant pour synchronisation.

### GitHub

#### Issues

Une issue est un ticket que l'on renseigne lorsque nous avons des nouvelles fonctionnalités à rajouter à un projet, un rapport de bug à effectuer, une question à propos d'une partie du projet etc...

#### Pull request

Nous avons vu comment créer des branches pour pouvoir apporter des modifications à un projet.
