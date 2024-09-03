# Host a Static Website on AWS - Project README

## Overview
This project demonstrates how to host a static HTML website on AWS, leveraging various AWS services to create a scalable, secure, and fault-tolerant infrastructure. The website is deployed on an EC2 instance within a Virtual Private Cloud (VPC) with multiple subnets, security groups, and an Auto Scaling Group to manage the EC2 instances. The entire process, including the infrastructure setup and deployment scripts, is documented and available in the accompanying GitHub repository.

## Project Architecture
The project architecture includes the following key components:

1. **Virtual Private Cloud (VPC):**
   - Configured with both public and private subnets spread across two different Availability Zones to ensure high availability and fault tolerance.

2. **Internet Gateway:**
   - Deployed to facilitate connectivity between instances within the VPC and the wider Internet.

3. **Security Groups:**
   - Established as a network firewall mechanism to control inbound and outbound traffic to the instances.

4. **Availability Zones:**
   - Leveraged two Availability Zones to enhance system reliability and ensure the website remains accessible even if one zone fails.

5. **Public Subnets:**
   - Used for infrastructure components like the NAT Gateway and Application Load Balancer (ALB).

6. **EC2 Instance Connect Endpoint:**
   - Implemented for secure connections to instances within both public and private subnets.

7. **Private Subnets:**
   - Web servers (EC2 instances) are positioned within Private Subnets to enhance security, preventing direct access from the Internet.

8. **NAT Gateway:**
   - Enabled instances in private subnets to access the Internet for updates and other necessary communications without exposing them directly to the Internet.

9. **Application Load Balancer (ALB):**
   - Used in conjunction with a target group to evenly distribute incoming web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.

10. **Auto Scaling Group:**
    - Automatically manages EC2 instances to ensure the website is always available, scalable, fault-tolerant, and elastic.

11. **Certificate Manager:**
    - Secured application communications by using SSL/TLS certificates for the website.

12. **Simple Notification Service (SNS):**
    - Configured to send alerts about activities within the Auto Scaling Group, ensuring timely notifications for any changes in the infrastructure.

13. **Route 53:**
    - Domain name was registered and a DNS record was set up to point to the Application Load Balancer, ensuring proper routing of traffic to the website.

## Deployment Instructions

To deploy the static website on AWS, follow the steps below:

1. **Clone the GitHub Repository:**
   - Clone the project repository to your local machine or directly to the EC2 instance.
   ```bash
   git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
   ```

2. **Connect to the EC2 Instance:**
   - Use SSH or EC2 Instance Connect to access your EC2 instance.

3. **Switch to the Root User:**
   - Gain full administrative privileges by switching to the root user.
   ```bash
   sudo su
   ```

4. **Update Installed Packages:**
   - Ensure all installed packages on the EC2 instance are up to date.
   ```bash
   yum update -y
   ```

5. **Install Apache HTTP Server:**
   - Install the Apache web server to serve the static website.
   ```bash
   yum install -y httpd
   ```

6. **Navigate to the Apache Web Root:**
   - Change the current working directory to the Apache web root directory.
   ```bash
   cd /var/www/html
   ```

7. **Install Git:**
   - Install Git to enable cloning of the repository.
   ```bash
   yum install git -y
   ```

8. **Clone the Repository to the EC2 Instance:**
   - Clone the project repository into the Apache web root directory.
   ```bash
   git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
   ```

9. **Copy Website Files:**
   - Copy all files from the cloned repository to the Apache web root, including hidden files.
   ```bash
   cp -R host-a-static-website-on-aws/. /var/www/html/
   ```

10. **Clean Up:**
    - Remove the cloned repository directory to clean up unnecessary files.
    ```bash
    rm -rf host-a-static-website-on-aws
    ```

11. **Enable and Start Apache:**
    - Configure Apache to start automatically at system boot and start the Apache server to serve the website.
    ```bash
    systemctl enable httpd
    systemctl start httpd
    ```

## Additional Resources
- **AWS Documentation:** Refer to the official [AWS Documentation](https://docs.aws.amazon.com/) for detailed guidance on using AWS services.
- **GitHub Repository:** All scripts and reference diagrams used in this project are available in the [GitHub repository](https://github.com/aosnotes77/host-a-static-website-on-aws).

## Conclusion
This project demonstrates the deployment of a static website on AWS using a highly available, scalable, and secure architecture. The use of multiple AWS services ensures that the website remains accessible, even under varying load conditions, and is protected from common security threats. The provided scripts and setup instructions allow for easy replication and customization of this deployment in different environments.
