# Setup DevOps Project using Maven, Terraform, Jenkins, SonarQube, JFrog Artifactory, Ansible, Docker, Kubernetes, Helm, and Prometheus

**Tools I have used**
```
GitHub
Jenkins
Terraform
Ansible
Maven
SonarQube
Jfrog
Docker
Kubernetes
Helm Charts
Prometheus
Grafana
```
**Steps to perform during this CICD pipeline project**
```
Set up Terraform
Provision Jenkins master, build Node and Ansible using Terraform.
Set up Ansible server.
Configure Jenkins master and build node using Ansible.
Create a Jenkins pipeline job
Create a Jenkins file from scratch.
Create Multi-branch pipeline
CICD Project Workshop 2
Enable webhook on GitHub.
Configuring Sonar Cube and Sonar Scanner.
Execute Sonar Cube analysis.
Define rules and gates on Sonar Cube.
Sonar callback rules.
Jfrog Artifactory Setup.
Create a Docker file
Store Docker Images on Jfrog Artifactory.
Provisioned Kubernetes cluster using Terraform.
Create Kubernetes Objects.
Deploying the Kubernetes objects using Helm.
Set up Prometheus and Grafana using Helm Charts.
Monitor Kubernetes Cluster using Prometheus
```

## Install Git, Terraform AWS CLI on Local machine or EC2 Instance

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/2919e392-2ec8-44ec-9062-d3ecdf17e9c9)

**Install Terraform on ubuntu22 Base instance**

```
https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
```
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/e5e93ffc-f22f-4b32-bfd2-548a9f47f51c)

**Install AWS CLI on ubuntu22 base instance**

```
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
```
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/73399400-eb3d-4533-b71b-a50335203454)

**Configure AWS CLI**

Create one IAM user and attach Administrator policy then create accesskey and secretkey

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/48a3cd3c-b68e-4794-8762-e359c61124d3)

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/00793277-3904-4944-9337-4701aec0c56b)


