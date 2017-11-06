# PE-DevOps
Project work in Dev Ops

### Installing docker:
Use this link for [Installing docker on linux](https://runnable.com/docker/install-docker-on-linux)

### Installing jenkins:
```sh
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
$ sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
$ sudo apt-get update && sudo apt-get install jenkins
$ sudo systemctl start jenkins && sudo systemctl status jenkins
```
Just check this shows **active**. Further follow this [link](https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-16-04) in case of any issue while running above commands. Now, download the jenkins.war file to run it on local server from this [link](https://updates.jenkins-ci.org/download/war/)

```sh
$ java -jar jenkins.war
```
If above command is throwing error of java version, upgrade java version to 1.8 from this [link](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)

**This will start jenkins tool on local server.**
