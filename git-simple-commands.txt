> ## GIT commands : 
{.is-info}

**Ajouter tous les fichiers**
```
git add -A
```

**Ajouter un fichier**
```
git add nom_du_fichier
```

**Basculer sur un Commit**
```
git checkout numero_commit_dans_GitHub
```

**Basculer sur une Branche Existante**
```
git checkout nom_branch_existante
```

**Récupérer un fichier d’une autre branch**
```
git checkout origin/main path/to/your/folder
```

**ou si ce n’est pas depuis la main**
```
git checkout <other-branch-name> -- path/to/your/folder
```
  
**Clone**
```
git clone @source nouveau_dossier_local
```
  
**Corriger le dernier commit**
```
git commit --amend
```
  
**Différence avec le dépôt Git ETAPE 01**
```
git fetch
```
  
**Différence avec le dépôt Git ETAPE 02**
```
git diff --name-only nom_de_la_branche
```
  
**Etats des modifications 1**
```
git status
```
  
**Etats des modifications 2**
```
git whatchanged -n 1
```
  
**Faire un commit**
```
git commit -m "nom_de_la_branche - message pour préciser le commit"
```
  
**Liste des branches**
```
git branch list
```
  
**Nouvelle branche**
```
git branch nom_nouvelle_branche
```
  
**Supprimer une branche locale**
```
git branch -d [nom-de-ma-branche]
```
  
**Push force**
```
git push --force-with-lease
```
  
**Push initial**
```
git push --set-upstream origin nom_nouvelle_branche
```
  
**Push suivants**
```
git push
```
  
**Rebase 1 - Do**
```
git rebase master
```
  
**Rebase 2 - Cancel**
```
git rebase --abort
```
  
**Renommer une branche locale**
```
git branch -m old-name new-name
```
  
**Restaurer un fichier depuis la master**
```
git checkout origin/master nom_du_fichier
```
  
**Restaurer un fichier en local avant le PULL**
```
git checkout nom_du_fichier
```
  
**Résumé sur les branches**
```
git remote -v show -n origin
```


> Un Git pull permet de récupérer les fichiers de la branche en cours, tels qu’ils sont sur le dépôt Github.
{.is-info}

**Vérifier la branche de travail actuelle sur le serveur**
```
git branch
```


**Voir les fichiers qui ont été changés (= liste des modifications)**
```
git status
```


**Voir les différences avec la branche distante**
```
git diff --name-only origin/nom_de_la_branche
```



---


> toujours une Rebase jamais de Merge
{.is-info}

**Mettre à jour la main**
```
git branch main
git pull
```

**Se positionner sur la branche qui doit être rebasée avec la main**
```
git checkout NOM_DE_MA_BRANCHE
git pull
```

> Lancer la commande : `git rebase main`
{.is-success}


**Pour connaitre quels sont les fichiers concernés :**
```
git status
```

> Ceux concernés sont en rouge
{.is-info}



**Editer les fichiers en rouge avec Nano ou PhpStorm pour gérer les conflits, un par un
Les conflits sont indiqués dans chaque fichier**

- Une fois les fichiers modifiés, les ajouter un par un :

```
git add MON_FICHIER_01
git add MON_FICHIER_02
git add MON_FICHIER_03
```

- Finir le rebasage s’il existe encore des conflits, sinon ce n’est pas la peine
```
git rebase --continue
```

- Faire un push avec Force with lease
```
git push --force-with-lease
```


---


> afin de réduire le nombre de commit ( SQUASH )
{.is-info}
- **Se placer sur la branche en question :**
```
git checkout NOM_DE_MA_BRANCHE
git pull
```


- **Lancer la commande :**
```
git rebase -i HEAD~5
```


>  Le numéro renseigné après “HEAD~” indique le nombre de commit à afficher dans la liste , en général on ajoute un peu plus de commit à squasher pour s’assurer une bonne visibilité lors de l' opération
{.is-info}

 
- **Fusionner les commits en remplaçant pick par lettre s (s comme squash) et laisser le dernier commit sur lequel squasher en pick.**

***Avant :***
```
pick 735153ef SUP-258-voisin-erreur-500-formulaire-contact-extranet : Problème dans l'envoie email
pick 85b5481c SUP-258-voisin-erreur-500-formulaire-contact-extranet : Rectification suite à la revue
pick b654a155 SUP-258-voisin-erreur-500-formulaire-contact-extranet : Rectification inégalité stricte
```

***Après :***
```
pick 735153ef SUP-258-voisin-erreur-500-formulaire-contact-extranet : Problème dans l'envoie email
s 85b5481c SUP-258-voisin-erreur-500-formulaire-contact-extranet : Rectification suite à la revue

s b654a155 SUP-258-voisin-erreur-500-formulaire-contact-extranet : Rectification inégalité stricte
```

> !!! Ne Squasher que ses propres PR, pas celles des autres !!!
{.is-danger}


- **Valider les modifications**
```
CTRL + X
CTRL + O
```

- **Une nouvelle fenêtre s’ouvre pour modifier les commentaires**
Supprimer les lignes inutiles


- Remplacer le nom de l'auteur du commit par le sien
```
git commit --amend --reset-author
```

- **Faire un push avec Force with lease pour jouer le squash des commits**
```
git push --force-with-lease
```

- **Faire un git pull**
```
git pull
```
