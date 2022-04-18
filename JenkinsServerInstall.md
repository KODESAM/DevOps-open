## Install Jenkins on Ubuntu 20.04 ##

latest Update 

```
sudo apt-get update
```

Install java 8
```
sudo apt-get install openjdk-8-jdk
```
Download jenkins repo
```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```

Add Jenkins Repo

```
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```
Update 
```
sudo apt-get update
```
Install jenkins
```
sudo apt-get install jenkins
```
Check jenkins service status
```
service jenkins status
```
Enable jenkins service
```
service jenkins enable
```
Browse Jenkins via IP and Port
```
https://IP:8080
```
