# Exercice Git

## Présentation
Le but de ces exercices est d'utilisé git et voir comment travailler avec en equipe.

## Exercice 1: git clone
Le but de cette exercice est de récupérer du code depuis github.

Pour cela vous devez récupérer ce projet.

Cliquez sur le bouton "code" et copiez l'url.

Dans un terminal, choisicez un dossier qui contiendra votre projet.


ouvrez un terminal (shell, cmd ou powershell) et tapez la commande:
```
git clone <url que vous avez copié>
```

git téléchargera le projet.

## Exercice 2: réinitialiser un répértoir git.
Vous avez maintenant le projet sur votre systeme. Mais ce projet est relié avec mon github. Vous devez donc réinitialiser votre git local.

Dans le terminal:
```
cd <nom du projet>
rm .git
```

Le but de ces commande est de suprimer le dossier `.git`. Ce dossier est un __dossier caché__, il faut donc activer les dossier cachés pour le voir dans votre exporateur de fichier. Il contient toutes les informations de notre projet et permet déxecuté les commandes git. Le supprimé permet de supprimer git de notre dossier.

Il faut maintenant reinitialiser votre git local:
Dans le terminal, lancez la commande:
```
git init
```
Cette commande permet de créer le dossier `.git` et donc permet l'utilisation de git. En le recréant, nous avons réinitialisé le git.

Nous pouvons maintenant enregistrer tout les changement sur votre propre git.

git propose un systeme de `remote` qui permet de lui dire quel est le compte qui doit recevoir nos modification.

Créer un nouveau repository sur votre compte github ou gitlab. Il ne faut cocher aucune case.

Vous avez maintenant un exemple de commande pour ajouter votre code a ce repository.

Copier la commande qui ressemble a:
```
git remote add origin <url de votre repo>
```
et executer la dans le dossier.

Vous pouvez maintenant envoyer vos modification au serveur avec la commande suivante:
```
git push -u origin master
```

`origin` est notre _remote_. Il fait referance a votre compte github ou gitlab.
Cette commande dit:
```text
git(git) Envoie(push) mes données au repository avec le remote (origin), appel la branche créer comme master (master) et souvient toi de cette commande (-u).
```

Si vous mettez a jour votre repository sur le site de github u gitlab, vous pourrez voir que l'ensemble du code est maintenant disponible en ligne.

## Exercice 3: Les commits
Git permet de géré des _version_ de notre code. Pour cela il utilise un systeme de `commit`. Ces dernier permettent de permettent de sauvegarder les modifications depuis le dernier commit.

Au debut d'un projet, nous avons rien dans notre projet. Apres avoir créer ou non les permier fichiers et dossier, vous pouvez sauvegarder l'ensemble des modifications dans un `commit`. Si vous faite une ou plusieur modifications, vous pouvez créer une nouvelle sauvegarde non pas du code en entier, mais uniquement des modifications, ajout ou suppression de nos fichier dans un `commit`.

Nous pouvons voir un commit comme un postit ou nous notons les modifications sur certain fichier depuis le dernier postite.

Pour ajouter un fichier a notre postit(commit) nous utilisons la commande:
```
git add README.md
```
Vous avez ajouté les modifications (ici la création du fichier) a votre future postit.

Mais si nous devions ajouter tout les fichier a la main l'ajout de chaque fichier, cela prendrait trop de temps. La commande suivante permet d'ajouter TOUT les fichiers, dossiers non vide et tout les fichiers dans tout les dossier qui se trouve dans le dossier courant.
```
git add *
```
ou 
```
git add .
```
Ces deux commandes sont equivalente.

Apres avoir noté l'ensemble des fichiers, nous alons specifier que nous avons fini d'ecrire nos changement. Git crééra un commit contenant tout les modifications depuis le dernier commit.

```
git commit -m "mon premier commit"
```

Bravo vous avez créé votre premier commit qui porte le message "mon premier commit".

## Exercice 4: git push
Il faut maintenant envoyer le commit sur le repository distant. 

Vous devriez pouvoir utiliser la commande:
```
git push
```

Si cette commande ne marche pas, vous n'avez pas utiliser la premiere fois le -u dans votre commande.
Vous pouvez reexecuté la commande:
```
git push -u origin master
```

## Exercice 5: Les commits a plusieurs.
Pour cet exercice, vous devez faire equipe avec une autre personne.

Par default, vous etes le seul a pouvoir envoyer des modifications sur votre repository distant (qui se trouve sur github ou gitlab). Il faut donc ajouter un autre utilisateur comme membre pour qu'il puisse effectuer des modifications.

Par la suite nous parlerons de 
Utilisateur 1 (qui posséde le compte git)
Utilisateur 2 (celui qui est membre)

L'utilisateur 2 doit récupéré votre git sur sa machine, pour cela il doit exécuté la commande:
```
git clone <url du repository de l'utilisateur 1>
```
### Utilisateur 1

L'utilisateur 1 peut faire une modification dans le fichier `fichier1.py` en modifiant ``numero_de_utilisateur`` avec la valeur 1.

Vous avez aportez une modification a un fichier de ce projet. 
Vous pouvez avoir des informations sur quel sont les fichiers ayant eu des modifications et qui ne sont pas encore dans un commit avec la commande:
```
git status
```

Enregistrez votre modification:
```
git add *
git commit -m "je suis l'utilisateur 2"
```

et envoyer les modifications sur le repository distant avec la commande:
```
git push
```

## Utilisateur 2
Le deuxieme utilisateur peut faire de même en metant le numero 2 au fichier 2.

Quand l'utilisateur 2 voudra envoyer ses données, un message d'erreur s'affiche. 
Normal, il na pas récupéré l'ensemble des modifications sur le repositry distant. Il doit pouvoir les récupérés avant d'envoyer les données au serveur.

Pour récupéré les modifications:
```
git pull
```

Cette commande permet de récupéré les modifications que vous n'avez pas encore.

Apres cela vous pouvez retanté de faire un git push.

Git fonctionne avec un systeme de commits chainés. Chaque commit definie les modofications, un message mais aussi quel est le commit précedant. grace a cela git est capable de récupéré l'ensemble des mofications depuis le debut du projet.

Quand vous n'avez pas les même commits que ceux sur le serveur, votre commit aura le même parent que celui sur le repository distant, il y a donc un probléme. En Récupérant le ou les commits qui vous manque, vous positionnez votre commit apres celui qui etait dans le repository distant. 
Au passage vous avez gagné les modifications du repository distant.

## Exercice 6: Les Conflis
Normelement si on se debrouille bien, le cas précedent est le pmus courant. Mais dans certains cas nous pouvons avoir un confli.

Si les deux utilisateurs modifie le même fichier a la même ligne alors il y aura un confli entre les deux commit.

Par exemple, les deux utilisateurs modifie la ligne 6 du fichier 1, font un commit et le push sur le serveur distant, le dernier aura un message d'erreur lors du push comme vu precedement. Mais cette fois apres un git pull, il aura aussi un message.

Le fichier 1 posséde un confli, git nous laisse alors chosir comment géré le probléme en metant en evidence le probléme de conflit.

Apres avoir choisie la modification a garder grace a votre editeur de text ou IDE favorie, il doit faire un commit puis refaire un push.

Dans cette exemple la modification est petite, mais si un projet est mal découpé entre les developpeurs et qu'ils modifient les même lignes, il peut y avoir de gros confli qui peuvent prendre du temps a résoudre.

## Exercice 7: Les branches.
Pour réduire ces problémes, il existe le systeme de branche.

Il est possible de séparé la sauvegarde des modification (commit) dans une autre branche indépendante. Seul les personnes sur les même branches peuvent avoir des problémes de confli.

chaque utilisateur créer sa branche avec la commande
```
git checkout -b <utilisateur1 ou utilisateur2>
```
Vous avez créé une nouvelle branche qui porte votre nom d'utilisateur. 

Les deux utilisateurs peuvent une nouvelle fois modifier la ligne 6 du fichier 1, faire un commit et poussé les modifications sur le serveur avec la commande:
```
git push -u origin <nom de votre branche>
```

Vous ne devriez pas avoir de probléme de confli.

apres un git pull, vous récupéreré votre branche et celle de l'autre utilisateur. 

Pour le voir, vous pouvez utiliser la commande
```
git branch
```

## Exercice 8: Les merges
Travailler sur sa branche limite les confli mais ne permet pas de travaillé en equipe.

Nous pouvons effectuer nos modifications sur une branche puis rapatrier toutes les modifications sur la branche master pour rassemblé les modifications.

Pour cela nous devons retourner sur la branche master:
```
git checkout master
```

La commande git checkout permet de changé de branche. L'option -b permet de créer une branche si elle n'existe pas encore en local.


Une fois sur la branche master (pour le verifier vous pouvez utiliser la commande git branch, la branche actuelle est notifier par une etoile) vous pouvez demander de récupéré l'ensemble des modifications sur votre branche et de les ajoutés a la branche principale. Pour cela:
```
git merge <nom de votre branche>
```

Pour envoyé cette fusion au serveur distant vous pouvez utiliser la commande git push.

Le dernier a fair cette manipulation aura un probléme de confli.

Le faite de résté sur notre branche nous permet de ne pas géré les conflit a chaque push/pull. Mais lors du merge, il peut toujours y avoir des confli.

Il peut alors géré le conflit, commit et push.

## Exercie 9: Les branches communes
Dans la plupar des projets, nous utilisons plusieurs branches qui vons récupéré les modifications des autre branches.

Chaque projet a une branche principale. C'est par default "master" ou "main" et c'est la branche visible sur votre repository distant.

Si vous récupérez un git grace a la commande git clone, vous arriverez sur cette branche.

Elle sert en général de branche qui représente l'etat de production du projet, celui qui est utilisé par les clients ou d'autre développeur.

La deuxieme branche souvent utilisé est la branche `develop`. Sur cette branche l'on trouvera le code qui est encore en developpement. 

Une fois qu'il sera dans un etat assez avancé, il poura etre merge sur la branche master.

Normalement les developpeurs ne travaille pas sur cette branche mais sur des branches parraléles qu'ils merges dessus.

Ajoutez la branche "develop" a votre git.

Pour faire le push, vous devez utiliser la commande
```
git push -u origin develop
```

## Exercice 10: Les messages de commit
Chaque commit doit possédé un message.

Ces messages sont vraiment important pour la lisibilités des modifications.

Il existe plusieurs normes ecrire ces messages comme par exemple la norme angular.

Vous pouvez voir les informations des commit grace a l'utilisataire gitk. DAns un terminal:
```
gitk
```
Cet outil permet de voir les commits, leurs modifications, messages, date, auteur, ...

## Exercice 11: git stash
Il est defois important de mettre de coté nos changement avant de faire un commit. Pour cela il existe la commande git stash:

La commande `git stash` met de coté les modifications. Il marche comme un "couper". Elle peut donc etre utilisé pour suppirmer toutes vos modifications depuis le dernier commit.

La commande `git stash pop` permet de remettre les modifications couper par la commande `git stash`.

Cette commande fonctionne comme un systeme de pile.

## Commandes interdites sauf cas trés rare.
Lors ce qu'on ne maitrise pas git, nous avons souvent des problémes et il ce peut que nous essayons des commanes qui peuvent vraiment endomager le git.

Toutes les commandes avec les options `-hard` ou `-force` ne doivent pas etre utilisé sauf si vous savez exactement ce qu'elles font. Par exemple la commande `git push --hard` peut endomager le git distant.

AL commande `git fetch` permet de récupérer les modifications distante mais sans faire de merge avec les branches distantes. Elle peut occasionné une duplication des branches et peut rendre leurs gestions confuses.


