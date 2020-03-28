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


## Infrastructure Design
![Infrastructure Design](https://github.com/hadriane/cicd_pipeline_java/blob/master/images/Infrastructure_Design.png)


### Overview

Prepare the underlining infrastructure

1. AWS
    1. Launch AWS EC2 instances
    2. Give each AWS EC2 instance a pulblic ip address
    2. Configure Security Groups for the AWS EC2 instances
2. OS
    1. Create users
    2. Add uses to necessary groups
    3. Give sudo privalages where necessary
    4. Genetate SSH keys for users
    5. Copy SSH keys over to necessary servers
    6. Enable yum repositories
    7. Install packages
3. Github
    1. Create a Github account
    2. Copy SSH key from Jenkins server to Github
    2. Fork "helloworld" repo
4. Docker Hub
    1. Create a Access Tokens
    2. Create a repository
    3. Clone Docker image
5. Install software and plugins
    1. Jenkins host
        1. Install Jenkins
        2. Install Maven
        3. Install plugins
    2. Ansible host
        1. Install Ansible
    3. Docker host
        1. Install Docker
 
