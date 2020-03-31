### 6 - Installing Ansible

1. Enable EPEL repo for Python Pip
```
[root@ansible ~]# yum --enablerepo=extras install -y epel-release
```

2. Install Python Pip
```
[root@ansible ~]# yum install -y python-pip
```

3. Upgrade Pip
```
[root@ansible ~]# pip install --upgrade pip
```

4. Install Ansible
```
[root@ansible ~]# pip install ansible
```

5. Create Ansible directory
```
[root@ansible ~]# mkdir /etc/ansible
```

6. Create ansibleadm user
```
useradd ansibleadm
passwd ansibleadm
```

7. Grant sudo access to ansibleadm user
    1. Open sudoers file
    ```
    visudo
    ```
    2. Add "ansibleadm      ALL=(ALL)       NOPASSWD: ALL" to the bottom of the file and save it
    ```
    ## Read drop-in files from /etc/sudoers.d (the # here does not mean a comment)
    #includedir /etc/sudoers.d
    ansibleadm      ALL=(ALL)       NOPASSWD: ALL
    ```

8. Allow SSH password login
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

9. Generate SSH key and copy ssh public key to Docker server
   1. Generate SSH key
   ```
   [ansibleadm@ansible root]$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/ansibleadm/.ssh/id_rsa):
    Created directory '/home/ansibleadm/.ssh'.
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    [ansibleadm@ansible root]$ ssh-copy-id ansibleadm@<private_ip_of_docker_server>
   ```
   2. Test by SSH into Docker server without password
   ```
   [ansibleadm@ansible root]$ ssh ansibleadm@<private_ip_of_docker_server>
   Last login: Wed Mar 25 06:29:29 2020
   [ansibleadm@docker ~]$ logout
   ```
   
10. Test ansible
    1. Create Ansible skeleton role
    ```
    [root@ansible ~]# cd /etc/ansible/
    [root@ansible ansible]# ansible-galaxy init tomcat
    - Role tomcat was created successfully
    ```
    2. Move into Tomcat directory create a hosts directory
    ```
    [root@ansible ansible]# cd tomcat/
    [root@ansible tomcat]# mkdir hosts
    ```
    
    3. Create a hosts file in hosts directory, add the following contents to it and save the file
    ```
    [tomcatservers]
    <private_ip_of_docker_server>
    ```
    
    4. Switch to ansibleadm user and do a ping test
    ```
    [root@ansible hosts]# su ansibleadm
    [ansibleadm@ansible hosts]$ ansible all -m ping -i hosts
    172.31.12.99 | SUCCESS => {
        "ansible_facts": {
            "discovered_interpreter_python": "/usr/bin/python"
        },
        "changed": false,
        "ping": "pong"
    }
    [ansibleadm@ansible hosts]$
    ```
