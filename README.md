# aws-ecc2-tomcat-server
Step by step deployment of an Apache Tomcat10 web server on AWS EC2 (Amazon Linux 2023) with Java 17 and custom security group configurations.

## Project Overview
This project demonstrates cloud infrastructure management, remote Linux administration, networking setup, and web application deployment.

**Key Objectives**
- Provision an AWS EC2 instance (Amazon Linux 2023).
- Configure AWS Security Group inbound network access rules (SSH, HTTP, Custom TCP).
- SSH into the cloud instance, update system dependencies, and install Java OpenJDK 17.
- Validate live web access via the public IPv4 address on port 8080.

## 1. EC2 Instance Provisioning
- **OS:** Amazon Linux 2023 AMI
- **Instance Type:** 't3.micro' (AWS Free Tier)
- **Key Pair:** RSA SSH key configuration ('tomcat-key.pem')
  <img width="1453" height="729" alt="EC2 Instance" src="https://github.com/user-attachments/assets/7feefa98-816f-4dfd-8a72-78fa916d99c0" />

## 2. Network & Security Configuration
Configured AWS Inbound Security Group Rules to allow necessary incoming traffic:
- **SSH (Port 22):** Restricted to `My IP` for secure admin access.
- **HTTP (Port 80):** Open to `0.0.0.0/0` for public web traffic.
- **Custom TCP (Port 8080):** Open to `0.0.0.0/0` for direct Tomcat application verification.
<img width="1427" height="734" alt="Security Groups" src="https://github.com/user-attachments/assets/9c560db4-a59c-4c63-bbe8-be1e995de1ed" />

## 3. System Configuration & Installation

### Environment Setup
```bash
# Update System Packages
sudo dnf update -y

# Install Java OpenJDK 17 (Amazon Corretto)
sudo dnf install java-17-amazon-corretto -y

# Verify Java Installation
java -version

# Download Apache Tomcat archive
wget [https://archive.apache.org/dist/tomcat/tomcat-10/v10.1.20/bin/apache-tomcat-10.1.20.tar.gz](https://archive.apache.org/dist/tomcat/tomcat-10/v10.1.20/bin/apache-tomcat-10.1.20.tar.gz)

# Extract Archive
tar -xvzf apache-tomcat-10.1.20.tar.gz

# Navigate to Tomcat Directory & Start Service
cd apache-tomcat-10.1.20
./bin/startup.sh 
```
<img width="1446" height="755" alt="Terminal Installation" src="https://github.com/user-attachments/assets/13abfafa-9270-4791-aef2-3bacd0bc4524" />

## 4. Live Deployment Verification
Successfully verified the active web deployment by accessing http://<EC2-Public-IP>:8080 in a web browser.
<img width="1456" height="729" alt="Tomcat Deployment" src="https://github.com/user-attachments/assets/365ce0af-52e2-4f1d-ab69-c90463563a6c" />

