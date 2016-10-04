PROG2 Lab - Build Tools - Maven
===============================

## Introduction
This lab is designed to help you become familiar with the Maven build automation tool to manage your projects.

## Objectives
In this excercise you will:
- Setup set up your Maven environment
- Learn to master Maven configuration, lifecycle and goals

## Requirements

**Hardware:** none

**Software:**
- An up to date web browser
- Your preferred text editor
- Basic Maven installation for your platform (see installation section)
- optional: Eclipse or IntelliJ IDEA to test the Maven IDE integration.


## Expected results
Complete the tasks given below. Look up the required commands in the available documentation (see [References](#References)). To complete the assignment show your lab assistant the running maven configuration.

<!--
## Grading
- none
--> 

## References
Following some references which might help you to complete the tasks:
- [Maven Quick Reference Card][mvnqref]
- [DZone Maven Refcard][mvndzone]
- [Maven Reference Book][mvnref]
- [Maven By Example Book][mvnex]
- [Maven Central Repository][mvncentral]

[mvnqref]:    https://maven.apache.org/guides/MavenQuickReferenceCard.pdf "Maven Quick Reference Card"
[mvndzone]:   http://refcardz.dzone.com/refcardz/apache-maven-2 "DZone Maven Refcard"
[mvnref]:     http://books.sonatype.com/mvnref-book/reference "Maven Reference Book"
[mvnex]:      http://books.sonatype.com/mvnex-book/reference "Maven By Example Book"
[mvncentral]: http://search.maven.org/#browse "Maven Central Repository"

[mvninstall]: http://books.sonatype.com/mvnex-book/reference/installation-sect-maven-install.html
[zhaw-gh]:    https://github.engineering.zhaw.ch/ "ZHAW SoE GitHub Enterprise"
[mvn-archetype]:  http://books.sonatype.com/mvnref-book/reference/archetype-sect-using.html
[mvn-dependency]: http://books.sonatype.com/mvnref-book/reference/pom-relationships-sect-project-dependencies.html
[tomcat-mvn]: http://tomcat.apache.org/maven-plugin-2.1/run-mojo-features.html
[mvn-eclipse]: http://maven.apache.org/plugins/maven-eclipse-plugin/
[mvn-idea]: https://maven.apache.org/plugins/maven-idea-plugin/
[idea-build-tools]: https://www.jetbrains.com/idea/help/build-tools.html
[idea-mvn]: https://www.jetbrains.com/idea/help/maven.html
<!--
##Preparation Work before the Lab
- none
-->
## General Notes
#### Using the command line
Maven is integrated in many IDEs and can be used graphically. To learn how it works it is best to use the *native* tools. In the first two parts of this lab you will therefore primarily use the command line.
 
#### Ask for help
If you are stuck and have a problem you can not solve using the documentation, ask your colleques, the lecturer or lab assistant for help.


## Tasks

This lab consists of three parts:

1. [Setting up Maven](#part1-settingupmaven)
2. [Mastering Maven](#part2-masteringmaven)

### Part 1 - Setting up Maven
#### Installation
Ensure that the command line version of Maven is installed on your computer and that you know how to access it via the command line / terminal interface.

Find some basic info for all Systems in the [install instructions][mvninstall].

The official way to install Maven is to download and unpack the binary ZIP file to a common directory, set the environment variable `M2_HOME` and add the bin directory to your `PATH` environment variable.

##### Windows
Follow process in the [install instructions][mvninstall].

##### Unix (Linux / OS X / Solaris / FreeBSD) manual installation
Download newest apache-maven-x.x.x-bin.zip from <http://maven.apache.org/download.html>.
Open shell:
```
$ sudo unzip ~/apache-maven-x.x.x-bin.zip -d /usr/share/
$ sudo ln -s apache-maven-x.x.x /usr/share/maven
```

Open `~/.profile` (single user) or `/etc/profile` (all users) and add the following lines:

```
export M2_HOME=/usr/share/maven
export PATH=$PATH:$M2_HOME/bin
```

##### Unix (Linux / OS X / Solaris / FreeBSD) installation using package manager
An alternative option to install maven is to use the package manager of the unix system. 

* on DEB based systems (Debian,Ubuntu,...) 
  `$ sudo apt-get install maven` (this is a quite outdated version 3.0.x)
* on RPM based systems (RedHat,CentOS,Fedora,...) exists no official package (use above manual instructions).
* on OS X you can install Maven using a packet manager for OS X like Homebrew or MacPorts.
  Because the packages are usually compiled during installation you need to install Xcode beforehand. This is recommended especially, if you already have Xcode installed or you would like to install also other common unix packages. 
  Homebrew (<http://brew.sh>): 
  `$ brew install maven`
  MacPorts (<http://www.macports.org/install.php>):
  `$ port install maven2`

##### Verify installation
Open a new shell or cmd.exe session and test if maven is available:
```
$ mvn -version
Apache Maven 3.2.3 (33f8c3e1027c3ddde99d3cdebad2656a31e8fdf4; 2014-08-11T22:58:10+02:00)
Maven home: /usr/local/Cellar/maven/3.2.3/libexec
Java version: 1.8.0_20, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_20.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.10.2", arch: "x86_64", family: "mac"
```

> This concludes part 1 of the lab. You should now have a working Maven installation.



### Part 2 - Mastering Maven

In this section you will learn how to use Maven to automate an existing project. This is also called 'mavenizing' a project.

#### Fork and clone your copy of the project on GitHub
Make sure, that you have forked the PROG2-lab-IT... repository and cloned it to your local repository. 

** This should not be required, if you executed the Git & GitHub exercise **

> **Do NOT try to push to the original repository in the @PROG2 organization**

#### Create a basic POM file
Your local project directory contains only a `src` folder (beside these instructions).
It contains all the sources which typically will be checked in using version control.

'Mavenizing' an applications means basically to create a Project Object Model (POM) file describing this artifact.

- The first step is to create a basic `pom.xml` file. This can be done easiest using the Maven _archetype_ plugin.
  It is normally used to create new projects (new directory containing a pom.xml and the required files). Because we only need the pom.xml file, you should call the `mvn archetype:generate` goal in a separate temporary directory *(outside of the project git folder)*.

  See the [archetype reference page][mvn-archetype] to see the exact syntax.
  To create the correct values, you should use the following properties:
    - groupId=ch.zhaw.PROG2
    - artifactId=mvnlab
    - packageName=com.company (very often identical to the groupId, but must not be)
    - archetypeArtifactId=maven-archetype-webapp
    - interactiveMode=false
  for the rest of the properties the default values will be used, if not set.

- Copy `mvnlab/pom.xml` to your project root (next to the src directory).
- Check the content of your `pom.xml` file. (Optionally you can change the name and URL e.g. to the GitHub homepage)

- Change (`cd`) to the project directory and try to build your project using `mvn compile`. It will produce errors, because it is missing some classes. This will be solved in the next step, when you define the dependencies.
- Before committing to the repository you should add the `target/` directory to `.gitignore`. Because maven will put all generated files by default to `target/`, this will avoid to check in generated files.

> You should avoid to check in _generated_ files into version control.

- Time to commit your first changes.

#### Add dependencies
In this step you will define all the required dependencies. Maven will then automatically resolve the dependencies and download the required artifacts from [Maven Central][mvncentral].

- Usually you would have to go throug your project and find all required artifacts.
- Add the required dependencies to the `<dependencies>` element.
  To make it a bit easier following a list of the working artifacts and versions:
  (See the [dependency reference page][mvn-dependency] to see exact syntax)

| groupId                  | artifactId              | version       | scope   |
|--------------------------|-------------------------|---------------|---------|
| org.springframework      | spring-context          | 3.2.3.RELEASE | compile |
| org.springframework      | spring-webmvc           | 3.2.3.RELEASE | compile |
| org.aspectj              | aspectjrt               | 1.6.10        | compile |
| javax.inject             | javax.inject            | 1             | compile |
| javax.servlet            | servlet-api             | 2.5           | provided|
| javax.servlet.jsp        | jsp-api                 | 2.1           | provided|
| javax.servlet            | jstl                    | 1.2           | compile |
| org.springframework.data | spring-data-jpa         | 1.3.4.RELEASE | compile |
| org.springframework      | spring-jdbc             | 3.2.3.RELEASE | compile |
| org.hibernate            | hibernate-entitymanager | 4.2.3.Final   | compile |
| com.h2database           | h2                      | 1.3.173       | compile |
| org.codehaus.jackson     | jackson-mapper-asl      | 1.9.13        | compile |
| junit                    | junit                   | 4.7           | test    |
| org.springframework      | spring-test             | 3.2.3.RELEASE | test    |
| com.jayway.jsonpath      | json-path               | 0.8.1         | test    |

- What is the reason for the **scope**? what does it achieve?

- Add the following block at the end of the dependencies to configure logging:

```
    <!-- Logging -->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>1.6.6</version>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>jcl-over-slf4j</artifactId>
      <version>1.6.6</version>
      <scope>runtime</scope>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>1.6.6</version>
      <scope>runtime</scope>
    </dependency>
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.15</version>
      <scope>runtime</scope>
      <exclusions>
        <exclusion>
          <groupId>javax.mail</groupId>
          <artifactId>mail</artifactId>
        </exclusion>
        <exclusion>
          <groupId>javax.jms</groupId>
          <artifactId>jms</artifactId>
        </exclusion>
        <exclusion>
          <groupId>com.sun.jdmk</groupId>
          <artifactId>jmxtools</artifactId>
        </exclusion>
        <exclusion>
          <groupId>com.sun.jmx</groupId>
          <artifactId>jmxri</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
```

- What are the exclusions used for? Why are they used here?
  (What happens, if you comment out the <exlusions> block?)

- You can see the full dependency tree using `mvn dependency:tree -Dverbose`

- now it should be possible to compile the sources:
  `mvn clean compile`

- to make sure the tests are compiling (without running them) you can use:
  `mvn test-compile`
  (see the build lifecycle) 

#### Verify the default lifecycles
Now lets test, if the goals of the default, clean and site lifecycles work.

- Cleanup the project by using `mvn clean`
  This will delete the `target` directory, which contains all the generated files.
- What is the comand to generate all class files?
- Let's run the unit tests
  `mvn test`
- What happens, if you run `mvn package`?
- How can you skip the unit test, when you only want to package our artifact?
- Try `mvn install`. What does install do?
  (check `~/.m2/repository/ch/zhaw/PROG2/`)


#### Run an embedded tomcat
Maven allows to run web applications in an embedded tomcat (or jetty) container.
This is usefull to run integration tests (like selenium) or test your application manually.

To do this you have to integrate and configure the [maven tomcat plugin][mvn-tomcat].

- First add the tomcat maven plugin into the `<build><plugins>` block (after `<dependencies>`).

```
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <executions>
          <execution>
            <id>start-tomcat</id>
            <goals>
              <goal>run</goal>
            </goals>
            <configuration>
              <fork>true</fork>
            </configuration>
          </execution>
          <execution>
            <id>stop-tomcat</id>
            <goals>
              <goal>shutdown</goal>
            </goals>
          </execution>
        </executions> 
        <configuration>
          <port>8080</port>
          <uriEncoding>UTF-8</uriEncoding>
        </configuration>      
      </plugin>
    </plugins>
  </build>
```

- Now you can start tomcat using `mvn tomcat:run`.
- It will log the port and URLs of your application.
- To access the test application open <http://localhost:8080/mvnlab/product/searchForm> in your browser

#### Use Maven with Eclipse or IntelliJ IDEA
Often you want to manage your projects using maven, but develop in your favourite IDE.
Maven therfore supports integration plugins for the major IDEs (Eclipse, IntelliJ, Netbeans,...)
To use Maven with Eclipse, you can use the [Maven Eclipse Plugin][mvn-eclipse].
To use Maven with IntelliJ IDE, you can use the [Maven IDEA Plugin][mvn-idea] (see below).
The plugin(s) allow to generate the Eclipse/IDEA configuration files based on the pom.xml definition.

##### Eclipse
- Add the maven-eclipse maven plugin into the `<build><plugins>` block.

```
      <plugin>
          <artifactId>maven-eclipse-plugin</artifactId>
          <version>2.9</version>
          <configuration>
              <additionalProjectnatures>
                  <projectnature>org.springframework.ide.eclipse.core.springnature</projectnature>
              </additionalProjectnatures>
              <additionalBuildcommands>
                  <buildcommand>org.springframework.ide.eclipse.core.springbuilder</buildcommand>
              </additionalBuildcommands>
              <downloadSources>true</downloadSources>
              <downloadJavadocs>true</downloadJavadocs>
          </configuration>
      </plugin>

```

- Now you can automatically generate the required project files using
  `mvn eclipse:clean eclipse:eclipse`
  (the eclipse:clean goal removes first all existing eclipse project files)

- It is now possible to import the project into your Eclipse environment.

- Because the Eclipse project files can now be generated, they should not be checked into git.
  You should add the following entries to your .gitignore file:
  ```
  # Eclipse files
  .project
  .metadata
  .classpath
  .settings/
  .loadpath
  bin/
  ```

- Now `git status` should not list eclipse files

##### IntellliJ IDEA
- Add the maven-idea maven plugin into the `<build><plugins>` block.

```
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-idea-plugin</artifactId>
        <version>2.2.1</version>
      </plugin>

```

- Now you can automatically generate the required project files using
  `mvn idea:clean idea:idea`
  (the idea:clean goal removes first all existing idea project files)

- It is now possible to import the project into your IntelliJ IDEA environment.

- Because the IDEA project files can now be generated, they should not be checked into git.
  You should add the following entries to your .gitignore file:
  ```
  # IntelliJ IDEA files
  *.iml
  *.ipr
  *.ids
  *.iws
  .idea/
  ```

- Now `git status` should not list IntelliJ IDEA files

Beside using the `maven-idea-plugin`, IntelliJ IDEA has built in support for Maven. See the [IntelliJ IDEA Maven Help Page][idea-mvn].
It also has very good support for other build-tools like Gradle or Ant. See the [Buil-Tools Help page][idea-build-tools].

#### Cleanup your project

- Show the tests and running server to your lab assistant.
- Clean up your project using `mvn clean`.
  This will not remove the Eclipse / IDEA configuration. To do this you explicitly have to call the plugin goal `mvn eclipse:clean` resp. `mvn idea:clean`.
- Check in the current status to your git repository and push it upstream to your public repo on the [ZHAW SoE GitHub Server][zhaw-gh].


> This concludes part 2 of the lab. You should now master the basic Maven workflows.



#### Closing the Lab

The main repository 'PROG2-lab-IT...' contains a branch (*yourlogin*) for each student.

- All students:  
  To declare that you finished the lab, send a Pull-Request to 'your personal branch' in the main repository you forked in the beginning of the lab.  
  (e.g. Pull request from *yourrepo*/master to PROG2-lab-IT.../*yourlogin*)


> **Congratulations! You finished the Lab Build-Tools - Maven**
