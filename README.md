# install-git
Set up the latest git version on different Linux distro  
Source code from https://github.com/git/git/archive/v2.25.0.tar.gz

## Installation a partir des sources sous centos7
log in as a normal user on your centos minimal  
```shell script
  cd
  git
  sudo yum -y update
  sudo yum -y install wget 
  wget  https://github.com/git/git/archive/v2.25.0.tar.gz
  tar -zxvf v2.25.0.tar.gz 
  cd git-2.25.0
  sudo yum -y install "@Development tools"
  sudo yum -y install gettext-devel curl-devel perl-CPAN perl-devel openssl-devel zlib-devel
  git  --version 
  make configure 
  ./configure --prefix=/usr/local
  nproc    # display the number of core 
  make -j<value of nproc>
  make -j<value of nproc> test 
  git --version 
  sudo yum -y remove git 
  git --version 
  sudo make install 
  git --version 
# reinitialiser le shell
  source ~/.bash_profile 
  git --version 
``` 

## Installer docker en utilisant le repo ci-dessous 
```shell script
   git clone https://github.com/system-dev-formations/install-docker-centos7.git
   cd install-docker-centos7
```
installer ansible dans un virtualenv 
```shell script
    sudo yum -y install python3
    python3 -m venv venv
    source venv/bin/activate
    pip3 install ansible
````

## installer docker en utilisant le playbook 
```shell script
    ansible-playbook -i inventory playbook.yml
```

## Demarrer Bitbucket dans un container 
```shell script
docker volume create --name bitbucketVolume
docker run -v bitbucketVolume:/var/atlassian/application-data/bitbucket --name="bitbucket" -d -p 7990:7990 \
                   -p 7999:7999 atlassian/bitbucket-server
````
## Installer Gitlab dans un container 
```shell script
   git clone https://github.com/cesigit/docker-gitlab
   cd docker-gitlab
```

## Installer docker-compose
Si vous avez perdu votre connexion avec virtualenv faites  
```shell script
   source ~/install-docker-centos7/venv/bin/activate
```
autrement faites
```shell script
   pip3 install docker-compose
```
et lancer le container gitlab 
```shell script
   docker-compose up -d 
```
## installation simple d'un serveur git 
```shell script
mkdir -p /home/centos/git-repo/project-1.git
cd git-repo/
cd project-1.git/
git init --bare
# voir liste fichier avec plus recent vers le bas
ls -alrt
```
## utiisation de ce simple serveur git a partir de machine local
```shell script
  cd ~/git-roubaix
  mkdir simple-git 
  cd simple-git
  git init
  echo \#Test > README.md
  git add .
  git commit -m"First init"
  git remote add origin ssh://<votre_user>@<votre_ip_adresse/home/centos/git-repo/project-1.git
  git push -u origin master
  git status

## "suite"
# TOUJOURS EN "LOCAL"
# Connect to gitlabs
# Make project
# -> "public"
# -> "with README"
# Clone project (http)
# In empty folder/project folder
# -> git clone <url>
# Dans le fichier nouveau fichier créer
# git remote -v
# Donne l'url d'ou on est connecté
# 
# git config --global user.name "<username>"
# git config --global user.email "<usermail>"
# 
# Mettre des aliases
# git config --global alias.br branch
# git config --global alias.ci commit
# git config --global alias.st status
# git config --global alias.last 'log -1 HEAD'
# Check config file
# cat ~/.gitconfig
# 
# Editer fichier config
# Changer editeur par defaut
# git config --global -e
# git config --global core.editor <nomediteur>
# 
# Ajout alias:
# hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
# 
# Voir fonctionnement de git
# echo content > <filename(plus extension)>
# git st(atus)
# -> le fichier n'est pas suivi
# git add <filename>
# git st
# -> le fichier est "suivi"
# 
# 
# git commit -m "<description/commentaire>"
# git log
# 
# Permet de voir les fichier pret à être commiter
# commande "plomberie"
# git ls-files --stage
# 
# Affiche le dernier commit
# git log -1
# 
# stages new files and modifications, without deletions
# git add .
# git st
# 
# ?????
# git commit -am "<description/commentaire>"
# ?????
# .gitignore was needed for this...
# ?????
# see git stash (?)
# ?????
# 
# rtfm:
# git mv <file>
# git rm <file>
# git rm --cached <file>
# git log --oneline
# git log --oneline -4
# Voir alias (au dessus)
# git hist
# git diff
# git diff --cached
# git hist
# -> get "hashnumber"
# git diff <hashnumber>
# git diff <hashnumber>..HEAD
# git blame <file>
# Search ?
# git log -S <text>
# /!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\
# Irreversible, ne pas faire ! 
# git reset --hard HEAD
# Reversible
# git reset <hash_du_commit>
# /!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\ 
# 
# ?????
# git commit --amend
# git commit --amend --no-edit
# 
# Tag
# Aide a l'identification
# git checkout <valeur_du_hash>
# git tag <nom_du_tag> <valeur_du_hash>
# git tag v1.2
# git show <tag>
# 
# Push with tag(?)
# git push origin --tags
# (commande suivante est visible qu'en local, ne supprime pas le push du dessus, etc)
# supprime le tag
# git tag -d <nom_du_tag>
# (cmd suivante le fait en remote)
# git push origin :refs/tags/<nom_dutag> 
# 
# Savoir les branches systemes
# * = branche courante
# git branch
# git branch -v
# Test format nom de branch (voir restriction)
# git check-ref-format --branch 2.x/fix/ticket
# Création nouvelle branche
# git branch <nom_de_branche>
# ***** Changer de branche *****
# ***** Changer de branche *****
# git checkout <nom_de_branche>
# Faire nouvelle branche et se mettre dessus direct
# git checkout -b <nom_de_branche>
# 
# Pour fusionner des branches
# -> /!\ Se mettre sur branches master en premier
# git merge <nom_de_branche>
# 
# ?????
# git rebase
# 
# Voir liste repo distant
# git remote
# ---
# exercices: 29.01.2020
# echo content > file1.c
# echo content > file2.c
# git add .
# git st
# git commit -m "comment string"
# git log -1
# git log --oneline
# (commande suivante: ajoute à la fin du fichier, "append")
# echo more >> file1.c
# git commit -am "comment string(2)"
# git cat-file -t <hash_du_commit(?)>
# Affiche tree SHA1
# git cat-file -p <hash_du_commit(?)>
# git cat-file -p <tree_SHA1>
# Garbage Collector
# git gc
# git status -s
# 
# change some files check "diff" and/or
# "diff --staged" and/or
# "diff HEAD"
# do some "status" 
# do some "commit" with/o "-m" and/or "-am" 
# with/o comments/description
# then some "status"
# Enjoy !
# 
# difference entre fichier
# git diff <hash_fichier_n>..<hash_fichier_n+1>
# 
# git branch <nom_de_branche>
# git checkout <nom_de_branche>
# faire de nouveau fichier/modifier ceux creer precedement
# (commende suivante ajoute "tout")
# git add .
# git commit -m "commentaire"
# 
# *******************************************
# Exercice: suite
# git checkout master 
# echo "Initial content" > file-test.c
# cat file-test.c 
# git add .
# git commit -m "adding new file on master"
# git branch newbranch
# echo "Update on master" > file-test.c 
# git commit -am "update on master"
# git checkout newbranch
# echo "Update on newbranch" > file-test.c 
# git commit -am "update on newbranch"
# voir les logs (version control)
# git checkout master
# git merge newbranch
# (-> conflits)
# echo "merged version" > file-test.c
# git commit -am "Fixed conflicts"
# (Commande suivante pour supprimer branche)
# git branch -d newbranch
# git branch
# (my comment: Discount conflicts fix)
# *******************************************
# Exercice: suite.
# (sur la branches master)
# echo "another one" > file6.c
# git add .
# git commit -m "un autre fichier dans le repo"
# git rm file6.c
# git status
# ls (just checking)
# git reset --hard HEAD
# git status
# ls
# git rm file6.c
# git status -sb
# git commit -m "je l'ai detruit"
# git status
# ls
# echo "fichier 7" > file7.c
# git add file7.c
# git status
# ("sauvegarder" travail)
# git stash
# git status
# (liste de tout ce que l'on a sauvegarder)
# git stash list
# echo update >> file-test.c
# git commit -am "update file"
# (pour ...)
# git stash pop
# git status
# *******************************************
# Exercice: suite.
# Cesigit - calc2
# git clone <url> <name_of_folder_to clone_line>
# cd calc2/
# git branch
# (voir remote branches)
# git branch -r
# (voir "message")
# git branch -av
# (voir ajouter upstream pour "tracker changement")
# git remote add upstream <url_du_clone>
# git remote -v
# git branch -av
# -----
# cd calc_other
# git branch
# git branch -av
# (voir .html -> "ouvrir" dans browser)
# (suivre branche distante (?))
# git branch features origin/features
# git branch
# (voir "features" et clé)
# git branch -av
# ( "-b" crée la branche durant le checkout)
# git checkout -b cpick
# git log --oneline features
# (commande suivante: branch**)
# git cherry-pick <hash_of_add_max_function>
# git log cpick --online
# git rebase <hash_of_add_exp_function>
# git rebase <hash_of_add_min_function>
# git log --oneline
# (cherry-pick && rebase == meme difference)
# (cherry-pick == "old")
# git checkout master
# git merge cpick
# git push
# - - - - -
# (back in calc2)
# git branch -av
# git branch ui origin/ui
# git branch -av
# git merge ui
# git push origin master
# (-> conflit because modif above)
# git pull origin master
# (-> conflit because modif above)
# (annulation/suppression de merge)
# git merge --abort
# (mettre a jour repo distant sans mettre a jour branches locales)
# git fetch
# git branch
# git hist (see alias)
# git rebase origin/master
# (-> toujours un conflit)
# (annulation/suppression de rebase)
# git rebase--abort
# ( ????? )
# git rebase -Xours origin/master
# git log --oneline
# 
# *******************************************
# Exercice: suite.
# Cesigit - super_calc
# cd super_calc/
# git branch
# git branch -av
# git worktree add -b features ../super_calc_features origin/features
# cd ../super_calc_features/
# vim calc.html (modif title)
# git commit -am "Update title" ( -am == add && message)
# cd ../super_calc
# git branch
# git log --oneline features
# git worktree list
# rm -Rf ../super_calc_features/
# git worktree prune
# 

```





