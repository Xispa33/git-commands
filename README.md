Ce dépôt référence une liste de commandes git.

# SOMMAIRE
- [INITIALISATION DU PROJET](#INITIALISATION-DU-PROJET)
- [STAGING](#STAGING)
- [RECUPERATION DES MODIFICATIONS](#RECUPERATION-DES-MODIFICATIONS)
- [ANNULER DES MODIFICATIONS](#ANNULER-DES-MODIFICATIONS)
- [HISTORIQUE DES MODIFICATIONS](#HISTORIQUE-DES-MODIFICATIONS)
- [BRANCHES](#BRANCHES)
- [ETIQUETTAGE](#ETIQUETTAGE)
- [AUTRES](#AUTRES)
- [LICENSE](#LICENSE)  

---
# INITIALISATION DU PROJET

```sh
$ git init
```
- Création du dossier .git/ dans le répertoire courant

```sh
$ git config --list
```
- Renvoie la liste de tous les paramètres git (locals et globals). 

```sh
$ git config --list --local
```
- Renvoie la liste de tous les paramètres git locals.

```sh
$ git config --list --global
```
- Renvoie la liste de tous les paramètres git globals.

```sh
$ git config --local user.name "name"
```
- Configure le nom de l'utilisateur du dépôt local

```sh
$ git config --global user.email "email"
```
- Configure l'email de tous les dépôts git de la session

```sh
$ git config --global color.ui true
```
- Avoir la coloration syntaxique

```sh
$ git config --global branch.autosetuprebase always
```
- Faire un rebase lors d'un pull. Il se peut que la valeur par défaut soit merge, ce qui n'est pas pratique car à chaque pull, on a un commit de merge en plus.


Dans un fichier *.gitignore*, mettre tous les fichiers à ne pas stager.

[Back to top](#INITIALISATION-DU-PROJET)
---

# STAGING
```sh
$ git add <fichier1> <fichier2> ...
```
- Stager \<fichier1> et \<fichier2>

```sh
$ git status
```
- Obtenir la liste des fichiers modifiés depuis le dernier commit

```sh
$ git commit -m "Message de commit"
```
- Commiter la liste des fichiers modifiés

```sh
$ git commit -am "Message de commit"
```
- Commiter la liste des fichiers modifiés et stagés (le *-a* permet de faire le `git add` sur chaque fichier stagé)

```sh
$ git add <file>
$ git commit --amend --no-edit
```
- Ajouter le fichier \<file> au dernier commit effectué et sans modifier le message de dernier commit. Pour modifier le message, enlever le paramètre --no-edit

[Back to top](#STAGING)
---

# RECUPERATION DES MODIFICATIONS
```sh
$ git pull --rebase <remote_name> <branche>
```
- Récupère les changements sur le dépôt distant \<remote_name> et les met dans la branche \<branche>

```sh
$ git fetch <remote_name> <branche>
```
- Permet de récupérer les modifications sur le remote \<remote_name> de \<branche> **SANS** les merger sur la branche \<branche> (à la différence du pull).


[Back to top](#RECUPERATION-DES-MODIFICATIONS)
---

# ANNULER DES MODIFICATIONS

## Reset
Avec le reset, on réécrit l'historique, on peut donc supprimer des commits.  Pour ne pas perdre l'historique, il faut faire des **revert**.
```
$ git reset HEAD <fichier1>
```
- Annuler le staging de \<fichier1>, mais ne supprime pas les dernières modifications.

```
$ git reset
```
- Annuler le staging de tous les fichiers, mais ne supprime pas les dernières modifications. On peut également préciser un numéro de commit.

```
$ git reset --hard
```
- Annule le staging et les modifications de tous les fichiers depuis le dernier commit.

```
$ git reset --hard <sha commit>
```
- Annule le staging et les modifications de tous les fichiers depuis le  commit de sha \<sha commit>.

```
$ git reset --hard HEAD~n
```
- Annule le staging et les modifications de tous les fichiers des n derniers commits.

```
$ git reset --hard HEAD^^^^^^
```
- Annuler le staging et les modifications de tous les fichiers des 6 derniers commits.

```
$ git reset --soft <sha commit>
```
- Revient au commit de sha <sha commit> et laisse les modifications en staging \<sha commit>. Permet de revenir en arrière juste avant le commit des modifications.

```
$ git reset --mixed <sha commit>
```
- Revient au commit de sha <sha commit> mais ne stage pas les modifications \<sha commit>. Permet de revenir en arrière juste avant le commit des modifications.

## Revert

## Autres
```sh
$ git checkout -- .
```
- Annule les dernières modifications effectuées sur tous les fichiers **non stagés**. Les fichiers untracked ne sont pas modifiés. Le contenu de ces fichiers redevient identique à celui du dernier commit.

```sh
$ git restore --staged <fichier1>
```
- Annule les dernières modifications effectuées et stagées sur \<fichier1>. Le contenu de \<fichier1> redevient identique à celui du dernier commit.

```sh
$ git checkout <fichier1>
```
- Annule les dernières modifications effectuées sur \<fichier1>. Le contenu de \<fichier1> redevient identique à celui du dernier commit.

```sh
$ git checkout <sha commit> <fichier1>
```
- Annule les dernières modifications effectuées sur \<fichier1>. Le contenu de \<fichier1> redevient identique à celui du commit de sha \<sha commit>.


[Back to top](#ANNULER-DES-MODIFICATIONS)
---

# HISTORIQUE DES MODIFICATIONS
```sh
$ git log
```
- Afficher la liste des derniers commits

```sh
$ git log -n x
```
- Afficher les x derniers commits

```sh
$ git log --one-line
```
- Afficher la liste des derniers commits sur une seule ligne

```sh
$ git log -p <fichier>
```
- Afficher l'historique des modifications de \<fichier> à chaque commit

```sh
$ git log -n x -p <fichier>
```
- Afficher l'historique des modifications de \<fichier> des x derniers commits

```sh
$ git show --pretty="" --name-only <sha>
```
- Affiche les fichiers commités du commit de sha \<sha>


```sh
$ git diff
```
- Affiche toutes les modifications depuis le dernier commit. 

```sh
$ git diff <fichier>
```
- Affiche les modifications sur \<fichier> depuis le dernier commit. 

```sh
$ git checkout <sha commit>
```
- Affiche le contenu de tous les fichiers au commit de clé sha \<sha commit>. Cette commande est utile lorsque on veut juste visualiser le contenu d'un fichier à un commit donné. Tous les commits effectués en HEAD détachée seront perdus lorsqu'on change de branche. (chercher les commandes pour les rappatrier). Il ne faut donc surtout pas modifier le fichier après cette commande !! Après cette commande, entrer la commande suivante pour retourner sur une branche:
```sh
$ git checkout <branche> 
```

```sh
$ git commit --amend -m "Message de commit"
```
- Revient sur le commit précédent et modifie le message du dernier commit. Si des fichiers ont été stagés après le dernier commit, ces fichiers vont se retrouver dans le dernier commit. Si on ne veut pas modifier le message de commit, on peut enlever le -m et le "".

```sh
$ git rebase <nom_branche>
```
- Rappatrie les commits de la branche \<nom_branche> sur la branche courante. Cette commande est notamment utile lorsque des commits \<nom_branche> sont antérieurs aux derniers commits de la branche courante. Cela permet également de faire un merge entre 2 branches si la branche parent a évolué.

```sh
$ git rebase -i <nom_branche>
```
- Rappatrie les commits de la branche \<nom_branche> sur la branche courante en mode intéractif. L'intérêt du mode intéractif est qu'il permet de squasher (=rassembler) les commits avant le rebase.
Un éditeur Vi s'ouvre et on choisit les commits à squasher à l'aide de la lettre s.  
**ATTENTION**: Pour squasher le **commit de la ligne M avec le commit de la ligne M+1**, il faut mettre un "s" à la place du "pick" de la ligne **M+1**.   
Si un conflit apparait, il faut:  
1 - Résoudre le conflit  
2 - Stager et commiter
3 - Lancer la commande: `$ git rebase --continue`.  
Vi apparait ensuite. Il faut rentrer les messages de commit à écrire pour les commits squashés.
 
```sh
$ git rebase -i HEAD~n
```
- Cette commande de passer en mode rebase intéractif. On peut par exemple squasher plusieurs commits en 1 grâce à celle-ci ou inverser l'ordre des commits. Le "~n" permet d'afficher les n derniers commit dans l'éditeur Vi.

**ATTENTION**: Squasher un historique de commits poussé en conf est dangereux. 

```sh
$ git cherry-pick <sha commit>
``` 
- Récupérer le commit de sha \<sha commit>. Le commit ajouté se retrouve alors en position HEAD de la branche courante.

```sh
$ git cherry-pick -n <sha commit>
``` 
- Récupérer le commit de sha \<sha commit>,**sans le commiter**. La position HEAD de la branche courante n'a pas changé. Seuls les fichiers stagés dans le commit de sha \<sha commit> ont été modifiés.

[Back to top](#HISTORIQUE-DES-MODIFICATIONS)
---

# BRANCHES
```sh
$ git branch <nom_branche>
```
- Créé une branche nommée \<nom_branche>.

```sh
$ git checkout <nom_branche>
```
- Se placer sur la branche nommée \<nom_branche>.

```sh
$ git checkout -b <nom_branche>
```
-Créer et se placer sur la nouvelle branche nommée \<nom_branche>.

```sh
$ git checkout -D <nom_branche>
```
- Supprime la branche nommée \<nom_branche>

```sh
$ git merge <branche>
```
- Fusionne la branche \<branche> sur la branche courante en fast-forward (déplacement de la tête de la branche courante la tête de \<branche>).  
Exemple 1: Si <branche> est issue de master et que seule <branche> a évolué, fusion en fast forward.  
Exemple 2: Si <branche> est issue de master, que <branche> **ET** master ont évolué mais des fichiers différents ont été modifiés, fusion en récursif (auto-merging). 

```sh
$ git merge --no-ff <branche>
```
- Fusionne la branche \<branche> sur la branche courante en non fast-forward. Le contenu de <branche> est rappatrié sur la branche courante. Des conflits sont potentiellement à régler. 1 commit de plus est à faire (ce n'est pas le cas en fast forward).

```sh
$ git merge --squash <branche>
```
- Fusionne la branche \<branche> sur la branche courante. Tous les commits effectués sur \<branche> seront concaténer en 1.

```sh
$ git branch -m <old_branch> <new_branch>
```
- Renommer une branche nommée \<old_branch> en \<new_branch>

[Back to top](#BRANCHES)
---

# STOCKAGE DES MODIFICATIONS
```sh
$ git stash
```
- Sauvegarde les modifications non stagées en mémoire

```sh
$ git stash list
```
- Voir la liste des élements stashés

```sh
$ git stash apply
```
- Applique l'ensemble des modifications sauvegardées du dernier stash

```sh
$ git stash drop
```
- Supprime le dernier élement stockés de la stash list

```sh
$ git stash save <stash message>
```
- Sauvegarde les modifications non stagées et choisir le message

```sh
$ git stash show stash@{n}
```
- Permet de visualiser les modifications non stagées du stash n

```sh
$ git stash show stash@{n} -p
```
- Permet de visualiser les modifications non stagées du stash n plus détaillé

```sh
$ git stash pop stash@{n}
```
- Apply et drop l'élément n de la stash list


[Back to top](#STOCKAGE-DES-MODIFICATIONS)
---

# ETIQUETTAGE
```sh
$ git tag
```
- Affiche la liste des tags

```sh
$ git tag -l 'v1.xx.xx'
```
- Affiche la liste des tags contenant 'v1.xx.xx'

```sh
$ git tag -a vX.Y -m "Message"
```
- Ajouter un tag à la version courante en spécifiant le message d'étiquettage

```sh
$ git show vX.Y
```
- Visualiser les données de l'étiquette vX.Y

```sh
$ git tag -a vX.Y <sha commit>
```
- Ajouter un tag au commit de sha \<sha commit>

```sh
$ git tag -d <tag_name>
```
- Supprimer le tag \<tag_name> **en local**

```sh
$ git push --delete <remote> <tag_name>
```
- Supprimer le tag \<tag_name> **en global** sur le remote \<remote>

```sh
$ git tag -f -a <tagname>
$ git push -f --tags
```
- Update tag <tagname>
 
[Back to top](#ETIQUETTAGE)
---
# AUTRES
```sh
$ git clone <remote_path> <folder_name>
```
- Clone le dépôt au chemin \<remote_path> dans le dossier \<folder_name>

```sh
$ git remote add <remote_nom> <remote_path>
```
- Ajouter un remote

```sh
$ git remote -v
```
- Afficher la liste des remotes

```sh
$ git remote rename <old_remote_nom> <new_remote_nom>
```
- Renommer le remote \<old_remote_nom> en \<new_remote_nom>

```sh
$ git remote remove <remote_nom>
```
- Supprime le remote \<remote_nom>

```sh
$ git submodule add <lien vers remote>
```
- Créer un submodule

```sh
$ git clone ... 
```
- Cloner un répository contenant des submodules et se placer sur la branche \<branche> du dépôt parent

```sh
$ git push <remote_name> <branche> 
```
- Pousser les modifications sur le remote \<remote_name> et la branche \<branche> 

```sh
$ git clean -f -d
```
- Supprime tous les fichiers non suivis. Les fichiers suivis dans le .gitignore ne seront pas supprimés

```sh
$ git clean -f -d -x
```
- Supprime tous les fichiers non suivis. Les fichiers suivis dans le .gitignore le seront également

```sh
$ git clean -d -n
```
- Permet de visualiser quels fichiers seraient supprimés si la commande `clean` était lancée.

```sh
$ git clean -i
```
- Clean en mode intéractif

```sh
$ git rm -f <file>
```
- Permet de supprimer le fichier \<file> précédemment tracké..

```sh
$ git blame <fichier>
```
- Permet de lister les dernières modifications de chaque ligne du fichier \<fichier>

```sh
$ git blame -L l1,l2 <fichier>
```
- Permet de lister les dernières modifications de chaque ligne du fichier \<fichier> entre les lignes l1 et l2

```sh
$ git log -S "pattern" --pretty=format':%h %an %ad %s'
```
- Permet de lister les modifications et trouver les modifications contenant "pattern". Faire un `git diff ` sur le fichier concerné après pour voir les évolutions en question.

```sh
$ git revert <sha commit>
```
- Permet de supprimer un commit. Cette commande créé un commit

```sh
$ git revert <oldest commit sha>..<newest commit sha>
```
- Permet de supprimer un range de commit. Cette commande créé un commit

[Back to top](#AUTRES)

---
# LICENSE

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
