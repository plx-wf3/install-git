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



```





