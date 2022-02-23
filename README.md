# esgi-git-3iwj-2022

## Pré-requis

- Terminal de commande
- OpenSSH
- Git

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

4.10 rebase
4.11 tag
4.12 stash
4.13 mv
4.14 rm
4.15 diff
4.16 remote
4.17 pull
4.18 clone
5 GitHub
5.1 Introduction
5.2 Création d'un compte
5.3 Configuration OpenSSH
5.4 Création d'un dépôt
5.5 Markdown
5.6 README
5.7 Issues
5.8 Pull requests
5.9 Guide de contribution
5.10 License
5.11 Modèle d'issue
5.12 Modèle de pull request
5.13 Milestone
5.14 Projets & Kanban
5.15 Versioning sémantique
5.16 Badges
5.17 GitHub Pages
6 GitHub Action
6.1 Introduction
6.2 Automatisation
6.3 Intégration continue
6.4 Déploiement continu
7 Serveur Git local
7.1 Introduction
7.2 Dépendances
7.3 Administration
7.4 Sécurisation
7.5 Dépôt
7.6 Tests
