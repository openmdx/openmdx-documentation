# openMDX 2.10 for _Apache TomEE_ Step-by-Step Guide #

This guide explains how to install, setup and deploy the examples of _openMDX 2.10_ on _Apache TomEE_.

In this guide we use _Apache TomEE_ to deploy the sample applications. However, if you prefer you can deploy the applications also on any other _J2EE_ Application Server.

__IMPORTANT:__ This guide assumes that the _openMDX 2.10_ projects are successfully setup as described in [openMDX 2.10 for Ant Step-by-Step](./StepByStepAnt.md).

Open a shell and go to the directory where you have installed openMDX 2.10, e.g. _/tmp/dev_. Set the environment by executing _setenv.bat_ in Windows platforms and _setenv.sh_ on Unix platforms.

Then go to the directory _./openmdx2-example/helloworld_. Run the command _ant assemble_. This builds the _EARs_ which we will deploy on _Apache TomEE_. The console output looks as shown below.

![img](files/StepByStepTomEE/StepByStepTomcat.pic090.png)

The generated _EAR_ is located in the directory _./openmdx2-example/jre-1.6/helloworld/deployment-unit_. Copy the file _openmdx-helloworld.ear_ to the directory _$CATALINA_BASE/apps_ as shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic100.png)

Next we have to add the user _guest_ to the _tomcat-user.xml_ which allows us to login to the _helloworld_ application. Open the file _$CATALINA_BASE/conf/tomcat-users.xml_. Add a new entry for the user _guest_ (if does not already exist) and add the role _openMDXUser_ as shown below.

![img](files/StepByStepTomEE/StepByStepTomcat.pic120.png)

In a next step we have to prepare _TomEE_ so that it is able to run _openMDX_ based applications.

Create the file _setenv.sh_ in _$CATALINA_BASE/bin_ for Linux platforms:

~~~~~~
#!/bin/sh

# [openMDX]
export JAVA_OPTS="$JAVA_OPTS -Xmx800M"
export JAVA_OPTS="$JAVA_OPTS -XX:MaxPermSize=256m"
export JAVA_OPTS="$JAVA_OPTS -Djava.protocol.handler.pkgs=org.openmdx.kernel.url.protocol"
# export JAVA_OPTS="$JAVA_OPTS -Dorg.openmdx.persistence.jdbc.useLikeForOidMatching=false"
# export JAVA_OPTS="$JAVA_OPTS -Djavax.jdo.option.TransactionIsolationLevel=read-committed"
export CLASSPATH=$CLASSPATH:$CATALINA_BASE/bin/openmdx-system.jar
# [openMDX]

echo "Using JAVA_OPTS:       $JAVA_OPTS"
~~~~~~

Create the file _setenv.bat_ in _%CATALINA_BASE%/bin_ for Windows platforms:

~~~~~~
REM [openMDX]
set JAVA_OPTS=%JAVA_OPTS% -Xmx800M 
set JAVA_OPTS=%JAVA_OPTS% -XX:MaxPermSize=256m
set JAVA_OPTS=%JAVA_OPTS% -Djava.protocol.handler.pkgs=org.openmdx.kernel.url.protocol
REM JAVA_OPTS=%JAVA_OPTS% -Dorg.openmdx.persistence.jdbc.useLikeForOidMatching=false
REM JAVA_OPTS=%JAVA_OPTS% -Djavax.jdo.option.TransactionIsolationLevel=read-committed
set "CLASSPATH=%CLASSPATH%;%CATALINA_BASE%\bin\openmdx-system.jar"
REM [openCRX]

echo Using JAVA_OPTS:       "%JAVA_OPTS%"
~~~~~~

Then copy _openmdx-system.jar_ to _$CATALINA_BASE/bin_.

~~~~~~
> cp /tmp/dev/openmdx2/jre-1.6/core/lib/openmdx-system.jar $CATALINA_BASE/bin
~~~~~~

Finally start _TomEE_ with _$CATALINA_BASE/bin/catalina.sh run_. This starts _TomEE_ and deploys the application _helloworld_. The console output should look as shown below.

![img](files/StepByStepTomEE/StepByStepTomcat.pic130.png)

Next navigate to the URL _http://localhost:8080/openmdx-helloworld/_. This opens the _helloworld_ login page. Enter the user _guest_ and the password which you have defined in the _tomcat-users.xml_.

![img](files/StepByStepTomEE/StepByStepTomcat.pic140.png)

The main page of the _helloworld_ application is shown after successful login. The GUI of the _helloworld_ application uses the generic _openMDX/Portal_ GUI. The GUI is not customized, that's why labels and icons do not look very user-friendly. However, the GUI is fully workable.

![img](files/StepByStepTomEE/StepByStepTomcat.pic150.png)

In order to test the _sayHello()_ operation, go to the menu _Pane:Op:90000_ and select the menu entry _Pane:Op:Tab:sayHello_ as shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic160.png)

The _sayHello()_ operation takes as parameter the language which makes _helloworld_ to return a language-specific _Say Hello_ text. Enter one of the languages _de_, _en_ or _fr_ and click _OK_.

![img](files/StepByStepTomEE/StepByStepTomcat.pic170.png)

The GUI invokes the operation _sayHello()_ which returns the _Say Hello_ message as result which is shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic180.png)

Stop _TomEE_ with _$CATALINA_BASE/bin/catalina.sh stop_.

In a next step we will build and deploy the _workshop_ application. Go back to the shell and change to the directory _./openmdx2-example/workshop_. Run the command _ant assemble_.

![img](files/StepByStepTomEE/StepByStepTomcat.pic190.png)

Next copy the EAR _openmdx-example-workshop.ear_ from the directory _./openmdx2-example/jre-1.6/workshop/deployment-unit_ to the directory _$CATALINA_BASE/apps_ as shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic200.png)

Because the _workshop_ example accesses a database we have to add a JDBC datasource configuration to the configuration _tomee.xml_. Open the file _./openmdx2-example/workshop/src/connector/openejb-3/openejb.xml_ and copy/paste the configuration entry into the file _$CATALINA_BASE/conf/tomee.xml_ as shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic210.png)

Compare the contents of your _apps_ directory with the directory structure shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic230.png)

Before restarting _TomEE_ clean the contents of the directory _work_ and _temp_. This makes sure that we do not deploy old files.

Start _TomEE_ with _$CATALINA_BASE/bin/catalina.sh run_.

![img](files/StepByStepTomEE/StepByStepTomcat.pic250.png)

Launch a browser and navigate to _http://localhost:8080/openmdx-workshop/_ and login as _guest_:

![img](files/StepByStepTomEE/StepByStepTomcat.pic260.png)

Next you should see the main page of the workshop application:

![img](files/StepByStepTomEE/StepByStepTomcat.pic290.png)

The project comes with some basic customizing. E.g. it comes with a wizard which can be launched from the menu item _Wizards > Create New Project..._. A wizard is a user-defined GUI extension. Wizards are a powerful and flexbile way to extend the standard _openMDX/Portal GUI_. Wizards are implemented as standard _JSPs_ and as such have access to the full functionality of the application's API. The source code of the wizard is located in the directory _./openmdx2-example/workshop/src/data/org.openmdx.example/wizards/en_US_.

![img](files/StepByStepTomEE/StepByStepTomcat.pic300.png)

Before we can use the wizard we have to create the team member _The Boss_. In the tab _Team Members_ select _New > Team Member_ and fill out the form as shown below:

![img](files/StepByStepTomEE/StepByStepTomcat.pic310.png)

Next launch the wizard. Enter values for project name, project manager and project tasks and click OK. After successful completion the wizards returns to the standard GUI which displays the newly created objects.

![img](files/StepByStepTomEE/StepByStepTomcat.pic320.png)

## Congratulations ##
Congratulations! You have successfully built and deployed the _openMDX SDK 2.10_ projects on _TomEE_.