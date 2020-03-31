### 7 - Creating New Docker Image and Pushing To Docker Hub

1. Login to Docket Hub [here](https://hub.docker.com/)

2. Create a Access Tokens
    1. Click on the drop down arrow next to your <docker_hub_username> at the top right of the page
    2. Click on **Account Settings**
    3. Click on **Security** at the left navigation bar
    4. Click **New Access Token**
    5. Give an **Access Token Description** name
    6. Click **Create**
    7. Note down the generated **Access Token**
    8. Click **Copy and Close**

3. Create a repository
    1. Click **Create Repository**
    2. Give it a **Name** and **Description**
    3. Set the **Visibility** to **Private**
    4. Click **Create**

4. Connect Docker server to Docker Hub
    1. Login to Docker server
    2. Become root, run the below command and enter the **Access Token** at the **Password** prompt
    ```
    [centos@docker ~]$ sudo su -
    Last login: Wed Mar 25 10:30:04 UTC 2020 on pts/1
    [root@docker ~]# docker login --username <docker_hub_username>
    Password:
    Login Succeeded
    [root@docker ~]#
    ```

5. Create a new Docker image out of an existing Docker container
    1. Run the docker container if it is not already started
    ```
    [root@docker ~]# docker run -d --name tomcat-container -p 8080:8080 docker.io/amd64/tomcat:8.5-jre8
    ```
    2. Create an image out of the running container
   ```
   [root@docker ~]# docker commit -m "Message" -a "Author Name" <container_name> <docker_hub_username>/<docker_hub_repo_name>:<tag>
   Ex: [root@docker ~]# docker commit -m "Custom Tomcat Container" -a "Hadriane" tomcat-container hadriane/cicd-tomcat:v1
   ```

6. Push created Docker image to Docker Hub
```
[root@docker ~]# docker push <docker_hub_username>/<docker_hub_repo_name>:<tag>
Ex: [root@docker ~]# docker push hadriane/cicd-tomcat:v1
```
