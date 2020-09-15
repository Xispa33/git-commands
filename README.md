Ce dépôt référence une liste de commandes git.

# SOMMAIRE
- [INITIALISATION DU PROJET](#INITIALISATION-DU-PROJET)
- [STAGING](#STAGING)
- [DIFFERENCES ENTRE FICHIERS](#DIFFERENCES-ENTRE-FICHIERS)
- [ANNULER DES MODIFICATIONS](#ANNULER-DES-MODIFICATIONS)
- [HISTORIQUE DES MODIFICATIONS](#HISTORIQUE-DES-MODIFICATIONS)
- [BRANCHES](#BRANCHES)
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

[Back to top](#STAGING)
---

# DIFFERENCES ENTRE FICHIERS

[Back to top](#DIFFERENCES-ENTRE-FICHIERS)
---

# RECUPERATION DES MODIFICATIONS
fetch
pull

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
$ git restore <fichier1>
```
- Annule les dernières modifications effectuées sur \<fichier1>. Le contenu de \<fichier1> redevient identique à celui du dernier commit.

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
# FUSIONS
merge
merge ff
merge noff

[Back to top](#FUSIONS)
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
- Fusionne la branche \<branche> sur la branche courante en non fast-forward. Le contenu de <branche> est rappatrié sur la branche courante. Des conflits sont potentiellement à régler.

```sh
$ git merge --squash <branche>
```
- Fusionne la branche \<branche> sur la branche courante. Tous les commits effectués sur \<branche> seront concaténer en 1.

[Back to top](#BRANCHES)
---

# AUTRES

[Back to top](#AUTRES)

---
# LICENSE

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
