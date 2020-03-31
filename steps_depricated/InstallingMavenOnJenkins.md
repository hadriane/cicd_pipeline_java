### 4 - Installing and Configuring Maven on Jenkins server

1. Installing Maven
    1. Download Maven
    ```
    [root@jenkins ~]# yum install -y wget
    [root@jenkins ~]# cd /tmp/
    [root@jenkins tmp]#  wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
    [root@jenkins tmp]#  tar -xvzf apache-maven-3.6.3-bin.tar.gz
    [root@jenkins tmp]# mv apache-maven-3.6.3 /opt/maven
    [root@jenkins tmp]#  rm -f apache-maven-3.6.3-bin.tar.gz
    ```
2. Set Maven environment variable
    1. open /root/.bash_profile and modify it to like below then save the file
    ```
    # User specific environment and startup programs
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
    M2_HOME=/opt/maven
    M2=/opt/maven/bin
    PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2
    ```
    2. logoff, login then check the enviroment variable
    ```
    [root@jenkins ~]# exit
    logout
    [root@jenkins centos]# sudo su -
    Last login: Mon Mar 23 07:32:38 UTC 2020 on pts/0
    [root@jenkins ~]#
    [root@jenkins ~]# echo $M2
    /opt/maven/bin
    [root@jenkins ~]# echo $M2_HOME
    /opt/maven
    [root@jenkins ~]#
    ```
3. Configure Maven plugin on Jenkins server
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. On the left navigation bar click on **Manage Jenkins** >> **Manage Plugins** >> **Available tab**
    3. Search for "Maven" using the **Filter** on the top right
    4. Look for and tick the check box for **Maven Integration** & **Maven Invoker** from the search results
    5. Click on **Install without restart** on the bottom left
    6. On the left navigation bar click on **Manage Jenkins** >> **Global Tool Configuration**
    7. In the **Maven** section
        1. Click **Add Maven**
        2. Untick **Install automatically**
        3. Give **Name** as "M2_HOME"
        4. Give **MAVEN_HOME** as "/opt/maven"
        5. Click **Save**
