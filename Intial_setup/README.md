# Initial Setup
Initial setup of tools like jenkins, docker, selenium and deciding which method is better for the continuous integration.


### Installing jenkins: (Build Step)
##### Method 1:
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

### Setting up and running jenkins for continuous integration:
Follow the links below to setup jenkins
* Setup jenkins for continuous integration with Github, use this [link](https://www.youtube.com/watch?v=bGqS0f4Utn4&t=420s)
* Install *Github Integration plugin*, *Github plugin*, *Git plugin* in jenkins using manage jenkins.
* Setting up a webhook URL in github, for reference use this [link](https://medium.com/@marc_best/trigger-a-jenkins-build-from-a-github-push-b922468ef1ae)
* *{jenkins url}/safeRestart* to restart jenkins.
* *use backslash* at the end of you github webhook url(http://ci.jenkins/github-webhook/) otherwise post request may not work.

**This will trigger auto build when new commit is pushed on the github repository**


##### Method 2:
Using jenkinsci/blueocean docker image for jenkins installation. For this docker should be installed previously in the system. 
```sh
$ docker run \
  --rm \
  -u root \
  -p 8080:8080 \
  -v jenkins-data:/var/jenkins_home \ 
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v "$HOME":/home \ 
  jenkinsci/blueocean
```
 The above method is for linux users for Windows and Mac users follow this [link](https://jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/#run-jenkins-in-docker).

### Setting up and running jenkins for continuous integration:
Follow the links below to setup jenkins
* Create a Jenkinsfile in the root of the project. Save the code below in the Jenkinsfile.

```sh
pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
    }
}
```

Now add few changes in the local git repository and finally commit the changes. Go back to the jenkins interface the build step will be visible in the jenkins interface.

For more details follow this [link](https://jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/#run-jenkins-in-docker).

### Installing Selenium: (Testing Step)
##### Method 1:
Using jenkins plugin(jenkins IDE) for firefox to create the jenkins html suite file, for this follow this [link](https://www.oshyn.com/blogs/2011/november/how_to_create_a_test_suite_in_selenium_). But selenium IDE is not supported in 55+ firefox versions. 

##### Method 2:
Using ruby or python scripts for selenium. Taking an example of ruby script.
* Installing [selenium-webdriver](http://www.seleniumhq.org/docs/03_webdriver.jsp#chapter03-reference) by running the command below.
```sh
$ gem install selenium-webdriver
```
Using Ruby for Testing:
```rb
require "selenium-webdriver"
require "test/unit"
 
class LoginClass < Test::Unit::TestCase
 
  def setup  
    @driver = Selenium::WebDriver.for :firefox
    @driver.get('http://localhost:3000')
    @driver.manage.window.maximize  
  end
 
 
  def teardown
    @driver.quit
  end
 
 
  def test_login
    @driver.find_element(:name, "signin").click
    @driver.find_element(:name, "username").send_keys "username"
    @driver.find_element(:name, "password").send_keys "password"
    @driver.find_element(:name, "submit").click
    sleep 0.3
    assert(@driver.find_element(:id => "hello").text.include?("Hello"),"Assertion Failed")
    @driver.find_element(:name, "logout").click
  end
end
```
 This will open a web driver instance everytime ruby or python scripts are run. This method is good if no other services are running on the system these scripts are run otherwise run these scripts in virtual machine.

 ##### Method 3:
 Using .test.js or .test.rb files for various languages like javascript and ruby. Most of the frameworks like ruby on rails and React have these features in built to write test cases and run them everytime in the continuous integration pipeline. They generate results on the basis of written scripts and show them on the jenkins blueocean interface.

### Installing docker: (Deployment Step)
Use this link for [Installing docker on linux](https://runnable.com/docker/install-docker-on-linux)
