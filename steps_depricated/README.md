## Building A CI/CD Pipeline Using AWS, Jenkins, Maven, Ansible, Docker and Sonarqube

### Purpose

The purpose of building a CI/CD pipeline is to get to know the tools used in CI/CD pipelines

### Tools

- Jenkins
- Maven
- Git
- Ansible
- Docker
- Docker Hub
- Sonarqube
- Tomcat

### Preliminaries

1. We would be installing the above tools on AWS EC2

2. Required EC2 Instances

| Server  | Instance Type | Elastic IP | Open Port(s) |
|---------|---------------|------------|--------------|
| Jenkins | t2.medium     | Yes        | 22,8080      |
| Tomcat  | t2.micro      | Yes        | 22,8080      |
| Ansible | t2.micro      | Yes        | 22           |
    
### Overview of Steps

> ***Note**: Click on each step to go to their individual readme's*

1. [Change server hostname and SSH timeout for all servers](https://github.com/hadriane/cicd_pipeline/blob/master/ChangeHostnameAndSSHTimeout.md)
2. [Installing and Configuring Jenkins](https://github.com/hadriane/cicd_pipeline/blob/master/InstallingJenkins.md)
    1. Install Java 1.8
    2. Find Java executable and take the last entry
    3. Set Java environment variable
    4. Enable Jenkins repo
    5. Install Jenkins
    6. Enable and start Jenkins
    7. Get the initial Jenkins password
    8. Login to Jenkins
3. [Installing and Configuring Git on Jenkins server](https://github.com/hadriane/cicd_pipeline/blob/master/InstallingGitOnJenkins.md)
    1. Install Git
    2. Configure Git plugin on Jenkins server
4. [Installing and Configuring Maven on Jenkins server](https://github.com/hadriane/cicd_pipeline/blob/master/InstallingMavenOnJenkins.md)
    1. Installing Maven
    2. Set Maven environment variable
    3. Configure Maven plugin on Jenkins server
5. [Installing Tomcat](https://github.com/hadriane/cicd_pipeline/blob/master/InstallingTomcat.md)
    1. Change server hostname and SSH timeout
    2. Install wget
    3. Install Java 1.8
    4. Find Java executable and take the last entry
    5. Set Java environment variable
    6. Downalod Tomcat
    7. Start Tomcat
    8. Allow access to Tomcat Manager App & Host Manager
    9. Update Tomcat users information
    10. Restart Tomcat server
    11. Login to Tomcat
5. [Installing Docker](https://github.com/hadriane/cicd_pipeline/edit/master/InstallingDocker.md)
    1. Change server hostname and SSH timeout 
    2. Install Docker
    3. Pull docker image Tomcat 8.5
    4. Run a docker container using Tomcat 8.5 image
    5. Test if Docker Tomcat 8.5 container works
6. [Installing Ansible](https://github.com/hadriane/cicd_pipeline/edit/master/InstallingAnsible.md)
    1. Change server hostname and SSH timeout
    2. 

