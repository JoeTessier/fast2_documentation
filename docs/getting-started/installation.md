---
weight : 10
draft : false

title : Installation
icon : las la-laptop-code

---
## Requirements
The installation of Fast2 requires a few environment specifications to run properly : 

* JRE8, JRE11 : you can either get it from Oracle or [OpenJDK](https://developers.redhat.com/products/openjdk/download). If you have multiple JDK/JRE already installed, point out the correct one in the `config/env.properties` file of the Fast2 installation folder.
* RAM : we highly recommend having 8GB or more, although 4GB might be enough for design stage.
* Processor : 8 CPUs.

While setting up the production server for Fast2, make sure to scale the Fast2 machine accordingly. You may need to increase the allocated memory for both the broker and the background database. If you planned to deal with campaigns of a few millions of documents, setting **8GB** of memory for the [broker](/documentation/configuration/#configure-the-broker) and **8GB** for the [database](/documentation/elasticsearch/#memory) as well is a good starting point. 

Make sure to confirm the compatibility between Elasticsearch and your environment at [Elasticsearch Support Matrix](https://www.elastic.co/fr/support/matrix).

## Fast2 packages
The Fast2 distribution you need depends on your target environment. It exists three way to deploy a Fast2 :
- On premise: regular package, as an all-in-one zip file
- AWS: Standard AMIs
- K8S: Docker Images

Each distribution ships the following
- A broker with one embedded worker and a user interface
- An additional worker with all tasks catalog
- A template to create workers with custom tasks

## Root folder anatomy
{{< image "documentation/rootFolder.png" "Root folder anatomy" "50%">}}

## Start Fast2 Broker
Once the regular Fast2 package is unzipped, Fast2 can be launched right away.

Once the regular Fast2 package is unzipped, Fast2 can be launched right away.

Whether Fast2 is launched from the batch file or as a service on your environment, the UI will be available at [http://localhost:1789/]().

By default, Fast2 Broker starts an embedded Elastic Search and an embedded Fast2 Worker. 

All commands below are to be run under the Fast2 install path (where the Zip has been unzipped). 

### From command line

=== ":fontawesome-brands-windows: Windows"

    Go into the Fast2 install folder, and run :

    ```cmd
    C:\path-to-fast2\> startup-broker.bat
    ```
 
    Administrator rights might be required since Fast2 will handle some port communications. 

=== ":fontawesome-brands-linux: Linux"

    The following Linux installation steps work for most of Unix-based sytems. 
    Elasticsearch cannot be started from root user, you will need to create a secondary user to start the database binary alongside your Fast2 process.

    Once connected as the latter user, start Elasticsearch via its binaries.

    Then, since you started Elasticsearch manually, disable the command triggering Fast2 to start the embedded Elasticsearch, from the `config/application.properties` file : 

    ```log
    broker.elasticsearch.embedded.enabled=false
    ```

    You can now properly execute the following script: 

    ```
    $ ./startup-broker.sh
    ```
    
    To quit the Fast2 process, just hit `Ctrl+C` in the command line the startup file opened.

To end the Fast2 process, just hit `Ctrl+C` in the command line the startup file opened.

### As service

=== ":fontawesome-brands-windows: Windows"

    Go into the Fast2 installation folder, and open the Windows Command Prompt.

    To install the service : 

    ```cmd
    C:\path-to-fast2\service\windows> Fast2_broker_service.exe install
    ```

    Your machine may prompt a message asking to download .NET components. Please click [OK] and proceed.

    Once this command is complete, you should see in your services registory a newly installed Fast2 service. You can start/stop/restart it as any other service, or via the Command Prompt (just replace `install` in the previous command by _start_/_stop_/_uninstall_/_restart_/_status_).

    The logs of the service will be available from the `path-to-fast2\service\log` folder.

=== ":fontawesome-brands-linux: Linux"

    There are several ways to create a service under linux distribution. We will do it through systemd. 
    Its major benefit is that it has been the default init system for the majority of linux distributions (Ubuntu, Red Hat, Fedora...).

    <br />

    ##### :material-numeric-1-circle: Create a user for Fast2

    Since the embedded database cannot be started in sudo mode, an additional user needs to be created in the Linux machine so the broker will successfully initiate the database bootup.

    Let's condider here our user to be *fast2user*. 

    Head out to the `./startup-broker.sh` and get the user start the broker by switching users (with `su fast2user -c`) for the Java command. 

    The result should be as follows:

    ```diff
    - "$JAVA" -Xmx$BROKER_MAX_MEMORY -jar fast2-broker-package-X.Y.Z.jar
    + su fast2user -c "$JAVA -Xmx$BROKER_MAX_MEMORY -jar fast2-broker-package-X.Y.Z.jar"
    ```

    <br/>

    ##### :material-numeric-2-circle: Execution path

    Edit the `ExectStart` field from the file `service/linux/fast2-broker.service` by changing the `PATH/TO/FAST2` portion: set it to Fast2 install path.
    
    ```
    [Unit]
    Description=Fast2 Broker

    [Service]
    ExecStart=/home/userName/fast2-complete-package-2.0.0/startup-broker.sh

    [Install]
    WantedBy=default.target
    ```

    <br />

    ##### :material-numeric-3-circle: Symbolic link

    Now link it to the `/etc/systemd/system` directory through a symbolic link.

    ```
    $ sudo ln -s SOURCE TARGET

    $ sudo ln -s service/linux/fast2-broker.service /etc/systemd/system
    ```

    If the links are broken once they're created, you probably need to put an absolute path for the target as follow ;

    ```
    $ sudo ln -s /home/userName/fast2-complete-package-2.0.0/service/linux/fast2-broker.service /etc/systemd/system
    ```

    Next, reload systemd services unit and enable them :

    ```
    $ systemctl daemon-reload
    $ systemctl enable fast2-broker.service
    ```

    The terminal should prompt the following message :

    ```
    Created symlink from /etc/systemd/system/default.target.wants/fast2-broker.service to /etc/systemd/system/fast2-broker.service.
    ```

    <br />
    
    ##### :material-numeric-4-circle: Script uses
    
    Test your script by starting it and then checking the status :

    ```
    $ service fast2-broker start

    $ service fast2-broker status

    OR

    $ systemctl start fast2-broker.service

    $ systemctl status fast2-broker.service
    ```

    You can restart or stop the service at anytime with the commands : 

    ```
    $ service fast2 start | restart | stop | status
    ```

## Start Fast2 Worker

The Broker starts an embedded worker by default.

=== ":fontawesome-brands-windows: Windows"

    If you wish to start multiple workers, just hit :

    ```cmd
    C:\path-to-fast2\> startup-worker.bat
    ```

=== ":fontawesome-brands-linux: Linux"

    ```
    ./startup-worker.sh
    ```

If the worker and broker are not booted up on the same machine, you need to setup the Broker host name in the worker configuration file.
Edit the file `config/application.properties` and modify `broker.host` accordingly.

You can setup Fast2 Worker as a service the same way you did for the Fast2 Broker.


