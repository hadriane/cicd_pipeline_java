### 3 - Installing and Configuring Git on Jenkins server

1. Install Git
```
[root@jenkins ~]# yum install -y git
```

2. Configure Git plugin on Jenkins server
    1. Go to http://<public_ip_of_jenkins_server>:8080
    2. On the left navigation bar click on **Manage Jenkins** >> **Manage Plugins** >> **Available** tab
    3. Search for "Github" using the **Filter** on the top right
    4. Look for and tick the check box for "Github" from the search results
    5. Click on **Install without restart** on the bottom left
    6. On the left navigation bar click on **Manage Jenkins** >> **Global Tool Configuration**
    7. In the **Git** section
        1. Change **Name** from "Default" to "Github"
    
3. Configuring Github webhook trigger
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
    
