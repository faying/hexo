---
title: R Shiny Server (Ubuntu 14.04) 配置
---

##用户配置

Username:r

Password:空格

##基础环境配置
###自動選擇最快的源
    sudo apt-get install unzip 
    sudo apt-get install python-setuptools
    wget -O getfastmirror-master.zip https://github.com/alvan/getfastmirror/archive/master.zip
    unzip ./getfastmirror-master.zip
    cd ./getfastmirror-master/
    sudo ./setup.py install
    sudo getfastmirror update -t
###安装ssh访问


    sudo apt-get install openssh-server
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install open-vm-tools
    
###安装中文语言配置

    sudo apt-get install language-pack-zh-hant
    sudo apt-get install language-pack-zh-hans

###关闭防火墙

    sudo apt-get autoremove iptables 

##安装Oracle JDK
检查是否已安装JDK

    java -version

返回

    vdm@vdm-test:~$ java -version
    The program 'java' can be found in the following packages:
     * default-jre
     * gcj-4.9-jre-headless
     * openjdk-7-jre-headless
     * gcj-4.8-jre-headless
     * openjdk-6-jre-headless
     * openjdk-8-jre-headless
    Try: sudo apt-get install <selected package>
    
添加JDK安装源

    sudo apt-get install python-software-properties 
    sudo add-apt-repository ppa:webupd8team/java 
    sudo apt-get update

安装Oracle JDK 8

     sudo apt-get install oracle-java7-installer
    
添加路径到`/etc/profile`
    
    sudo nano /etc/profile

```bash    
JAVA_HOME="/usr/lib/jvm/java-7-oracle"
JRE_HOME="$JAVA_HOME/jre"
export JAVA_HOME
export JRE_HOME
export PATH=$PATH:$JAVA_HOME:$JAVA_HOME/bin:$JRE_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib
export LD_LIBRARY_PATH=/usr/lib/jvm/java-7-oracle/jre/lib/amd64:/usr/lib/jvm/java-7-oracle/jre/lib/amd64/server


```

    source /etc/profile
    java -version
    
    
##安装R依賴

    
    sudo apt-get -y install build-essential gfortran libreadline6 libreadline6-dev xorg-dev cairo-dock cairo-dock-plug-ins git automake automake autotools-dev libbison-dev byacc zip gobjc
    sudo apt-get -y install tk-dev gcc gfortran texlive texlive-fonts-extra libreadline-dev libxml2-dev 
    sudo apt-get -y install libcurl4-gnutls-dev texinfo 
    sudo apt-get -y install libcurl4-openssl-dev libssl1.0.0 libcairo2-dev
    sudo apt-get -y install libicu-dev zlib1g zlib1g.dev libpcre3 libpcre3-dev liblzma-dev
    sudo apt-get -y install libssl-dev libssh2-1-dev gsl-bin libgsl0-dev libpango1.0-dev
    sudo apt-get install libbz2-dev
   
   
    sudo apt-get autoclean                
    sudo apt-get clean                    
    sudo apt-get autoremove             
    
##安裝R
    
    sudo apt-add-repository -y "deb http://cran.rstudio.com/bin/linux/ubuntu `lsb_release -cs`/"
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
    sudo apt-get update
    
    wget https://mran.revolutionanalytics.com/install/mro/3.2.3/MRO-3.2.3-Ubuntu-15.4.x86_64.deb
    wget https://mran.revolutionanalytics.com/install/mro/3.2.3/RevoMath-3.2.3.tar.gz
    sudo dpkg -i MRO-3.2.3-Ubuntu-15.4.x86_64.deb
    tar -xzf RevoMath-3.2.3.tar.gz
    cd RevoMath
    sudo ./RevoMath.sh

    
###安装RStudio Server
    https://dailies.rstudio.com/
    sudo apt-get install gdebi-core
    wget https://s3.amazonaws.com/rstudio-dailybuilds/rstudio-server-0.99.1116-amd64.deb
    sudo gdebi rstudio-server-0.99.1116-amd64.deb
    

###安装Shiny Server
```r
install.packages("shiny")
```
     wget https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/shiny-server-1.4.2.789-amd64.deb
      sudo gdebi shiny-server-1.4.2.789-amd64.deb

##安装R Packages
###rJava

    
    R CMD javareconf
    R
    
```r
install.packages('rJava',,'http://www.rforge.net/')
```

    
###Rserve 提供与Java连接的服务
```r
install.packages("Rserve")
```
###其他分析用R包
    
```r
install.packages("Hmisc")
install.packages("rmarkdown")
install.packages("RJSONIO")
install.packages("randomForest")
install.packages("corrplot")
install.packages("ROCR")
install.packages("foreach")
install.packages("doSNOW")
install.packages("DBI")
install.packages("xlsx")
install.packages("mlbench")
install.packages('devtools')
install.packages('topicmodels')
install.packages('wordcloud')
install.packages('ape')
install.packages('igraph')
install.packages('qdap')
install.packages('googleVis')
install.packages("Rwordseg", repos = "http://jliblog.com/cran/", type = "source")
install.packages("tmcn", repos = "http://jliblog.com/cran/", type = "source")
options(unzip = 'internal')
devtools::install_github("rstudio/shiny-incubator")
devtools::install_github('rstudio/shinyapps')
devtools::install_github('rstudio/shiny-incubator')
devtools::install_github("metagraf/rHighcharts")
devtools::install_github('ramnathv/rCharts')

install.packages('Rfacebook')
```

    
    

    
    



