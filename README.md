# PE-DevOps
Project work in Dev Ops

### Installing docker:
Use this link for [Installing docker on linux](https://runnable.com/docker/install-docker-on-linux)

### Installing jenkins: (Build Step)
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

### Setting up and running jenkins:
Follow the links below to setup jenkins
* Setup jenkins for continuous integration with Github, use this [link](https://www.youtube.com/watch?v=bGqS0f4Utn4&t=420s)
* Install *Github Integration plugin*, *Github plugin*, *Git plugin* in jenkins using manage jenkins.
* Setting up a webhook URL in github, for reference use this [link](https://medium.com/@marc_best/trigger-a-jenkins-build-from-a-github-push-b922468ef1ae)
* *{jenkins url}/safeRestart* to restart jenkins.
* *use backslash* at the end of you github webhook url(http://ci.jenkins/github-webhook/) otherwise post request may not work.

**This will trigger auto build when new commit is pushed on the github repository**

### Installing Selenium: (Testing Step)
