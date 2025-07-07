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

<img width="339" alt="Image" src="https://github.com/user-attachments/assets/ef675430-24a5-4b20-baad-1208a106b8d4" />

<img width="539" alt="Image" src="https://github.com/user-attachments/assets/cb815195-7f4a-4c95-9280-8ec195c8dfbc" />

<img width="540" alt="Image" src="https://github.com/user-attachments/assets/8fdb6a7f-b553-4dc3-a428-7019fdc2b0e8" />

<img width="554" alt="Image" src="https://github.com/user-attachments/assets/b37c6585-0044-41ca-a9e3-1b9e9929654d" />

<img width="845" alt="Image" src="https://github.com/user-attachments/assets/a756ef18-a422-40ff-8d68-dfa5eb578791" />

<img width="647" alt="Image" src="https://github.com/user-attachments/assets/bacd108c-3feb-411a-831d-f4b0d15551f5" />

<img width="578" alt="Image" src="https://github.com/user-attachments/assets/20a93ad9-a113-40e5-9281-ebaaf64b05b9" />

<img width="959" alt="Image" src="https://github.com/user-attachments/assets/b9eb8dda-4b41-4831-9f0b-aba3a137ff97" />

<img width="973" alt="Image" src="https://github.com/user-attachments/assets/f0c717e5-da84-4cd6-8670-28a4e672cc35" />

<img width="527" alt="Image" src="https://github.com/user-attachments/assets/2cf3c019-de0b-4449-a526-cbd1ca342e0c" />

<img width="844" alt="Image" src="https://github.com/user-attachments/assets/2f893948-4e30-459d-8ba7-6aa24c6f4c76" />

<img width="771" alt="Image" src="https://github.com/user-attachments/assets/032be15e-be3d-431c-81d0-9017038e18bb" />

<img width="959" alt="Image" src="https://github.com/user-attachments/assets/1d531d3a-07a2-4c12-aeb7-9c46dd3ca928" />

<img width="848" alt="Image" src="https://github.com/user-attachments/assets/06017d92-17cf-4fb9-a040-da6105c64558" />

<img width="398" alt="Image" src="https://github.com/user-attachments/assets/f83824f7-b439-4800-ae8c-b85d1adc8540" />

<img width="482" alt="Image" src="https://github.com/user-attachments/assets/7add3201-baa7-4c1d-be0b-c96fd9a0bbca" />

<img width="419" alt="Image" src="https://github.com/user-attachments/assets/6d7ea034-1389-4019-bd7e-577eac7f3688" />

<img width="967" alt="Image" src="https://github.com/user-attachments/assets/566e68c8-700b-4ab4-a95a-9c8868eeeef4" />

<img width="953" alt="Image" src="https://github.com/user-attachments/assets/b08cee07-1e61-48b2-9218-abde5545a9ad" />
