### Github

1. Get jenkinsadm SSH key from Jenkins host
    1. Copy the contents of the public key (except for the "jenkinsadm@jenkins" part at the end)
    ```
    [jenkinsadm@jenkins root]$ cd /home/gituser/.ssh/
    [jenkinsadm@jenkins .ssh]$ cat id_rsa.pub
    ssh-rsa XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/gPcTH32rPdR+c7OWTlJz5Xxu3NhilVAf8tt1tazzuwocdhN9CukhkoH3S2H5CVUstAUInHpf6UOR6y0w40JJgo8eF4X4FUDAZLnnGXuCOHagoWkwDB5yNuqnWyn9QwhiCspiLinVLtAHNWqS1UoJ5QsODOGv8E+pqDgZOL9KD2ZvP1nKmu9fqp2Dae1UkaHqXzBtPEVQiHNfu1kRBEGzRd/6d3XHpkkousv8z/QxwP4Disawvis7XkPnRxbB8NKzGMsH9lBT6sonQo56tW1p jenkinsadm@jenkins
    ```
2. Copy jenkinsadm SSH key from Jenkins host to Github
    1. Log into Github
    2. Click the **drop-down arrow** next to your Avatar on the top right
    3. Click **Settings**
    4. Click **SSH and GPG keys**
    5. Click **New SSH key**
    6. Give it a **Title** *Ex*: jenkinsadm
    7. Paste the SSH public key copied earlier into the **Key** box
    8. Click **Add SSH key**
3. Fork "helloworld" repository from my Github account to your account
    1. Go to https://github.com/hadriane/helloworld
    2. Click **Fork** on the top right
    3. The forked "helloworld" repository should now be at this URL https://github.com/<your_github_username>/helloworld
