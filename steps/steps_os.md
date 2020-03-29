### 2 - OS

Users On Each Host

| Host / User   | jenkinsadm | anisbleadm |
|---------------|:----------:|:----------:|
| Jenkins       |     Yes    |     Yes    |
| Ansible       |     No     |     Yes    |
| Docker        |     Yes    |     Yes    |


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
