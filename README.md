# Exercice Git

## Présentation
Le but de ces exercices est d'utiliser git et voir comment travailler avec en équipe.
___
## Exercice 1: git clone
Le but de cet exercice est de récupérer du code depuis github.
Pour cela vous devez récupérer ce projet.

Cliquez sur le bouton "code" et copiez l'URL.
Dans un terminal, choisissez un dossier qui contiendra votre projet.

Ouvrez un terminal (shell, cmd ou powershell) et tapez la commande:
```git
git clone <url que vous avez copié>
```


Git téléchargera le projet.
___
## Exercice 2: réinitialiser un répértoir git.
Vous avez maintenant le projet sur votre système. Mais ce projet est relié avec mon github. Vous devez donc réinitialiser votre git local.

Dans le terminal:

Linux : 
```
cd <nom du projet>
rm -r .git
```

Windows : 
```
cd <nom du projet>
rmdir /s .git
```

Le but de ces commandes est de supprimer le dossier`.git`. 

Ce dossier est un `dossier caché`, il faut donc activer les dossiers cachés pour le voir dans votre exporateur de fichier. 

Il contient toutes les informations de notre projet et permet d'éxecuter les commandes git. Le supprimer permet de supprimer git de notre dossier. Il faut maintenant réinitialiser votre git local: 

Dans le terminal, lancez la commande:
```
git init
```

Cette commande permet de créer le dossier`.git` et donc permet l'utilisation de git. En le recréant, nous avons réinitialisé le git.

Nous pouvons maintenant enregistrer tous les changements sur votre propre git.

Git propose un système de `remonte` qui permet de lui dire quel est le compte qui doit recevoir nos modifications.

Créez un nouveau repository sur votre compte github ou gitlab. Il ne faut cocher aucune case.

Vous avez maintenant un exemple de commande pour ajouter votre code à ce repository. Copiez la commande qui ressemble à :
```
git remote add origin <url de votre repo>
```
et executez la dans le dossier.

`origin` est notre `remote`. Elle fait reference au `repository` sur votre compte github ou gitlab.

Cette commande dit:
```text
git(git) Envoie(push) mes données au repository avec le remote (origin), appel la branche créer comme master (master) et souvient toi de cette commande (-u).
```

Si vous mettez a jour votre repository sur le site de github u gitlab, vous pourrez voir que l'ensemble du code est maintenant disponible en ligne.

## Exercice 3: Les commits

Git permet de gérer des version de votre code. 

Pour cela il utilise un système de `commit`. Ces derniers permettant de sauvegarder les modifications depuis le dernier commit.

Au début d'un projet, notre projet est vide. Après avoir créé les premiers fichiers et dossier, vous pouvez sauvegarder l'ensemble des modifications dans un `commit`. 

Si vous faites une ou plusieurs modification, vous pouvez créer une nouvelle sauvegarde non pas du code en entier, mais uniquement des modifications, ajout ou suppression de nos fichiers dans un `commit`.

Nous pouvons voir un commit comme un post-it où nous notons les modifications sur certain fichier depuis le dernier post-it.

Pour ajouter un fichier à notre post-it(commit) nous utilisons la commande :

```
git add README.md
```
Vous avez ajouté les modifications (ici la création du fichier) a votre future post-it.

Mais si nous devions ajouter tous les fichiers ont la main l'ajout de chaque fichier, cela prendrait trop de temps. 

La commande suivante permet d'ajouter TOUS les fichiers, dossiers non vides et tous les fichiers dans tous les dossiers qui se trouve dans le dossier courant.
```
git add *
```
ou 
```
git add .
```
Ces deux commandes sont équivalentes.

Après avoir noté l'ensemble des fichiers, nous allons specifier que nous avons fini d'écrire nos changements. Git créera un commit contenant tous les modifications depuis le dernier commit.

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
Si cette commande ne marche pas, vous n'avez pas utilisé la première fois le -u dans votre commande.
Vous pouvez réexécuter la commande:
```
git push -u origin master
```

## Exercice 5: Les commits a plusieurs.

Pour cet exercice, vous devez faire équipe avec une autre personne.

Par défaut, vos etes le seul a pouvoir envoyer des modifications sur votre repository distant (qui se trouve sur github ou gitlab). 

Il faut donc ajouter un autre utilisateur comme membre pour qu'il puisse effectuer des modifications. Par la suite nous parlerons de Utilisateur 1 (qui possède le compte git) Utilisateur 2 (celui qui est membre)

L'utilisateur 2 doit récupérer votre git sur sa machine, pour cela il doit exécuter la commande:

```
git clone <URL du repository de l'utilisateur 1>

``` 
### Utilisateur 1

L'utilisateur 1 peut faire une modification dans le fichier `1 py` en modifiant ``numero_de_utilisateur`` avec la valeur 1.

Vous avez apporté une modification à un fichier de ce projet. 

Vous pouvez avoir des informations sur quels sont les fichiers ayant eu des modifications et qui ne sont pas encore dans un commit avec la commande:
```
git status
```
Enregistrez votre modification :
```
git add *
git commit -m "je suis l'utilisateur 1"
```

et envoyez les modifications sur le repository distant avec la commande :
```
git push
```

## Utilisateur 2

Le deuxième utilisateur peut faire de même en mettant le numéro 2 au fichier 2.

Quand l'utilisateur 2 voudra envoyer ses données, un message d'erreur s'affiche. 

Normal, il n'a pas récupéré l'ensemble des modifications sur le repositry distant. 

Il doit pouvoir les récupérer avant d'envoyer les données au serveur.Pour récupérer les modifications:
```
git pull
```

Cette commande permet de récupérer les modifications que vous n'avez pas encore. Après cela vous pouvez rententer de faire un git push.

Git fonctionne avec un système de commit chainés. Chaque commit sauvegarde les modifications, un message mais aussi quel est le commit précédent. Grace à cela git est capable de récupérer l'ensemble des modifications depuis le début du projet.

Quand vous n'avez pas les mêmes commits que ceux sur le serveur, votre commit aura le même parent que celui sur le repository distant, il y a donc un problème. 

En Récupérant le ou les commit qui vous manquent, vous positionnez votre commit après celui qui était dans le repository distant. 

Au passage vous avez gagné les modifications du repository distant.

## Exercice 6: Les Conflis

Normalement si nous nous débrouillons bien, le cas précédent est le plus courant. 

Mais dans certains cas nous pouvons avoir un conflit. 
Si les deux utilisateurs modifient le même fichier a la même ligne alors il y aura un conflit entre les deux commit.

Par exemple, les deux utilisateurs modifient la ligne 6 du fichier 1, font un commit et le push sur le serveur distant, le dernier aura un message d'erreur lors du push comme vu précédemment. 

Mais cette fois après un git pull, il aura aussi un message. Le fichier 1 possède un conflit, git nous laisse alors choisir comment gérer le problème en mettant en évidence le problème du conflit.

Après avoir choisi la modification à garder grace à votre éditeur de texte où IDE favorie, il doit faire un commit puis refaire un push. Dans cet exemple la modification est petite, mais si un projet est mal découpé entre les développeurs et qu'ils modifient les mêmes lignes, il peut y avoir de gros conflit qui peuvent prendre du temps à résoudre.
___
## Exercice 7: Les branches.

Pour réduire ces problèmes, il existe le système de branche.

Il est possible de séparer la sauvegarde des modifications (`commit`) dans une autre branche indépendante. 

Seules les personnes sur les mêmes branches peuvent avoir des problèmes de conflit.

Chaque utilisateur créé sa branche avec la commande :

```
git checkout -b <utilisateur1 ou utilisateur2>
```
Vous avez créé une nouvelle branche qui porte votre nom d'utilisateur. 

Les deux utilisateurs peuvent une nouvelle fois modifier la ligne 6 du fichier 1, faire un commit et pousser les modifications sur le serveur avec la commande:
```
git push -u origin <nom de votre branche>
```

Vous ne devriez pas avoir de problème du conflit.

Après un git pull, vous récupérerez votre branche et celle de l'autre utilisateur. Pour le voir, vous pouvez utiliser la commande

```
git branch -a
```

## Exercice 8: Les merges

Travailler sur sa branche limite les conflits mais ne permet pas de travailler en équipe.

Nous pouvons effectuer nos modifications sur une branche puis rapatrier toutes les modifications sur la branche master pour rassembler les modifications.

Pour cela nous devons retourner sur la branche master:
```
git checkout master
```

La commande git check out permet de changer de branche. L'option -b permet de créer une branche si elle n'existe pas encore en local.

Une fois sur la branche master (pour le vérifier vous pouvez utiliser la commande git branch, la branche actuelle est notifié par une étoile) vous pouvez demander de récupérer l'ensemble des modifications sur votre branche et des ajoutés à la branche principale. 

Pour cela:
```
git merge <nom de votre branche>
```

Pour envoyer cette fusion au serveur distant vous pouvez utiliser la commande git push.

Le dernier à faire cette manipulation aura un problème du conflit.

Le faite de rester sur notre branche nous permet de ne pas gérer les conflits à chaque push/pull. 

Mais lors du merge, il peut toujours y avoir des conflits. Il peut alors gérer le conflit, commit et push.

## Exercie 9: Les branches communes

Dans la plupart des projets, nous utilisons plusieurs branches qui vont récupérer les modifications des autres branches. Chaque projet a une branche principale. 

C'est par défaut `master` ou `main` et c'est la branche visible sur votre `repository distant`.

Si vous récupérez un git grace à la commande `git clone`, vous arriverez sur cette branche.

Elle sert en général de branche qui représente l'état de production du projet, celui qui est utilisé par les clients ou d'autre développeurs.

La deuxième branche souvent utilisée est la branche `develop`. C'est sur cette branche que l'on trouvera le code qui est encore en développement. 

Une fois qu'il sera dans un état assez avancé, il pourra être remi sur la branche master.

Normalement les développeurs ne travaillent pas sur cette branche mais sur des branches paralèlles qu'ils `merge` dessus.

Ajoutez la branche `develop` à votre git.

Pour faire le push, vous devez utiliser la commande 
```
git push -un origine develop
```
## Exercice 10: Les messages de commit

Chaque commit doit posséder un message. Ces messages sont vraiment importants pour la lisibilité des modifications.

Il existe plusieurs normes pour écrire ces messages comme par exemple la norme `angular`.

Vous pouvez voir les informations des commit grace à l'utilisatrice gite. 

Dans un terminal:
```
gitk 
```

Cet outil permet de voir les commits, leur modification, messages, date, auteur, ...

## Exercice 11: git stash

Il est parfois important de mettre de côté nos changement avant de faire un commit. 
Pour cela il existe la commande `git stash`. Elle met de coté les modifications. Elle marche comme un "coupé". 

Elle peut donc etre utilisé pour supprimer toutes vos modifications depuis le dernier commis.

La commande `git stash pop` permet de remettre les modifications couper par la commande `git stash`.

Cette commande fonctionne comme un système de `pile`.

## Commandes interdites sauf cas très rare.

Lorsqu'on ne maitrise pas git, nous avons souvent des problèmes et il se peut que nous essayons des commandes qui peuvent vraiment endommager le git.

Toutes les commandes avec les options `-hard` ou `-force` ne doivent pas être utilisées sauf si vous savez exactement ce qu'elles font. 

Par exemple la commande `git push --force` peut endommager le git distant. La commande `git fetch` permet de récupérer les modifications distantes mais sans faire de merge avec les branches distantes. 

Elle peut occasionner une duplication des branches et peut rendre leurs gestions confuses.

