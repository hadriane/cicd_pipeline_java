### Jenkins

1. Login to jenkins
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. Enter the password from step 7
    3. Do not install any plugins for the moment
    4. Click **Start using Jenkins**
    5. Change Jenkins password
        1. Click on the drop down arrow next to **admin** at the right
        2. Click **Configure**
        3. Change the **Password**
        4. Click **Save**
        5. Login again with the new password
        
2. Configure Maven plugin
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. On the left navigation bar click on **Manage Jenkins** >> **Manage Plugins** >> **Available tab**
    3. Search for "Maven" using the **Filter** on the top right
    4. Look for and tick the check box for **Maven Integration** & **Maven Invoker** from the search results
    5. Click on **Install without restart** on the bottom left
    6. On the left navigation bar click on **Manage Jenkins** >> **Global Tool Configuration**
    7. In the **Maven** section
        1. Click **Add Maven**
        2. Untick **Install automatically**
        3. Give **Name** as "M2_HOME"
        4. Give **MAVEN_HOME** as "/opt/maven"
        5. Click **Save**

3. Configuring Github plugin
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. On the left navigation bar click on **Manage Jenkins** >> **Manage Plugins** >> **Available** tab
    3. Search for "Github" using the **Filter** on the top right
    4. Look for and tick the check box for "Github" from the search results
    5. Click on **Install without restart** on the bottom left
    6. On the left navigation bar click on **Manage Jenkins** >> **Global Tool Configuration**
    7. In the **Git** section, change **Name** from "Default" to "Github"
    8. Click **Save**

4. Configuring Github webhook trigger
    1. On Jenkins
        1. Go to http://<public_ip_of_jenkins_server>:8080
        2. Click on **Manage Jenkins** >> **Configure System**
        3. Scroll down to the **GitHub** section
        4. Click on **Advanced**
        5. Tick the checkbox **Specify another hook URL for GitHub configuration**
        6. Note down the URL. In my case it was "http://<public_ip_of_jenkins_server>:8080/github-webhook/"
        7. DO NOT click **Save**
    2. On Github
        1. Login to your Github account
        2. Navigate to your repository. In my case it was "helloworld"
        3. Click on **Settings**
        4. Click on **Webhooks**
        5. Click **Add webhook** then enter your Github password
        6. For **Payload URL** enter the URL you noted down earlier
        7. For **Content type** choose "application/json"
        8. For **Which events would you like to trigger this webhook?** choose "Just the push event."
        9. Click **Add webhook**

5. Configure Publish Over SSH plugin
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. On the left navigation bar click on Manage Jenkins >> Manage Plugins >> Available tab
    3. Search for "Publish Over SSH" using the Filter on the top right
    4. Look for and tick the check box for **Publish Over SSH** from the search results
    5. Click on **Install without restart** on the bottom left
    6. Go to http://<public_ip_of_jenkins_server>:8080
    7. Click on **Manage Jenkins** >> **Configure System**
    8. Scroll down to the **Publish over SSH** section
    > ***NOTE**: Repeat **Steps x -x** for Ansible host and Docker host 
    9. Click **Add**
    10. Give it a **Name** *Ex*: Ansible Host
    12. The **Hostname** shoud be the private IP address of the host
    13. The **Username** should be either "ansibleadm" or "dockeradm"
    > ***NOTE**: Do **Step x** only for Docker host 
    14. The **Remote Directory** should be "/tmp/java_artifacts"
    15. Click **Save**
