### Docker

> ***NOTE**: Do **Steps 1 - 2** on Docker Hub*
1. Create a Access Tokens on Docker Hub
    1. Login to [Docker Hub](https://hub.docker.com/)
    2. Next to you Docker Hub username on the top right, click on the **drop-down arrow**
    3. Click **Account Settings** >> **Security**
    4. Click **New Access Token**
    5. Give the Access Token a **Description** then click **Create**
    6. Click **Copy and Close**
    7. Save the Access Token in a secure place. We will need it in **Step 3**
2. Create a repository
    1. Click Create Repository
    2. Give it a Name and Description *Ex*: cicd_tomcat
    3. Set the Visibility to Private
    4. Click Create
> ***NOTE**: Do **Steps 3 - 9** on Docker host*
3. Connect Docker host to Docker Hub
    1. SSH to Docker host
    2. Become root, run the below command and enter the **Access Token** at the **Password** prompt
    ```
    [centos@docker ~]$ sudo su -
    Last login: Wed Mar 25 10:30:04 UTC 2020 on pts/1
    [root@docker ~]# docker login --username <docker_hub_username>
    Password:
    Login Succeeded
    [root@docker ~]#
    ```
4. Pull Tomcat 8.5 Docker image
```
[root@docker ~]# docker pull amd64/tomcat:8.5-jre8
```
5. Run a Docker container using Tomcat 8.5 image
```
[root@docker ~]# docker run -d --name tomcat-container -p 8080:8080 docker.io/amd64/tomcat:8.5-jre8
```
6. Check if Docker container is running
```
[root@docker ~]# docker ps -a
CONTAINER ID        IMAGE                             COMMAND             CREATED             STATUS              PORTS                    NAMES
b9b14be383fe        docker.io/amd64/tomcat:8.5-jre8   "catalina.sh run"   4 seconds ago       Up 4 seconds        0.0.0.0:8080->8080/tcp   tomcat-container
[root@docker ~]#
```
7. Create a Docker image out of the running container
```
[root@docker ~]# docker commit -m "Message" -a "Author Name" <container_name> <docker_hub_username>/<docker_hub_repo_name>:<tag>
Ex: [root@docker ~]# docker commit -m "Custom Tomcat Container" -a "Hadriane" tomcat-container hadriane/cicd-tomcat:v1
```
8. Push created Docker image to Docker Hub
```
[root@docker ~]# docker push <docker_hub_username>/<docker_hub_repo_name>:<tag>
Ex: [root@docker ~]# docker push hadriane/cicd-tomcat:v1
```
9. Create a directory with appropriate permissions to store Java artifacts
```
[root@docker ~]# cd /tmp/
[root@docker tmp]# mkdir java_artifacts
[root@docker tmp]# chown ansibleadm:ansibleadm java_artifacts
```
