# Git  - TP Branches et commit

# Rappels

## Initialiser un nouveau répertoire

Pour créer un nouveau répertoire suivi par GIT tapez:

```
$ git init tpgit
```

Cette commande crée le répertoire tpgit et le sous répertoire tpgit/.git dans lequel est stocké l'historique de votre projet.

Entrez dans le répertoire de travail:

```
$ cd tpgit
```

## S'identifier pour les futurs commits

Il est important (surtout en équipe) de savoir qui a fait quoi. Pour identifier vos futurs commits, tapez les commandes suivantes:

```
$ git config --global user.name "votre nom"
$ git config --global user.email "votre email"
```



Remarque: l'option -g permet de définir ces propriétés globalement pour tous vos répertoires suivis par GIT. Si vous l'omettez, les propriétés seront spécifiques au projet courant. Tapez `git config --list` pour visualiser toutes les propriétés de votre environement.

GIT comporte 3 espaces, on parle des 3 arbres de GIT:

- le **répertoire de travail** (**working directory**, en anglais): c'est là que vous faites toutes vos modifications.
- l'**index** ou **zone de staging** (**index** ou **staging area  ou **, en anglais): zone de transit avant la validation des modifications.
- le **dépot** (**git repository**, en anglais): l'ensemble des modifications validées, reliées entre elles.







# Exemple avec Python et git



#### Créer un dossier `TP_GIT_PYTHON_1`

```
mkdir tp_git_python_1

cd tp_git_python_1
```

### initialiser un dépot git vide

```
git init 
```

#### Créez deux fichiers dans le dossier

readme.md

```md
##Ceci est un TP Git et Python
```

hello.py

```python
print("Hello ESNL")
```

### Visuliser le statut

![image-20220202123759945](/home/laurent/.config/Typora/typora-user-images/image-20220202123759945.png)

![Screenshot](https://www.cristal.univ-lille.fr/TPGIT/images/04-commithello.svg)



### Ajouter les fichiers à l'index

```
 git add hello.py
 git add readme.md
 // Ou alors
 git add .
```

### Re-visualiser le statut

```
git status
```

![image-20220202124935620](/home/laurent/.config/Typora/typora-user-images/image-20220202124935620.png)

### Commit

```
git commit -m 'Initialisation du projet'
```

![image-20220202125102377](/home/laurent/.config/Typora/typora-user-images/image-20220202125102377.png)

### Ajout de la procédure 'ecrire()'

Ajouter la function 'ecrire()', pour obtenir le contenu suivant :

```python
def ecrire(chaine):
    print chaine

print "Hello world!"
```

--------------

## Testez ensuite les différentes commandes git présentées sur : 

[Git CheatSheet](https://ndpsoftware.com/git-cheatsheet.html#loc=index;)

### Commandes de base

Le processus de commit avec Git est  :

1. On développe en modifiant / déplaçant / supprimant des fichiers ;
2. Quand une série de modification est cohérente et digne d'être commitée, on la place dans la zone de staging ;
3. On vérifie que l'état de la zone de staging est satisfaisant ;
4. On committe ;
5. et on répète… 

- Pour copier un fichier du répertoire de travail vers la zone de staging, on utilise ***git add***.
- Pour sauvegarder la zone de staging dans le dépôt git et créer un nouveau commit, on utilise ***git commit*.**
- Pour copier un fichier du dépôt Git vers la zone de staging, on utilise ***git reset*.**
- Pour copier un fichier du staging vers le working directory (donc supprimer les modifications en cours), on utilise ***git checkout***.
- Pour visualiser les modifications entre le répertoire de travail et la zone de staging, on utilise ***git diff***
- Pour visualiser les modifications entre la zone de staging et le dernier commit, on utilise ***git diff --cached*.**



--------------



# TP2 Apprendre les branches avec un sandBox.

[Learn branching](https://learngitbranching.js.org/?demo=&locale=fr_FR)

## Commandes disponibles

Il existe une large variété de commandes git disponibles dans le mode bac à sable. Sont incluses :

- commit
- branch
- checkout
- cherry-pick
- reset
- revert
- rebase
- merge

## Commits Git

Un commit dans un dépôt (repository) git enregistre une image (snapshot) de tous les fichiers du repertoire. Comme un Copier-Coller géant, mais en bien mieux !

Git fait en sorte que les commits soient aussi légers que possible donc il ne recopie pas tout le répertoire à chaque commit. **En fait, git n'enregistre que l'ensemble des changements ("delta")** depuis la version précédente du dépôt. C'est pour cette raison que la plupart des commits ont un commit parent 

> Pour cloner un dépôt, il faut décompresser ("résoudre") tous ces deltas. C'est la raison pour laquelle la commande écrit :
>
> ```
> resolving deltas
> ```
>
> lorsque l'on clone un dépôt.

On peut considérer les commits comme des snapshots du projet. Les commits sont très légers et passer de l'un à l'autre est très rapide !

### Modifier le message du précédent commit

Si vous n'êtes pas satisfait de la qualité du message de votre dernier commit, modifier le en utilisant 

```
$ git commit --amend
```







## Branches Git

On utilise les branches tout le temps, ou presque. 

- Pour tester une fonctionnalité. 
- Pour isoler un développement un peu long.
- Pour mettre quelques commits de côté. 
- Pour développer sans "péter" la branche principale. 
- Pour corriger un bug sans impacter le développement d'une fonctionnalité parallèle. 

Les branches sous Git sont incroyablement légères. Elles sont simplement des références sur un commit spécifique -- rien de plus. C'est pourquoi beaucoup d'enthousiastes répètent en cœur :

```
des branches le plus tôt possible, et des branches souvent
```

Parce qu'il n'y a pas de surcoût (stockage/mémoire) associé aux branches, il est facile de diviser son travail en de nombreuses branches plutôt que d'avoir quelques grosses branches.

> Une branche est un moyen d'exprimer "Je veux inclure le contenu de ce commit et de tous les commits parents."

### Head

Avec Git, il existe une référence spéciale qui s'appelle HEAD. **La référence HEAD pointe vers le commit qui sera le parent du prochain commit.** 

La plupart du temps, HEAD ne pointe pas directement vers un identifiant de commit, mais plutôt vers une branche, (par exemple main ou bugFix).

```
$ cat .git/HEAD
ref: refs/heads/bugFix
```

> La commande **cat** de Linux est l’une des commandes les plus utiles que vous pouvez apprendre. Elle tire son nom du mot concaténer (concatenate en anglais) et vous permet de créer, de fusionner ou d’imprimer des fichiers dans l’écran de résultat standard ou vers un autre fichier et bien plus encore.

Quand vous créez un nouveau commit, il se passe ceci :

1. un nouvel objet commit est créé, avec pour parent le commit pointé par HEAD ;
2. la branche pointée par HEAD pointe maintenant vers ce nouveau commit ;

### Manipuler les branches

On va principalement manipuler les branches grâce à deux commandes :

- `git branch` permet de créer, lister et supprimer des branches.
- `git checkout` permet de déplacer la référence HEAD, notamment vers une nouvelle branche.

On utilise souvent le raccourci suivant, qui est trés exactement équivalent aux deux commandes précédentes :

```
$ git checkout -b nouvelleBranche
```

### Travailler sur des branches

Créer des branches va nous permettre de créer des flots de développement parallèles. 

Chaque commit sera ajouté à la chaîne des commits de la branche courante. 

On connaît la branche courante grâce à la commande *git branch*.

```
git branch
* master
  fixBug
```

### Fusionner des branches (merge)

Quand on a des branches divergeantes,  il faudra bien fusionner toutes ces modifications dans une seule et même arborescence.

C'est à ça que servent les fusions, ou *merge* dans le jargon.

Lorsqu'on fusionne deux branches, Git va intégrer toutes les modifications contenues sur chaque branche dans une seule et même arborescence. **Il va alors créer un commit qui aura deux parents.** 

```
$ git checkout master  # On se place sur la branche qui va "recevoir" les modifications de l'autre branche
$ git merge test  # FuuuuuuuuuuuuSion !
$ git branch -d test  # Une fois fusionnée, notre branche ne sert plus, et peut être supprimée
```

### Résoudre les conflits de fusion

Il peut arriver que la fusion soit impossible à réaliser sans intervention manuelle. Ce sera le cas si chaque branche apporte des modifications différentes au même endroit dans le même fichier. On dit qu'il y a conflit.

Dans ce cas là, Git interrompt le merge et insère des marqueurs dans les fichiers conflictuels. Il nous faudra éditer ces fichiers manuellement (ou à l'aide d'une interface spécifique), avant de poursuivre la fusion.



## Git Rebase

La seconde façon de combiner les contenus de deux branches est *rebase*. Rebase prend un ensemble de commits, les "recopie", et les ajoute en bout de chaîne à un autre endroit.

Bien que cela puisse sembler compliqué, l'avantage de rebase est de permettre d'obtenir une simple séquence linéaire de commits. Les logs/l'historique du dépôt seront bien plus propres si seul rebase est autorisé (plutôt que merge).

#### git rebase permet d'éviter les commits de fusion 

Quand on travaille avec Git, on a tendance à créer beaucoup de petites branches, ce qui est une bonne chose. Par contre, fusionner des branches créé des **commits de fusion**. (H dans l'exemple qui suit)

```
A---B---C---D ← master
     \
      E---F---G ← discussion
      
      
A---B---C---D---H ← master
     \         /
      E---F---G ← discussion      
```









---------------

# Git Add

La commande git-add indexe les modifications qui ont été faites dans les fichiers du répertoire de travail et **prépare ainsi le prochain commit.** Elles possèdent de nombreux arguments qui modifient son fonctionnement.

```
git add *fichier(s) ou dossier(s)*
```

Ajoute à l'INDEX le contenu des FICHIER(S) ou DOSSIER(S), nouveaux ou modifiés, les plaçant ainsi en attente d'inclusion dans le prochain commit. 

```
git add .
// ou
git add -A

```

> Depuis la version 2.0 de git, le fonctionnement de la commande git add . a changé. Cette commande prend maintenant en compte les fichiers supprimés. En conséquence, les commandes **git add -A et git add . ont strictement le même effet.**



```
git add --interactive
// ou

git add -i
```

 Pour ajouter de manière interactive à l'INDEX les contenus modifiés dans l'ESPACE_DE_TRAVAIL.



```
git add -u
```

Ajoute à l'INDEX le contenu des fichiers (ÉXISTANTS) modifiés.

 C'est ce que fait 'git commit -a' en préparation à un commit

# Ignorer des fichiers avec git (.gitignore)



Lorsqu'on utilise git pour gérer son code source, on a parfois besoin de pouvoir ignorer certains fichiers.

> Par exemple, si on  developpe avec un framework on a pas envie de polluer son dépot en comittant par erreur des répertoires de cache, ou la configuration créée par mon éditeur.

De même, on peut vouloir éviter d'insérer dans son dépôt des fichiers temporaires, finissant par ~ ou .tpl.

Pour tout ça, on va utiliser le fichier spécial **.gitignore**.

```
cat .gitignore
cache
log
test
*swp
*~
!toto~
```

Ainsi, tous les fichiers contenant cache, log, test, ou finissant par swp ou ~ seront ignorés. En revanche, l'usage du '!' indique que toto~ sera malgré tout traité.









-----------

# Annexes

## Ajouter un prompt

Utiliser un prompt spécial GIT est très pratique pour visualiser rapidement ou vous en êtes. Pour en configurer un, placez-vous dans votre répertoire personnel:

```
$ cd ~
```

Récupérez ce script et mettez-le dans le répetoire courant (répertoire personnel).

Ensuite, ajoutez les lignes suivantes à la fin du fichier .bashrc (créez-le si il n'existe pas):

```
. ~/git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
export PS1='\u@\h:\w$(__git_ps1 " (%s)")\$ '
```

Retournez dans votre dépot git:

```
$ cd tpgit
```

Mettez à jour votre environement bash (ou reconnectez-vous) :

```
$ . ~/.bashrc
```

Votre promt devrait ressembler à cela:

```
mon_login@ma_machine:~/tpgit (master)$
```

## Personaliser son environnement

Pour certaines commandes vous aurez besoin d'un éditeur de texte. **Ce sera l'éditeur par défaut de votre système qui sera choisi**. Si vous souhaitez en utiliser un autre (par exemple vi):

```
$ git config --global core.editor vi
```

Ajoutez également, pour éviter un message de warning un peu cryptique que GIT affichera lors d'une commande que nous utiliserons bientôt :

```
$ git config --global push.default simple
```









--------------



# 