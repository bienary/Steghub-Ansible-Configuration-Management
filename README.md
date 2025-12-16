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

> Test setup by making some change in README.md file in master branch and make sure that builds starts automatically.

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/29c8cf0a-1b6d-493c-beb6-1e6d39e0f9d2" />

<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/b076b76f-b21d-4c32-9845-6f2a7d5cd104" />


> Jenkins saves the files (build artifacts) in following folder.

```
ls /var/lib/jenkins/jobs/Ansible/builds/<build_number>/archive/
```
### Note: The Ansible name configuration on Jenkins is case sensitive.

<img width="1325" height="152" alt="image" src="https://github.com/user-attachments/assets/6627f803-2097-4eb0-8fde-5a6586a07370" />

### Allocate an Elastic IP to your Jenkins-Ansible server to maintain a consistent IP address for your GitHub webhook configuration.

<img width="1165" height="483" alt="image" src="https://github.com/user-attachments/assets/f794830b-03d6-4211-904c-366e73d2ed7f" />

## Prepare your development environment using Visual Studio Code.

- Install Visual Studio Code

> Download and install Visual Studio Code as your integrated Development Environment(IDE)

- Configure VS Code for GitHub

> Connect VS Code to your newly created GitHub repository:

- Clone down your ansible-config-mgt repo to your Jenkins-Ansible instance.

<img width="1319" height="217" alt="image" src="https://github.com/user-attachments/assets/a8a28c7c-02bb-4772-8aab-c945df6a17bf" />

## Ansible Development:

- Create Feature Branch

- Create a new branch for Development

```
git checkout -b feature/project-11-ansible-config
```

<img width="1313" height="469" alt="image" src="https://github.com/user-attachments/assets/6a2a2ee2-59a4-4f3e-9057-66d871120d44" />

- Create a directory and name it playbooks.

```
mkdir playbooks
```

- Create a directory and name it inventory.

```
mkdir inventory
```

<img width="1012" height="197" alt="image" src="https://github.com/user-attachments/assets/2c3bff35-0d9c-4c7c-83b4-ed8cd13f98f5" />

- Within the playbooks folder, create first playbook, and name it common.yml

<img width="945" height="100" alt="image" src="https://github.com/user-attachments/assets/000b1538-090e-42bd-96ee-cd043e9c70b0" />

- Create the initial inventory files (Development, Staging Testing and Production) dev, staging, uat, and prod respectively.

<img width="1072" height="264" alt="image" src="https://github.com/user-attachments/assets/adcc199c-0e3b-4355-8a90-550bb73eb780" />


## Ansible Inventory Setup

Within this project, the Ansible inventory file specifies the hosts and host groups targeted by playbooks, roles, and tasks. The inventory is organized by environment to ensure clear infrastructure separation, improve maintainability, and enable environment-specific automation workflows.

> Ansible uses SSH to connect to target servers. Set up SSH agent to manage your SSH keys & Confirm the key has been added with the command below:

```
eval `ssh-agent -s`
ssh-add <path-to-private-key>
ssh-add -l
```

<img width="1118" height="213" alt="image" src="https://github.com/user-attachments/assets/6e2a10c7-cd6f-4936-b9a2-065c064b904c" />

- Now, ssh into Jenkins-Ansible server using ssh-agent

```
ssh -A ubuntu@public-ip
```

<img width="1120" height="739" alt="image" src="https://github.com/user-attachments/assets/df3647d1-38f1-439d-b7d8-9b8a35660138" />

## Update Inventory File

```
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user=ec2-user

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user=ec2-user
<Web-Server2-Private-IP-Address> ansible_ssh_user=ec2-user

[db]
<Database-Private-IP-Address> ansible_ssh_user=ec2-user

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user=ubuntu
```




