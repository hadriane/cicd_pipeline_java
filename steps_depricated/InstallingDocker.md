### 5 - Installing Docker

> ***Note**: Click [here](https://github.com/hadriane/cicd_pipeline/blob/master/ListOfBasicDockerCommand.md) for a list of basic Docker commands*

1. Install Docker
```
[root@docker ~]# yum install -y docker
[root@docker ~]# systemctl enable docker
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[root@docker ~]# systemctl start docker
[root@docker ~]# yum --enablerepo=extras install -y epel-release
[root@docker ~]# yum install -y python-pip
[root@docker ~]# pip install --upgrade pip
[root@docker ~]# pip install docker-py
```

2. Pull docker image Tomcat 8.5
```
[root@docker ~]# docker pull amd64/tomcat:8.5-jre8
```

3. Run a docker container using Tomcat 8.5 image
```
[root@docker ~]# docker run -d --name tomcat-container -p 8080:8080 docker.io/amd64/tomcat:8.5-jre8
```

4. Test if Docker Tomcat 8.5 container works
    1. List all running Docker container
    ```
    [root@docker ~]# docker ps -a
    CONTAINER ID        IMAGE                             COMMAND             CREATED             STATUS              PORTS                    NAMES
    b9b14be383fe        docker.io/amd64/tomcat:8.5-jre8   "catalina.sh run"   4 seconds ago       Up 4 seconds        0.0.0.0:8080->8080/tcp   tomcat-container
    [root@docker ~]#

    ```
    2. Go to http://<public_ip_of_docker_server>:8080/

5. Create users for Ansible server and Jenkins server
    1. ansibleadm user
        1. Create ansibleadm user
        ```
        [root@docker ~]# useradd ansibleadm
        [root@docker ~]# passwd ansibleadm
        ```
        2. Grant sudo access to ansibleadm user
        3. Open sudoers file
        ```
        [root@docker ~]# visudo
        ```
        4. Add "ansibleadm      ALL=(ALL)       NOPASSWD: ALL" to the bottom of the file and save it
        ```
        ## Read drop-in files from /etc/sudoers.d (the # here does not mean a comment)
        #includedir /etc/sudoers.d
        ansibleadm      ALL=(ALL)       NOPASSWD: ALL
        ```
        5. Add ansibleadm to dockerroot group
        ```
        [root@docker ~]# usermod -aG dockerroot ansibleadm
        ```
    2. 
        1. Create jenkinseadm user
        ```
        [root@docker ~]# useradd jenkinseadm
        [root@docker ~]# passwd jenkinseadm
        ```
    
6. Allow SSH password login
    1. open /etc/ssh/sshd_config file
    2. Comment out "PasswordAuthentication no" and uncomment "PasswordAuthentication yes" then save the file
    ```
    # To disable tunneled clear text passwords, change to no here!
    PasswordAuthentication yes
    #PermitEmptyPasswords no
    #PasswordAuthentication no
    ```
    3. Restart sshd service
    ```
    [root@docker ~]# service sshd restart
    Redirecting to /bin/systemctl restart sshd.service
    [root@docker ~]#
    ```

8. Move on to InstallingAnsible.md](https://github.com/hadriane/cicd_pipeline/edit/master/InstallingAnsible.md) then come back here and continue on with step 9

9. Move on to [Installing and Configuring Jenkins](https://github.com/hadriane/cicd_pipeline/edit/master/InstallingJenkins.md) step 13 then come back here and continue on with step 10

10. Disallow SSH password login
    1. open /etc/ssh/sshd_config file
    2. Comment out "PasswordAuthentication yes" and uncomment "PasswordAuthentication no" then save the file
    ```
    # To disable tunneled clear text passwords, change to no here!
    #PasswordAuthentication yes
    #PermitEmptyPasswords no
    PasswordAuthentication no
    ```
    3. Restart sshd service
    ```
    [root@docker ~]# service sshd restart
    Redirecting to /bin/systemctl restart sshd.service
    [root@docker ~]#
    ```
 
11. Create a directory to store Java artifacts
    1. Create a directory
    ```
    [root@docker ~]# cd /tmp/
    [root@docker tmp]# mkdir java_artifacts
    ```
    2. Change ownership of the directory to jenkinsadm
    ```
    [root@docker tmp]# chown jenkinsadm:jenkinsadm java_artifacts
    ```
