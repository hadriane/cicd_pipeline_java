### AWS


Instance Types

- AMI ID : ami-0affd4508a5d2481b
- AMI Type : CentOS 7 (x86_64) - with Updates HVM

| Server  | Instance Type | Elastic IP | EBS Volume Size | Security Group Name / Tag | Open Port(s) |
|---------|---------------|:----------:|:---------------:|:-------------------------:|:------------:|
| Jenkins | t2.micro      |     Yes    |       8 GB      |       CICD - Jenkins      |    22,8080   |
| Ansible | t2.micro      |     Yes    |       8 GB      |       CICD - Ansible      |      22      |
| Docker  | t2.micro      |     Yes    |       8 GB      |       CICD - Docker       |    22,8080   |


1. Create Security Groups
    1. Login to your AWS console
    2. Navigate to **EC2 Dashboard**
    3. Click on **Security Groups** 
    > ***NOTE**: Repeat **Steps iv - vii** to create the other 2 Security Groups*
    4. Click **Create security group**
    5. Give the **Security group name** as described in the "Security Group Name / Tag" column in the table above 
    6. Open ports in **Outbound rules** as described in the "Open Port(s)" column in the table above
    7. Click **Create security group**

3. Launch AWS EC2 instances
    1. Navigate back to **EC2 Dashboard**
    > ***NOTE**: Repeat **Steps ii - xviii** to create the other 2 hosts*
    2. Click on **Instances** >> **Launch Instance**
    3. Search "Centos" then click on **AWS Marketplace**
    4. Click **Select** on the top most results then click **Continue**
    5. Select **t2.micro** then click **Next: Configure Instance Details**
    6. Modify the values for **Configure Instance Details** as below
        1. **Number of instances**: 1
        2. **Subnet**: Public Subnet
        3. **Auto-assign Public IP**: Enable
        4. Leave the rest of the options at its default values
    7. Click **Next: Add Storage**
    8. Modify the values for **Add Storage** as below
        1. **Size (GiB)**: 8
        2. **Delete on Termination**: Ticked
        3. Leave the rest of the options at its default values
    9. Click **Next: Add Tags** then **Add Tag**
    10. Modify the values for **Add Tags** as below
        1. **Key**: "Name" 
        2. **Value**: as described in the "Security Group Name / Tag" column in the table above 
    10. Click **Next: Configure Security Group**
    11. Select the Security Group **Name** matching the server you are creating now
    12. Click **Review and Launch**
    13. Click **Launch**
    14. Select **Create a new key pair**
    15. Give it a **Key pair name**
    16. Click **Download Key Pair** asn save the file in a secure place
    17. Click **Launch Instances**

3. Allocate each AWS EC2 instance a pulblic ip address
    1. Navigate back to **EC2 Dashboard*
    > ***NOTE**: Repeat **Steps ii - iv** to associate the balance 2 Elastic IP addresses with the balance 2 EC2 instances*
    2. Allocate an Elastic IP addresses
        1. Click **Elastic IPs** then click **Allocate Elastic IP address**
        2. Select **Amazon's pool of IPv4 addresses** then click **Allocate**
    3. Tag the Elastic IP address
        1. Tick the newly tagged Elastic IP address
        2. Click **Tags** then click **Manage tags**
        3. Modify the values for **Manage tags** as below
            1. **Key**: "Name" 
            2. **Value**: as described in the "Security Group Name / Tag" column in the table above
            3. Click **Save**
    4. Assign the allocated Elastic IP address to an EC2 instance
        1. Tick the newly tagged Elastic IP address
        2. Click **Actions** then click **Associate Elastic IP address**
        3. Search the EC2 instance in **Instance**
        4. Select a **Private IP address**
        5. Click **Associate**
        
        
    
