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

## Technologies Used

- Configuration Management: Ansible

- CI/CD: Jenkins

- Cloud Platform: AWS (EC2, Elastic IP)

- Version Control: Git & GitHub

- OS: Ubuntu Linux

- IDE: Visual Studio Code

## Step 1 - Install and Configure Ansible on EC2 Instance.

Update the Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.

<img width="1138" height="97" alt="image" src="https://github.com/user-attachments/assets/33daa769-a999-499a-b587-8471a9febb66" />


### Github Repository Creation
- Create a new repository named ansible-config-mgt in your GitHub account.

### Ansible Installation
- Install Ansible on the jenkins-ansible server:

```
sudo apt update
sudo apt install ansible -y
```

<img width="1321" height="539" alt="image" src="https://github.com/user-attachments/assets/8fa52da0-e4ef-41ad-a08d-1986c15d753d" />

- Check your Ansible version by running
```
ansible --version
```

<img width="1322" height="267" alt="image" src="https://github.com/user-attachments/assets/46844fb5-aeb8-45d4-910e-20d4f0c200a1" />

### Jenkins Job Configuration
Configure Jenkins build job to save repository content every time you change it automatically: 

### Set up a webhook in Github:
Go to your ansible-config-mgt repository
Navigate to Settings > Webhooks > Add webhook

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/66378e16-2760-44cf-aadf-0e31d5f14bf6" />

## Create a new Freestyle project in Jenkins named ansible:

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/7ae609ae-bc83-4162-8dbc-d7c00ad024c2" />

### Configure Source Code Management:

- Choose Git
- Provide the ansible-config-mgt repository URL
- Add credentials for Jenkins to access the repository

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/a17d022e-5c67-46c4-9543-2d095086726a" />

### Configure Build Triggers:

- Select "GitHub hook trigger for GITScm polling"

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/e2287839-59a4-4eb7-86fb-80d297ec5a1b" />

### Configure Post-build Actions:
- Click `Add post-build action`
- Click `Archive the artifacts`
- Files to archive: **

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/2d582bba-5c68-46c2-a339-780bccf54b32" />
