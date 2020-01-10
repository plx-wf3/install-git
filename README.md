# install-git
Set up the latest git version on different Linux distro  
Source code from  https://github.com/git/git/archive/v2.24.1.tar.gz

## Manual install on centos
log in as a normal user on your centos minimal  
```shell script
   cd
   git
   yum -y update
   yum -y install wget 
   wget   https://github.com/git/git/archive/v2.24.1.tar.gz
   tar -zxvf v2.24.1.tar.gz 
   cd git-2.24.1
   sudo yum -y install "@Development tools"
   sudo yum -y install gettext-devel curl-devel perl-CPAN perl-devel openssl-devel zlib-devel
   git  --version 
   make configure 
   ./configure --prefix=/usr/local
   nproc    # get the number of core 
   make -j<value of nproc>
   make test 
  git --version 
  sudo yum remove git 
  git --version 
  sudo make install 
  git --version 
  which git 
  vim ~/.bash_profile 
  move $PATH at the end of PATH line
  source ~/.bash_profile 
  git --version 

  

``` 
