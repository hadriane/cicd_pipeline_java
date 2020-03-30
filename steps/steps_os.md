### 2 - OS

User On Each Host

| Server / Username | jenkinsadm | anisbleadm |
|-------------------|:----------:|:----------:|
| Jenkins           |     Yes    |     Yes    |
| Ansible           |     No     |     Yes    |
| Docker            |     Yes    |     Yes    |


1. Change server hostname and SSH timeout for all servers
    1. Change server hostname
        1. Use the below command to change the hostname of the server
        ```
        [root@ip-12-34-56-78 ~]# hostnamectl set-hostname new-hostname
        ```
    2. Change SSH timeout
        1. Open /etc/ssh/sshd_config file
        2. Uncomment and edit the following lines like below then save the file. This will give us 45 minustes of idle time
        ```
        ClientAliveInterval 900
        ClientAliveCountMax 3
        ```
    3. Reboot the machine
    ```
    [root@ip-12-34-56-78 ~]# reboot -h now
    ```
    4. Repeat the steps for all servers
2. Create users
    1. Create user according to *User On Each Host* table above
    ```
    [centos@jenkins ~]$ sudo su -
    [root@jenkins ~]# useradd <username>
    [root@jenkins ~]# passwd <username>
    ```
3. Add uses to necessary groups
    1. **FILL IN**
4. Grant sudo access to ansibleadm user on Ansible host
    1. Open sudoers file
    ```
    [centos@ansible ~]$ sudo su -
    [root@ansible ~]# visudo
    ```
    2. Add "ansibleadm      ALL=(ALL)       NOPASSWD: ALL" to the bottom of the file and save it
    ```
    ## Read drop-in files from /etc/sudoers.d (the # here does not mean a comment)
    #includedir /etc/sudoers.d
    ansibleadm      ALL=(ALL)       NOPASSWD: ALL
    ```
5. Generating SSH keys for users
    > ***Note**: For jenkinsadm, generate SSH key on Jenkins host and for ansibleadm, generate SSH keys on Ansible host*
    1. Generate SSH key
    ```
    [centos@jenkins ~]$ sudo su -
    [centos@jenkins ~]$ su <username>
    [<username>@jenkins root]$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    [<username>@jenkins root]$
    ```
6. Copy SSH keys over to necessary servers
    1. Allow SSH password login
        > ***Note**: Do the following on Jenkins host and Docker host only*
        1. Open /etc/ssh/sshd_config file
        2. Comment out "PasswordAuthentication no" and uncomment "PasswordAuthentication yes" then save the file
        ```
        # To disable tunneled clear text passwords, change to no here!
        PasswordAuthentication yes
        #PermitEmptyPasswords no
        #PasswordAuthentication no
        ```
        3. Restart sshd service
        ```
        [root@jenkins ~]# service sshd restart
        Redirecting to /bin/systemctl restart sshd.service
        [root@jenkins ~]#
        ``` 
    2. On Ansible host
        1. Copy ansibleadm SSH key to Jenkins host
        ```
        [centos@ansible ~]$ sudo su -
        [root@ansible ~]# ssh-copy-id ansibleadm@<private_ip_of_jenkins_server>
        ```
        2. Copy ansibleadm SSH key to Docker host
        ```
        [centos@ansible ~]$ sudo su -
        [root@ansible ~]# ssh-copy-id ansibleadm@<private_ip_of_docker_server>
        ```
    3. Disallow SSH password login
        > ***Note**: Do the following on Jenkins host and Docker host only*
        1. Open /etc/ssh/sshd_config file
        2. Comment out "PasswordAuthentication yes" and uncomment "PasswordAuthentication no" then save the file
        ```
        # To disable tunneled clear text passwords, change to no here!
        #PasswordAuthentication yes
        #PermitEmptyPasswords no
        PasswordAuthentication no
        ```
        3. Restart sshd service
        ```
        [root@jenkins ~]# service sshd restart
        Redirecting to /bin/systemctl restart sshd.service
        [root@jenkins ~]#
        ``` 
7. Enable yum repositories
    > ***Note**: Do the below step only on Jenkins host
    1. Enable Jenkins repoistory
    ```
    [centos@jenkins ~]$ sudo su -
    [root@jenkins ~]# curl --silent --location http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo | sudo tee /etc/yum.repos.d/jenkins.repo
    [jenkins]
    name=Jenkins-stable
    baseurl=http://pkg.jenkins.io/redhat-stable
    gpgcheck=1
    [root@jenkins ~]# sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
    ```
    > ***Note**: Do the below step only on Ansible and Docker host
    2. Enable EPEL repository
    ```
    [centos@ansible ~]$ sudo su -
    [root@ansible ~]# yum --enablerepo=extras install -y epel-release
    ```
8. Install packages
    > ***Note**: Do the below step on all hosts
    1. install wget
    ```
    [root@jenkins ~]# yum install -y wget
    ```
    > ***Note**: Do steps only on Jenkins hosts
    2. Install Java 1.8
    ```
    [root@jenkins ~]# yum install -y java-1.8*
    ```
