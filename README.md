# java/spring app
Instruction to run java spring apps on Stackato


## Installing Oracle JDK on linux system

Downloading the jdk
```bash
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u91-b14/jdk-8u91-linux-x64.tar.gz"
```

Installing the jdk
```bash
tar xzvf jdk-8u91-linux-x64.tar.gz
sudo mv jdk-8u91-linux-x64 /usr/local/
sudo ln -s /usr/local/jdk-8u91-linux-x64 /usr/local/jdk
```

Add path of jdk binaries and JAVA_HOME in  ~/.bashrc

```bash
# edit your .bashrc file with vi ~/.bashrc
export PATH=/usr/local/jdk/bin:$PATH
export JAVA_HOME=/usr/local/jdk
```

## Installing Maven
  
Downloading maven
```bash
wget http://mirror.klaus-uwe.me/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
```


Installing maven
```bash
tar xzvf apache-maven-3.3.9-bin.tar.gz
sudo mv apache-maven-3.3.9-bin /usr/local/
sudo ln -s /usr/local/apache-maven-3.3.9-bin /usr/local/maven
```

Add maven bin direcotry to path
```bash
# edit your .bashrc file with vi ~/.bashrc
export PATH=$PATH:/usr/local/maven/bin
```

source ~/.bashrc for jdk & maven environment
```bash
source ~/.bashrc
```

## Copy/clone source code (java app with maven pom.xml) - example from github.com/Stackato-Apps
```bash
git clone https://github.com/Stackato-Apps/hello-java.git
```

## Build application
```bash
cd hello-java
mvn clean package
```
   Note: If the target application exists aleady, you can use this binary to push it to stackato.

## Push to stackato cluster

   Note: stackato client has to be installed (see: https://docs.stackato.com/user/client/)
```bash
stackato target https://api.stackato-env-ip
stackato login <stackato-user>
   
stackato push -n [--health-timeout 500s]
```
   Note: use --health-timeout 500s in case of timeout during the deployment

## If no manifest.yml exist for your own application, you can use the hello-java example file:

```yaml 
---
applications: 
- name: <app-name>
  memory: 512M
  path: target/<app-target-name> 
```

Note: the app "app-target-name" is defined in the pom.xml file.






  
