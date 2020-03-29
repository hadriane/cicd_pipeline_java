### 1 - AWS

Instance Types

| Server  | Instance Type | Elastic IP | EBS Volume Size | Security Group Name / Tag | Open Port(s) |
|---------|---------------|:----------:|:---------------:|:-------------------------:|:------------:|
| Jenkins | t2.micro      |     Yes    |       8 GB      |       CICD - Jenkins      |    22,8080   |
| Ansible | t2.micro      |     Yes    |       8 GB      |       CICD - Ansible      |      22      |
| Docker  | t2.micro      |     Yes    |       8 GB      |       CICD - Docker       |    22,8080   |

1. Create Security Groups
    1. Login to your AWS console
    2. Navigate to **EC2 Dashboard**
    3. Click on **Security Groups** 
    4. Create 3 **Security Groups**
        1. Click **Create security group**
        2. Give the **Security group name** as described in the "Security Group Name / Tag" column in the table above 
        3. Open ports in **Outbound rules** as described in the "Open Port(s)" column in the table above
        3. Click **Create security group**

2. Allocate Elastic IP addresses
    1. Navigate back to **EC2 Dashboard*
    2. Allocate 3 Elastic IP addresses
        1. Click **Elastic IPs** then click **Allocate Elastic IP address**
        2. Select **Amazon's pool of IPv4 addresses** then click **Allocate**

3. Launch AWS EC2 instances
    1. Navigate back to **EC2 Dashboard*
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
        2. **Name**: as described in the "Security Group Name / Tag" column in the table above 
    10. Click **Next: Configure Security Group**
    11. Select the Security Group **Name** matching the server you are creating now
    12. Click **Review and Launch**
    13. Click **Launch**
    14. Select **Create a new key pair**
    15. Give it a **Key pair name**
    16. Click **Download Key Pair** asn save the file in a secure place
    17. Click **Launch Instances**
    18. Repeat the above steps for the other 2 servers
