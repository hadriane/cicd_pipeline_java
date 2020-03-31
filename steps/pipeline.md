### Pipeline

Now that we have build and configured of CI/CD infrastructure, lets proceed to configure a pipeline.

1. Start a new project
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. Click **New Item**
    3. Fill in as you wish **Enter an item name**
    4. Click **Maven Project**
    5. Click **Ok**
2. Configure the project
    1. In the **Source Code Management** section
        1. Click **Git**
        2. **Repositories URL** enter git@github.com:<your_github_username>/helloworld.git
        3. Click **Add** for **Credentials**
        4. Select **Jenkins**
        5. For **Kind** select **SSH Username with private key**
        6. **Username** is "jenkinsadm"
        7. Click **Add**
    2. In **Build Triggers** section, tick the following
        - **Build whenever a SNAPSHOT dependency is built**
        - **GitHub hook trigger for GITScm polling**
    3. In the **Build** section
        1. Enter **Root POM** as "pom.xml"
        2. Enter **Goals and options** as "clean install package"
    4. In the **Post-build Actions** section
        1. Click **Add post-built action**
        2. Select **Send build artifacts over SSH**
        3. For **Name** select "Ansible Host"
        4. For **Source files** enter "**/*.war"
        5. For **Remote directory** enter "/tomcat-v1"
        6. Click **Add Server**
        7. For **Name** select "Ansible Host"
        8. For **Remote directory** enter "/tomcat"
        9. For **Exec command** enter "ansible-playbook -i /etc/ansible/docker/hosts/hosts /etc/ansible/docker/docker.yml"
        10. Click **Save**
        11. You will be redirected to Project page
3. Run the build manually
    1. Click **Build Now**
    2. Ensure the build is successful
    3. Open a web browser and go to http://<ip_address_of_docker_host>:8080/webapp
    4. Ensure you can see the webpage
4. Trigger an automatic build
    1. Login to your Github account
    2. Go to "https://github.com/<your_github_username>/helloworld/tree/master/webapp/src/main/webapp"
    3. Click on "index.jsp"
    4. Click on the **Pencil Icon** to edit the file
    5. Add the following HTML code at the bottom of the file
    ```
    <h2> End to end complete </h2>
    ```
    6. Click **Commit changes**
    7. Check the progress of the build in Jenkins
    8. Go to "http://<ip_address_of_docker_host>:8080/webapp" in a web browser and you will see the sentence "End to end complete" at the bottom
    
    
        
