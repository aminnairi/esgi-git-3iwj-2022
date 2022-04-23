# esgi-git-3iwj-2022

https://github.com/aminnairi/esgi-git-3iwj-2022

## Pré-requis

- Terminal de commande
- [OpenSSH]()
- [Git](https://git-scm.com/)

## Contrôles continus

- [X] Premier contrôle continu
  - Date : 25/03/2022
  - Sujet : tout jusqu'au chapitre sur les [rebase](#modifier-l-historique)
- Deuxième contrôle continu : date à prévoir

## Examen

- Date à prévoir

## Références

- [GitKraken (client Git graphique)](https://www.gitkraken.com/)
- [Fish (Shell avec configuration par défaut moderne)](https://fishshell.com/)
- [Oh My Fish (framework de configuration pour Fish)](https://github.com/oh-my-fish/oh-my-fish)
- [Zsh (alternative à Bash)](https://github.com/zsh-users/zsh)
- [Oh My Zsh (similaire à Oh My Fish)](https://github.com/ohmyzsh/ohmyzsh)
- [Trello : permet d'organiser ses tâches](https://trello.com/)
- [Jira : permet d'organiser ses tâches dans l'écosystème Atlassian](https://www.atlassian.com/software/jira)
- [GitLab : alternative à GitHub](https://docs.gitlab.com/ee/ci/)
- [Stackedit : permet de prévisualiser du code Markdown dans le navigateur](https://stackedit.io/app#)

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

![image](https://user-images.githubusercontent.com/18418459/155697366-9691c3be-bb38-4046-a531-12cc01c9293f.png)

#### Connexion à un compte

Une fois le compte créer, il suffit de se connecter à la même adresse
https://github.com/

![image](https://user-images.githubusercontent.com/18418459/155697437-c40ca3f7-4c6f-4716-a62c-f0bdddef294e.png)

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

![image](https://user-images.githubusercontent.com/18418459/155697714-1d827bdc-75f5-4b10-b6fd-2b1620f3f1d4.png)

#### Création d'un nouveau projet

Nous pouvons désormais créer un nouveau projet depuis l'interface graphique de
GitHub. Pour cela, il faut se rendre [ici](https://github.com/new). Une fois
que l'on a renseigné un nom pour notre dépôt ainsi qu'une déscription et une
visibilité, on peut cliquer sur `create repository` afin de créer le projet
Git. Nous verrons ensuite comment publier des modification sur ce projet.

![image](https://user-images.githubusercontent.com/18418459/155697826-2689818c-f12e-4d02-bb79-d6dbeef3baa4.png)

### Git

#### Introduction

Git est né de la volonté des développeurs du noyau Linux de se soustraire à la
dépendance aux logiciels propriétaires d'historisation de code comme BitKeeper.
En effet, ce dernier, qui était originellement gratuit et open-source, s'est vu
se transformer en solution propriétaire et payante du jour au lendemain, ce qui
n'a pas plus aux développeurs. Cela a entraîné notamment Linus TORVALDS, à
l'origine de la création du noyau, à développer son propre outils
d'historisation de code qu'il a nommé Git.

L'avantage de Git par rapports à d'autres solutions propriétaires similaires et
qu'il est décentralisé, donc sa gestion est plus simple, et son déploiement
également puisqu'il n'y a pas de serveur : tout ordinateur peut devenir un
dépôt d'historique des changements apportés à un projet. Linus en a également
profité pour améliorer certains aspects du logiciel BitKeeper en apprenant des
choses que ce dernier faisait de mal comme être rapide, simple à utiliser et
être capable de pouvoir s'utiliser sur des très larges projets comme le noyau
Linux.

#### Configuration

Avant de pouvoir commencer à utiliser la commande `git`, il est nécessaire d'ajouter au minimum un nom d'utilisateur et une adresse email. Il est recommandé d'utiliser le même nom d'utilisateur et adresse email qu'utilisé sur GitHub.

```bash
git config --global user.name "aminnairi"
git config --global user.email "anairi@esgi.fr"
```

La commande `git config` permet de configurer un paramètre pour Git. l'option `--global` permet d'ajouter une option globale à tous les dépôts. Mais il est également possible d'avoir une configuration locale à un dépôt en particulier.

```bash
git config --local user.name "anairi"
git config --local user.email "anairi@esgi.fr"
```

De cette manière, la configuration ne sera pas partagé avec d'autres dépôts. La configuration est écrite dans le fichier `.git/config`. Il n'est pas recommandé de modifier le fichier directement sauf si vous êtes sûr de ce que vous faites.

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

#### Étapes d'un fichier

Un fichier suit un certain nombre d'étapes simples mais qu'il est important de
bien comprendre avant de pouvoir être ajouté effectivement dans l'historique.
Il est d'abord surveillé, c'est-à-dire que Git sait qu'un fichier a été créé ou
modifié, ensuite il est ajouté en attente d'historisation, puis avec un message
on l'ajoute à l'historique Git.

![image](https://user-images.githubusercontent.com/18418459/155701150-11c78e1a-802b-46bd-b758-25ee6b71f842.png)

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

#### Exercice

Créer un projet Git, et ajoutez un fichier `README.md` qui contient le texte `#
github`. Vous synchroniserez les changements apporter en local avec un dépôt
que vous créerez sur la plateforme GitHub.

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

#### Supprimer une branche

Si une branche créé n'est plus nécessaire, on peut la supprimer de notre
historique Git.

```bash
git branch --delete my-branch
```

À noter que les branches sont détruites localement, si l'on souhaite supprimer
une branche distante, il ne suffit pas de pousser ses changements et il faut le
faire explicitement.

```bash
git push --delete origin my-branch
```

Cela aura pour effet de supprimer effectivement la branche distante.

#### Changement de branche

Créer une branche n'est pas suffisant puisqu'il sera nécessaire de changer la
branche en cours d'utilisation.

```bash
git checkout new-documentation
```

En utilisant la commande `git` ainsi que l'option `checkout` nous pouvons
changer de branche à tout moment, en l'occurrence ici `new-documentation`.

Il est également possible de créer une branche et d'utiliser cette branche
directement en une seule commande.

```bash
git checkout -b new-branch
```

#### Publication de branche

Si l'on souhaite reprendre son travail plus tard sur une autre machine, ou que
l'on souhaite synchroniser son travail pour des raisons de sécurité, il est
possible de synchroniser une branche vers un dépôt distant.

```bash
git push origin new-documentation
```

Cela aura pour effet de publier le contenu de la branche directement sur
l'origine choisie. Un `git push` ne suffit pas et ne publie pas automatiquement
les branches.

#### Fusion de branches

Une fois que nous avons fini de travailler sur notre branche, nous pouvoir
fusionner les changements de l'une des branches vers une autre.

```bash
git checkout development
git merge new-documentation
git branch --delete new-documentation
git push --delete origin new-documentation
```

Ici, nous utilisons la commande `git checkout` afin de nous déplacer vers notre
branche principale qui est ici `development`. Puis, nous utilisons la commande
`git merge` afin de fusionner notre branche courante depuis une autre branche,
en l'occurrence la branche `new-documentation`. Enfin, puisque nous avons
terminé les changements et que notre branche de travail n'est plus nécessaire,
nous pouvons la supprimer en utilisant la commande `git branch` avec l'option
`--delete` afin de supprimer la branche souhaitée, ici `new-documentation`,
localement et sur l'origine.

#### Exercice

Créer une nouvelle branche `new-documentation` qui contiendra le contenu de
votre choix au fichier `README.md`. Une fois que cela est fait, vous publierez
la branche sur le dépôt GitHub. Enfin, vous fusionnerez les changements vers la
branche principale et vous supprimerez les branches localement et sur votre
origine.

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

Une fois que cela est fait, il est nécessaire d'ajouter les changements à
l'historique.

```bash
git add .
```

Le `.` ici est un alias vers le dossier courant sur lequel nous sommes dans le
Shell. Cela signifie que cela ajoute tous les fichiers surveillé à enregistrer
dans l'historique. Puisque le `rebase` est une opération potentiellement
destructrice, il est nécessaire de forcer une synchronisation vers une origine.

```bash
git push --force
```

#### Exercice

Remplacer tous les commits effectués jusqu'à présent par un seul et même
commit. Vous vérifierez sur l'origine que le dépôt distant ne contient plus
qu'un seul commit et que les changements sont toujours présents.

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

Pour synchroniser la nouvelle version, il est possible d'utiliser la commande
`git push` en renseignant après l'origine le nom de la version.

```bash
git push origin 0.1.0
```

Désormais, notre version apparaît sur GitHub et pourra être récupéré. Si l'on
s'est trompé sur une version, il est possible de la supprimer localement et à
distance.

```bash
git push --delete origin 0.1.0
git tag --delete 0.1.0
```

#### Version sémantique

Une version sémantique est un standard permettant de facilement reconnaître une
version dans un logiciel. Elle se compose de trois parties :

- Une version majeure
- Une version mineure
- Une version de correctif

Ces trois parties sont séparées par un symbole point (`.`). Les versions
commencent à partir de `0.1.0`.

Lorsque l'on modifie son projet et que l'on publie de nouveaux correctifs de
sécurité par exemple, on incrémente l'identifiant correspondant. Par exemple,
si je suis en version `0.1.0`, je passerais donc après le correctif en version
`0.1.1`. Si je suis en version `1.0.1`, je passerais en version `1.0.2`.

Lorsque l'on ajoute de nouvelles fonctionnalités, on incrémente la version
mineure. Par exemple, si je suis en version 0.1.0, je passe en version 0.2.0
après ajout d'une nouvelle fonctionnalité. Si je suis en version 1.0.1, je
passe en version 1.2.0, la version de correctif est réinitialisée dans ce cas.

Enfin, lorsque j'ajoute des changements qui entraîne une changement lourd du
logiciel et qu'une simple mise à jour n'est pas suffisante (par exemple,
changer tout une manière d'appeler une fonction), j'incrémente la version
majeure. Si je suis en version 0.1.0, je passe en version 1.0.0. Si je suis en
version 1.2.4, je passe en version 2.0.0. Notez que la version mineure et de
correctif sont toutes deux réinitialisées.

#### Exercice

Ajoutez un lien vers votre dépôt GitHub personnel dans le fichier `README.md`.
Ensuite, publiez une nouvelle version. Choisissez la version la plus adaptée à
ce cas de figure.

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

Ici, nous pouvons voir que dans ce fichier, il y a un conflit entre deux
développeur qui ont modifiés la même ligne avec deux textes différents. Nous
pouvons modifier le fichier afin d'appliquer les bons changements.

```
# Conflict Test
```

Après réflexion avec le développeur, nous nous mettons d'accord pour adopter ce
titre. Nous avons résolu le conflit, il ne nous reste plus qu'à apporter les
modification dans notre historique.

```bash
git add README.md
git commit --message "resolved conflict for the title"
git push
```

Nous venons d'enregistrer les modification après résolution du conflit et nous
avons poussé les changements sur notre dépôt distant pour synchronisation.

#### Exercice

Ajouter un collaborateur à votre projet, puis modifiez la même ligne du même
fichier. Tentez ensuite de vous mettre d'accord pour choisir la ligne à
retenir, résolvez les conflits et synchronisez tous sur le dépôt distant.

### Collaboration

#### Issues

Une issue permet d'organiser les différentes fonctionnalités de notre application et de les répartir entre tous les collaborateurs.

Une issue à un titre et un contenu. On peut également lui affecter un ou plusieurs assignee (un responsable), un label, un projet, un milestone.

Il est possible de créer des discussions communautaire autour d'une issue, de discuter de sa pertinence, de challenger les idées qui sont soulevées etc...

#### Labels

Les labels permettent de catégoriser une issue ou une pull request.

Il est possible d'ajouter plusieurs catégories de label à une seul issue ou pull request.

Il est également possible de créer ses propres labels, avec un nom, une description et une couleur permettant de l'identifier facilement.

Enfin, il est possible de modifier ou supprimer les labels. Certains labels sont déjà existants et ne correspondent probablement pas au projet sur lequel on souhaite travailler.

#### Milestones

Un milestone est un jalon, c'est-à-dire un moment important du développement de notre projet.

Cela permet de se donner des délais à respecter pour proposer un changement important dans la vie d'un projet, il est donc possible de créer des milestones pour des versions à publier, par exemple un milestone pour une future version 2.0.0.

Un milestone a un titre, une description et optionnellement une date à laquelle la milestone doit être achevée.

Une milestone comprends un ensemble d'issues ou de pull request qu'il est possible de lier à cette dernière.

#### Pull requests

Nous avons vu qu'il était possible de s'organiser en branches dans un dépôt. Cela permet de séparer le travail à faire sur une fonctionnalité en particulier. Nous avons également vu qu'il était possible, une fois le travail sur une branche terminé, de fusionner les changements vers une autre branche comme la branche principale par exemple.

Cela est également possible via GitHub et son interface de pull request.

Au lieu de fusionner les changements de nos branches nous-mêmes, nous allons proposer d'ouvrir une pull request pour une branche que nous souhaitons fusionner.

L'intérêt est de pouvoir proposer aux autres collaborateurs la possibilité de pouvoir effectuer des revues de code, cela est donc une très bonne pratique à adopter en travail collaboratif.

Il est possible de lier une issue à une pull request en utilisant les mot-clés `Closes #3` pour pouvoir fermer l'issues #3 par exemple, cela permet, une fois la pull request résolue, de pouvoir automatiquement fermer une issue. Cela ajoute une couche d'automatisation non negligeable lorsque nous travaillons sur plusieurs dizaines de pull request et issues en même temps.

#### Project

Un projet est un type d'organisation spéciale qui permet de simuler les bonnes pratiques liées aux méthodes Agiles et Scrum puisqu'il est possible de retrouver toutes les catégories de tâches (à faire, en cours, fait) dans un projet lorsqu'il est créé en mode Kanban.

Si l'on créé une pull request ou une issue, il est possible de lier ces derniers à un projet, permettant de facilement tracker son progrès au travers de notre projet Git. C'est une manière de voir le dépôt de plus loin et d'avoir une vue d'ensemble sur ce qu'il reste à faire.

Il est possible d'automatiser tout un projet en choisissant le mode Kanban with reviews.

Dans ce mode, les issues et les pull request sont automatiquement déplacées dans les bonnes colonnes en fonction de si une issue est ouverte ou fermées, si une pull request est en attente de revue de code ou non, etc...

#### Exercice

Par groupe de deux ou plus :
- Créer un dépôt Git sur GitHub avec le nom de votre choix
- Créez des issues sur une idée de projet (un site internet, une librairie, etc...)
- Créez des branches et ajouter des modification permettant de répondre à ces issues
- Créez une pull request par branche et faites valider votre code par un membre de votre équipe
- Simulez des requêtes de changement sur vos pull request (vous n'êtes pas d'accord sur une partie du code)
- Automatiser votre workflow avec un Project
- Montrez le résultat de tout cela lors d'un exemple préparé avec vos camarades

### Open Source et bonnes pratiques

#### README.md
#### Description
#### Guide de contribution
#### License
#### Modèles d'issues
#### Modèles de Pull Request
#### Badges


