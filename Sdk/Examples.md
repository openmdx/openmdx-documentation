# openMDX Examples #

This guide explains how to build the _openMDX Examples_.

## Prerequisites ##

Make sure that you have the following software installed:

* [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/) or [OpenJDK 8](https://openjdk.java.net/projects/jdk/8/)
* [JDK 11](http://www.oracle.com/technetwork/java/javase/downloads/) or [OpenJDK 11](https://openjdk.java.net/projects/jdk/11/)
* Set the environment variable JRE\_18 so that it points to the _jre_ directory of the JDK 8 installation, e.g. _/usr/lib/jvm/java-8-openjdk-amd64/jre_
* Set the path to JDK\_11
* [Gradle 6.9](https://gradle.org/install/)
* [GIT](http://git-scm.com/downloads)

## Build ##

Get the _openMDX Examples_ sources from the GIT repository:

~~~~~~
git clone https://github.com/openmdx/openmdx-example.git openmdx-example
~~~~~~

And then build _openMDX Examples_.

~~~~~~
cd openmdx-example
git checkout openmdx-v2.17.8
gradle clean
gradle assemble
~~~~~~

## Eclipse project files ##

Generate the Eclipse project files as follows:

```
gradle eclipse
```

This generates the Eclipse project files for the sub-projects _helloworld_, _workshop_. Import the projects into a new or existing Eclipse workspace.  

## Running the JUnits ##

Now you are ready to run the JUnit tests:

~~~~~~
gradle test
~~~~~~

## Congratulations ##
Congratulations! You have successfully built and run the _openMDX Examples_.
