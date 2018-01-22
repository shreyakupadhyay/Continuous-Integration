### Java Hello World 
##### Method 1:
1. Select *maven project* from the project types while creating new item. If this is not available for you then go to
Manage Jenkins -> Manage Plugins -> Available and search for "Unleash Maven Plugin". Once this is installed "maven project" will be shown in projects type list.

2. Provide description to the project otherwise leave it blank this is optional.

3. In Source Control Management select *Git* and give the *Repository URL* for your project where the java code is pushed which you want to build.

4. In Build Triggers select "Poll SCM". Poll SCM triggers build if there is a new commit in the code after last build. For this time need to be defined which will be used to check after what time new commit will be checked.  Put "H/5 * * * *" (without inverted commas) in Poll SCM. This will check for new commits in every five minutes. 

5.  In Build in Root POM give pom.xml file path in the repository URL. Generally this file should be in root of your java project. For reference have a look at this [repository](https://github.com/shreyakupadhyay/java-hello-world/).

6. pom.xml file 

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.shreyak</groupId>

    <artifactId>hello-world</artifactId>

    <version>1.0.0</version>

</project>
```
* *groupId* is shows the organization.
* *artifactId* shows the project.
* *version* shows the .jar file version.

7. Finally **save** the project. In case of testing right now without waiting for 5 minutes, select *Build Now*.

This process will build the java code and generate the .jar file of hello world program.

##### Method 2:
1. Select *Freestyle project* from the project types while creating new item.

2. Follow the *2 to 4* steps from *Method 1*.

3. In Build -> Add Build Step -> Execute shell. In command section after selecting *Execute shell* give the commands to run your java project. For reference have a look at this [repository](https://github.com/shreyakupadhyay/java-hello-world/).

```sh
$ javac src/main/java/HelloWorld.java
$ java src/main/java/HelloWorld
```
4. Finally **save** the project. In case of testing right now without waiting for 5 minutes, select *Build Now*.

This process will build the java code and returns the output of your code. Which can be seen in the *console output* of the project.

###### This is what needs to done for building java project. There are more than these two ways to build java project. 