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
# 
# 
# 

```





