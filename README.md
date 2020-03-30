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

**[AWS](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/steps_aws.md)**
1. Create Security Groups
2. Launch AWS EC2 instances
3. Allocate each AWS EC2 instance a pulblic ip address

**[OS](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/steps_os.md)**
1. Change server hostname and SSH timeout for all servers
2. Create users
3. Add uses to necessary groups
4. Grant sudo access to ansibleadm user
5. Genetate SSH keys for users
6. Copy SSH keys over to necessary servers
7. Enable yum repositories
8. Install packages

**[Github](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/steps_github.md)**
1. Get jenkinsadm SSH key from Jenkins server to Github
2. Copy jenkinsadm SSH key from Jenkins server to Github
3. Fork "helloworld" repo

**[Docker Hub](https://github.com/hadriane/cicd_pipeline_java/blob/master/steps/steps_dockerhub.md)**
1. Create a Access Tokens
2. Create a repository
3. Clone Docker image

 
