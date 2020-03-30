## Building A CI/CD Pipeline


### Purpose

The purpose of building a CI/CD pipeline is to automate steps in software delivery process


### Tools

The tools we would be using to build a CI/CD pipeline

|         |   **Tools**   |            |
|---------|---------------|------------|
| Jenkins |     Maven     |   Ansible  |
|  Docker |  Docker Hub   |   Tomcat   |
|   Git   |    Github     |   AWS EC2  |



### Infrastructure Design
![Infrastructure Design](https://github.com/hadriane/cicd_pipeline_java/blob/master/images/Infrastructure_Design.png)


### Overview of Steps

**[AWS](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/aws.md)**
1. Create Security Groups
2. Launch AWS EC2 instances
3. Allocate each AWS EC2 instance a pulblic ip address

**[OS](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/os.md)**
1. Change server hostname and SSH timeout for all servers
2. Create users
3. Add uses to necessary groups
4. Grant sudo access to ansibleadm user
5. Genetate SSH keys for users
6. Copy SSH keys over to necessary servers
7. Enable yum repositories
8. Install packages

**[Github](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/github.md)**
1. Get jenkinsadm SSH key from Jenkins server to Github
2. Copy jenkinsadm SSH key from Jenkins server to Github
3. Fork "helloworld" repo

**[Docker](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/docker.md)**
1. Create a Access Tokens
2. Create a repository
3. Connect Docker host to Docker Hub
4. Pull Tomcat 8.5 Docker image
5. Run a Docker container using Tomcat 8.5 image
6. Check if Docker container is running
7. Create a Docker image out of the running container
8. Push created Docker image to Docker Hub
9. Create a directory with appropriate permissions to store Java artifacts
 
**[Ansible](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/ansible.md)**
1. Create a diretory for Ansible
2. Create an Ansible skeleton role
3. Move into Tomcat directory create a hosts directory
4. Create a hosts file in hosts directory with contents of this [file](https://github.com/hadriane/cicd_pipeline_java/blob/master/ansible_roles/hosts)
5. Create an Ansible Playbook named docker-container.yml with contents of this [file](https://github.com/hadriane/cicd_pipeline_java/blob/master/ansible_roles/docker-container.yml)
6. Give ansible folder and its contents the appropriate owners

**[Jenkins](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/jenkins.md)**
1. 
