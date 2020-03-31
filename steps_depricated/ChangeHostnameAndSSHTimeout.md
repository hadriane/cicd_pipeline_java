### 1 - Change server hostname and SSH timeout for all servers
1. Repeat the following steps for all servers
    1. Change server hostname
        1. use the below command to change the hostname of the server
        ```
        [root@jenkins ~]# hostnamectl set-hostname new-hostname
        ```
    2. Change SSH timeout
        1. open /etc/ssh/sshd_config file
        2. uncomment and edit the following lines like below. This will give us 45 minustes of idle time
        ```
        ClientAliveInterval 900
        ClientAliveCountMax 3
        ```
    3. Reboot the machine
