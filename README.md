# Ansible Configuration Management with Jenkins

## Project Description
This project focuses on automating infrastructure configuration tasks previously performed manually by implementing **Ansible Configuration Management**. It builds on earlier projects by introducing automation, version control, and CI/CD integration using **Jenkins**, **GitHub**, and **AWS**.

The solution demonstrates how to manage multiple environments efficiently while applying DevOps best practices such as Infrastructure as Code (IaC), secure access patterns, and continuous integration.

---

## Learning Objectives
By completing this project, the following skills were demonstrated:

- Understanding Ansible architecture and use cases
- Automating server configuration using Ansible playbooks
- Managing multiple environments with Ansible inventories
- Integrating Ansible with Jenkins for CI/CD automation
- Implementing secure access using a Jump Server (Bastion Host)
- Using GitHub webhooks to trigger automated jobs

---

## Project Architecture
The architecture consists of a centralized Ansible control node and multiple target servers located in a private network.

- **Jenkins-Ansible Server**
  - Acts as the Ansible control node
  - Runs Jenkins jobs to trigger Ansible playbooks
- **Jump Server (Bastion Host)**
  - Provides secure SSH access to private servers
- **Web Servers**
  - Deployed in a private subnet
  - Managed exclusively via Ansible
- **GitHub Repository**
  - Stores Ansible configurations
  - Triggers Jenkins builds via webhooks

📸 **Architecture Diagram**
```md
![Architecture Diagram](screenshots/architecture.png)



