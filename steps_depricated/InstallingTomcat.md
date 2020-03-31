### 5 - Installing and Configuring Tomcat

1. [Change server hostname and SSH timeout for all servers](https://github.com/hadriane/cicd_pipeline/blob/master/ChangeHostnameAndSSHTimeout.md)

2. Install wget
```
[root@tomcat ~]# sudo su -
[root@tomcat ~]# yum install -y wget
```

3. Install Java 1.8
```
[root@tomcat ~]# yum install -y java-1.8*
```

4. Find Java executable and take the last entry
```
[root@tomcat ~]# find /usr/lib/jvm/java-1.8* | head -n 3
/usr/lib/jvm/java-1.8.0
/usr/lib/jvm/java-1.8.0-openjdk
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
```

5. Set Java environment variable
    1. open /root/.bash_profile and modify it to like below then save the file
    ```
    # User specific environment and startup programs
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
    PATH=$PATH:$HOME/bin:$JAVA_HOME
    ```
    2. logoff, login then check the enviroment variable
    ```
    [root@tomcat ~]# exit
    logout
    [root@tomcat centos]# su -
    Last login: Mon Mar 23 04:55:32 UTC 2020 on pts/2
    [root@tomcat ~]# echo $JAVA_HOME
    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
    [root@tomcat ~]#
    ```

6. Downalod Tomcat
```
[root@tomcat ~]# cd /tmp/
[root@tomcat tmp]# wget https://downloads.apache.org/tomcat/tomcat-8/v8.5.53/bin/apache-tomcat-8.5.53.tar.gz
[root@tomcat tmp]# tar -xvzf apache-tomcat-8.5.53.tar.gz
[root@tomcat tmp]# mv apache-tomcat-8.5.53 /opt/tomcat
[root@tomcat tmp]# rm -f apache-tomcat-8.5.53.tar.gz
```

7. Start Tomcat
```
[root@tomcat tmp]# cd /opt/tomcat/bin/
[root@tomcat bin]# ./startup.sh
Using CATALINA_BASE:   /opt/tomcat
Using CATALINA_HOME:   /opt/tomcat
Using CATALINA_TMPDIR: /opt/tomcat/temp
Using JRE_HOME:        /
Using CLASSPATH:       /opt/tomcat/bin/bootstrap.jar:/opt/tomcat/bin/tomcat-juli.jar
Tomcat started.
[root@tomcat bin]#
```

8. Allow access to Tomcat Manager App & Host Manager
    > ***Note**: Only do the following for POC servers, never for production sevres*
    1. Open /opt/tomcat/webapps/manager/META-INF/context.xml & /opt/tomcat/webapps/host-manager/META-INF/context.xml file
    2. Comment out **Valve className** and save the file
    ```
    <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
       allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
    ```

9. Update Tomcat users information
    1. Open /opt/tomcat/conf/tomcat-users.xml file
    2. Add the below config to the bottom of the file above **</tomcat-users>** line adter changing the password for **admin**, **deployer**, & **tomcat** then save the file
    ```
    <role rolename="manager-gui"/>
    <role rolename="manager-script"/>
    <role rolename="manager-jmx"/>
    <role rolename="manager-status"/>
    <user username="admin" password="s3cret" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
    <user username="deployer" password="s3cret" roles="manager-script"/>
    <user username="tomcat" password="s3cret" roles="manager-gui"/>
    ```

10. Restart Tomcat server
```
[root@tomcat tomcat]# cd /opt/tomcat/bin
[root@tomcat bin]# ./shutdown.sh
Using CATALINA_BASE:   /opt/tomcat
Using CATALINA_HOME:   /opt/tomcat
Using CATALINA_TMPDIR: /opt/tomcat/temp
Using JRE_HOME:        /
Using CLASSPATH:       /opt/tomcat/bin/bootstrap.jar:/opt/tomcat/bin/tomcat-juli.jar
[root@tomcat bin]# ./startup.sh
Using CATALINA_BASE:   /opt/tomcat
Using CATALINA_HOME:   /opt/tomcat
Using CATALINA_TMPDIR: /opt/tomcat/temp
Using JRE_HOME:        /
Using CLASSPATH:       /opt/tomcat/bin/bootstrap.jar:/opt/tomcat/bin/tomcat-juli.jar
Tomcat started.
[root@tomcat bin]#
```

10. Login to Tomcat
    1. Go to http://<public_ip_of_tomcat_server>:8080
    2. Click on **Manager App** on the right
    3. Login using username "admin" and password set in step 9
 
