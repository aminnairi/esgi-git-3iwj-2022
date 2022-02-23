## Création d'un dossier

Avant de créer un dépôt, il faut créer un dossier.

```bash
mkdir repository
cd repository
```

## Création d'un dépôt

Créer un dépôt permet de créer un dossier `.git` qui contient l'historique des fichiers modifiés. Ne supprimez pas ce dossier, sinon vous perdez tout votre historique.

```bash
git init
```

## Création d'un fichier initial

Pour commencer à utiliser Git, il suffit de créer un fichier.

```bash
echo "# repository" > README.md
```

## Ajout du fichier dans les fichiers à enregistrer

Pour pouvoir enregistrer les changements d'un fichier, il faut d'abord ajouter le fichier à l'historique courant.

```bash
git add README.md
```

Si on a beaucoup de fichier à ajouter, il est possible de tous les ajouter en une seule fois.

```bash
git add .
```

## Enregistrement des changements du fichier dans l'historique

Pour enregistrer les changements apportés au fichier, il faut l'enregistrer avec un message permettant de résumer rapidement les changements.

```bash
git commit --message "Initial commit"
```

## Ajout d'un dépôt distant

Pour pouvoir changer facilement d'ordinateur de travail ou pour sauvegarder son historique à plusieurs endroits, il est possible d'enregistrer une origine vers un autre dépôt distant.

```bash
git remote add origin root@localhost:repository.git
```

Si l'on s'est trompé, il est possible de modifier l'origine de nouveau.

```bash
git remote set-url origin root@localhost:repository.git
```

Il est également possible d'avoir plusieurs origines

```bash
git remote add upstream git@github.com:user/repository.git
git remote add upstream git@gitlab.com:user/repository.git
```

## Synchroniser les changements

Pour pouvoir synchroniser les changements, il faut pousser les différences sur les différentes origines.

```bash
git push origin development
```

Ici, `development` fait référence à la branche à synchroniser. Une branche est un dossier virtuel dans lequel nous travaillons. Par défaut, c'est la branche `master` qui est créée. Dans cet exemple, nous avons utilisé une autre branche.
