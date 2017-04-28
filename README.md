# My Jenkins-slave

## Do in master node (jenkins-master link https://github.com/ray81415/jenkins-docker)
ssh-keygen -t rsa -b 4096  
eval "$(ssh-agent -s)"  
ssh-add ~/.ssh/id_rsa  

## Do in slave node
mkdir ~/bin  
cd bin  
wget http://<master_ip>:8080/jnlpJars/slave.jar  
copy [id_rsa.pub of master] to /.ssh/authorized_keys (id_rsa.pub is in ~/.ssh/ of jenkins-master)  

## Dockerfile
This Jenkins has  

- nodejs 6.X  
- yarn  
- net-tools  
- openssh-server  
- vim

It is from https://hub.docker.com/_/jenkins/

## docker-compose.yml
Yaml file composes jenkins-master and jenkins-slave to do test.

[your home path] of volumes of yaml file have to be change to your path which you want to store jenkins' data to

## common.yml
Separate setting of jenkins-master and jenkins-slave to common.yml to simplify docker-compose.yml

## jenkins-master setting on web
ssh root@<slave_ip> java -jar /root/bin/slave.jar