# 🖥️ Project 3: EC2 Lab – Deploy an E-Commerce Web Server (GUI Mode)

## 🎯 Goal

Deploy an **e-commerce platform (OpenCart)** on a **Linux EC2 instance** using the **AWS Management Console (GUI)**. This includes:

- Installing Apache, PHP, and OpenCart
- Configuring **secure storage** with EBS encryption
- Assigning an **Elastic IP** for consistent public access
- (Optional) Using **IAM roles** for S3 backups

---

## 🧱 Architecture Summary

| Layer      | Technology                     | Purpose                          |
|------------|--------------------------------|----------------------------------|
| Web        | EC2 (Amazon Linux 2 / Ubuntu)  | Run Apache and PHP               |
| App        | OpenCart                       | E-commerce platform              |
| Storage    | Encrypted EBS Volume           | Secure persistent data storage   |
| IP         | Elastic IP                     | Fixed public access              |
| Backup     | IAM Role + S3 (Optional)       | Backup data to Amazon S3         |

---

## 📘 Task-by-Task Guide

### ✅ Task 1: Launch EC2 Instance

1. **Go to EC2 Dashboard**:  
   EC2 > Instances > Launch Instance

2. **Configuration**:
   - Name: `OpenCart-Server`
   - AMI: Amazon Linux 2 / Ubuntu 20.04
   - Instance Type: `t2.micro` (Free Tier eligible)
   - Key Pair: Choose or create one
   - Network: Default VPC with auto-assign public IP
   - Security Group (`OpenCartSG`):
     - HTTP (Port 80) – Anywhere
     - SSH (Port 22) – Your IP only

3. **User Data Script**:
   ```bash
   #!/bin/bash
   yum update -y
   yum install -y httpd php php-mysqlnd wget unzip

   systemctl start httpd
   systemctl enable httpd

   cd /var/www/html
   wget https://github.com/opencart/opencart/releases/download/3.0.3.8/opencart-3.0.3.8.zip
   unzip opencart-3.0.3.8.zip
   cp -r upload/* .
   rm -rf upload opencart-3.0.3.8.zip

   chown -R apache:apache /var/www/html
   chmod -R 755 /var/www/html
   
Launching EC2 Instance
<img width="613" alt="Image" src="https://github.com/user-attachments/assets/6bb0b7a5-085a-46ed-858d-d66b8a9d4935" />

<img width="555" alt="Image" src="https://github.com/user-attachments/assets/29a4d74e-445f-4054-921b-fb6bc407245a" />

