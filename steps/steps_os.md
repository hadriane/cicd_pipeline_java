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
3. Generating SSH keys for users
> ***Note**: For jenkinsadm, generate SSH key on Jenkins host and for ansibleadm, generate SSH keys on Ansible host*
    
    1. Generate SSH key
    ```
    [centos@jenkins ~]$ sudo su -
    [centos@jenkins ~]$ su <username>
    [<username>@jenkins root]$ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/gituser/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    [<username>@jenkins root]$
    ```
        
        
