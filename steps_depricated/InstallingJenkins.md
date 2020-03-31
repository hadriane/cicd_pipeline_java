### 2 - Installing and Configuring Jenkins

1. Install Java 1.8
    ```
    [root@jenkins ~]# yum install -y java-1.8*
    
    ```
2. Find Java executable and take the last entry
    ```
   [root@jenkins ~]# find /usr/lib/jvm/java-1.8* | head -n 3
    /usr/lib/jvm/java-1.8.0
    /usr/lib/jvm/java-1.8.0-openjdk
    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
    ```
3. Set Java environment variable
    1. open /root/.bash_profile and modify it to like below then save the file
    ```
    # User specific environment and startup programs
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
    PATH=$PATH:$HOME/bin:$JAVA_HOME
    ```
    2. logoff, login then check the enviroment variable
    ```
    [root@jenkins ~]# exit
    logout
    [root@jenkins centos]# su -
    Last login: Mon Mar 23 04:55:32 UTC 2020 on pts/2
    [root@jenkins ~]# echo $JAVA_HOME
    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64
    [root@jenkins ~]#
    ```
4. Enable Jenkins repo
    ```
    [root@jenkins ~]# curl --silent --location http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo | sudo tee /etc/yum.repos.d/jenkins.repo
    [jenkins]
    name=Jenkins-stable
    baseurl=http://pkg.jenkins.io/redhat-stable
    gpgcheck=1
    [root@jenkins ~]#
    [root@jenkins ~]# sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
    [root@jenkins ~]#
   ```
5. Install Jenkins
    ```
    [root@jenkins ~]# yum install -y jenkins
    ```
6. Enable and start Jenkins
    ```
    [root@jenkins ~]# systemctl enable jenkins
    jenkins.service is not a native service, redirecting to /sbin/chkconfig.
    Executing /sbin/chkconfig jenkins on
    [root@jenkins ~]# systemctl start jenkins
    [root@jenkins ~]#
    ```
7. Get the initial Jenkins password
    ```
    [root@jenkins ~]# cat /var/lib/jenkins/secrets/initialAdminPassword
    c3e29b1c90924c1aaa713a3358a32d81
    ```
8. Login to Jenkins
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. Enter the password from step 7
    3. Do not install any plugins for the moment
    4. Click **Start using Jenkins**
    5. Change Jenkins password
        1. Click on the drop down arrow next to **admin** at the right
        2. Click **Configure**
        3. Change the **Password**
        4. Click **Save**
        5. Login again with the new password

9. Create a user and generate SSH key to connect to Github
    1. Create a user "gituser"
    ```
    [centos@jenkins ~]$ sudo su -
    [root@jenkins ~]# useradd gituser
    [root@jenkins ~]# passwd gituser
    [root@jenkins ~]# su gituser
    ```
    2. Generate SSH key for "gituer"
    ```
    [gituser@jenkins root]$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/gituser/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    [gituser@jenkins root]$
    ```
10. Copy the SSH public key to Github
    1. Copy the contents of the public key (except for the "gituser@jenkins" part at the end)
    ```
    [gituser@jenkins root]$ cd /home/gituser/.ssh/
    [gituser@jenkins .ssh]$ cat id_rsa.pub
    ssh-rsa XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/gPcTH32rPdR+c7OWTlJz5Xxu3NhilVAf8tt1tazzuwocdhN9CukhkoH3S2H5CVUstAUInHpf6UOR6y0w40JJgo8eF4X4FUDAZLnnGXuCOHagoWkwDB5yNuqnWyn9QwhiCspiLinVLtAHNWqS1UoJ5QsODOGv8E+pqDgZOL9KD2ZvP1nKmu9fqp2Dae1UkaHqXzBtPEVQiHNfu1kRBEGzRd/6d3XHpkkousv8z/QxwP4Disawvis7XkPnRxbB8NKzGMsH9lBT6sonQo56tW1p gituser@jenkins
    [gituser@jenkins .ssh]$
    ```
    2. Log into Github
    3. Click the **drop-down arrow** next to your Avatar on the top right
    4. Click **Settings**
    5. Click **SSH and GPG keys**
    6. Click **New SSH key**
    7. Give it a **Title** EX: Jenkins_Server_gituser
    8. Paste the SSH public key copied earlier into the **Key** box
    9. Click **Add SSH key**

11. Create a user to SSH into Docker server
    1. Create jenkinseadm user
    ```
    [root@docker ~]# useradd jenkinseadm
    [root@docker ~]# passwd jenkinseadm
    ```
12. Move on to [Installing Docker](https://github.com/hadriane/cicd_pipeline/edit/master/InstallingDocker.md)

13. Generate SSH key for jenkinseadm user and copy it to Docker server
    1. Generate SSH key for jenkinsadm
    ```
    [root@jenkins ~]# su jenkinsadm
    [jenkinsadm@jenkins root]$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/jenkinsadm/.ssh/id_rsa):
    Created directory '/home/jenkinsadm/.ssh'.
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    [jenkinsadm@jenkins root]$
    ```
    2. Copy SSH public key to Docker server
    ```
    [jenkinsadm@jenkins root]$ ssh-copy-id jenkinsadm@<private_ip_of_docker_server>
    ```

14. Copy SSH private key for jenkinseadm user to Jenkins installation folder
    1. Copy SSH private key
    ```
    [root@jenkins .ssh]# cp /home/jenkinsadm/.ssh/id_rsa /var/lib/jenkins/.ssh/jenkinsadm.id_rsa
    ```
    2. Change permissions and ownership of the key
    ```
    [root@jenkins .ssh]# chmod 0600 /var/lib/jenkins/.ssh/jenkinsadm.id_rsa
    [root@jenkins .ssh]# chown jenkins:jenkins /var/lib/jenkins/.ssh/jenkinsadm.id_rsa
    ```

15. Continue on with [Installing Docker](https://github.com/hadriane/cicd_pipeline/edit/master/InstallingDocker.md)
