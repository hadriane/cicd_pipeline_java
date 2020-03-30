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
