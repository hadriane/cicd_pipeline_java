### Ansible

> ***NOTE**: All **Steps** below are done on Ansible host
1. Create a diretory for Ansible
```
[centos@ansible ~]$ sudo su -
[root@ansible ~]# mkdir /etc/ansible
```
2. Create an Ansible skeleton role
```
[root@ansible ~]# cd /etc/ansible/
[root@ansible ~]# ansible-galaxy init docker
```
3. Move into Tomcat directory create a hosts directory
```
[root@ansible tomcat]# mkdir -p docker/hosts
```
4. Create a hosts file in hosts directory with contents of this [file](https://github.com/hadriane/cicd_pipeline_java/blob/master/ansible_roles/hosts)
> ***NOTE**: For **Step 5** change the **<private_ip_of_docker_server>** accordingly*
5. Create an Ansible Playbook named docker-container.yml with contents of this [file](https://github.com/hadriane/cicd_pipeline_java/blob/master/ansible_roles/docker-container.yml)
> ***NOTE**: For **Step 6** change the **<your_docker_hub_username>** accordingly*
6. Give ansible folder and its contents the appropriate owners
```
[root@ansible ~]# chown -R ansibleadm:ansibleadm /etc/ansible
```
