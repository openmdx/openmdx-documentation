# Build from source #

This guide explains how to build _openMDX_ from the sources.

## Prerequisites ##

Make sure that you have the following software installed:

* [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/) or [OpenJDK 8](https://openjdk.java.net/projects/jdk/8/)
* [JDK 11](http://www.oracle.com/technetwork/java/javase/downloads/) or [OpenJDK 11](https://openjdk.java.net/projects/jdk/11/)
* Set the environment variable JRE\_18 so that it points to the _jre_ directory of the JDK 8 installation, e.g. _/usr/lib/jvm/java-8-openjdk-amd64/jre_
* Set the path to JDK\_11
* [Gradle 6.9](https://gradle.org/install/)
* [GIT](http://git-scm.com/downloads)

## Build ##

Clone the openMDX sources from the GIT repository:

```
git clone https://github.com/openmdx/openmdx.git openmdx
```

And then build _openMDX_.

```
cd openmdx
git checkout openmdx-v2.17.10
gradle clean
gradle assemble
```

## Eclipse project files ##

Generate the Eclipse project files as follows:

```
gradle eclipse
```

This generates the Eclipse project files for the sub-projects _client_, _core_, _portal_, _security_, _tomcat_. Import the projects into a new or existing Eclipse workspace.  

## Congratulations ##
Congratulations! You have successfully built _openMDX_ from the sources.
