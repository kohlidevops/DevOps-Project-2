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

**To create a Terraform file to create an EC2 instance**

```
https://github.com/kohlidevops/devops-workshop/blob/main/terraform_code/V1-EC2.tf
```
To execute the below commands to run the terraform file
```
sudo terraform init
sudo terraform validate
sudo terraform plan
sudo terraform apply
```
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/71ed5d6f-5801-4d41-ac9a-cecc049aa4b7)

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/ebbc5df0-24cb-4b5d-9628-96c98ff755e4)

Instance has been created.
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/9e103800-3f3e-4487-babe-0a42c7e0d471)

Then destroy this resource

```
sudo terraform destroy
```
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/25fff9fc-f2b2-4971-8bc3-f07765b51624)

**To create an EC2 instance along with security group using terraform**

Before, Remove the files V1-EC2.tf, terraform.tfstate and terraform.tfstate.backup (We have to create and run another terraform file)

create a file called V2-EC2.tf

```
https://github.com/kohlidevops/devops-workshop/blob/main/terraform_code/V2-EC2.tf
```
Now run the terraform command to launch instance

```
sudo terraform init
sudo terraform validate
sudo terraform plan
sudo terraform apply
sudo terraform destroy
```

**To create a VPC with Multiple EC2 instances - Jenkins, Build-Slave, and Ansible**

```
https://github.com/kohlidevops/devops-workshop/blob/main/terraform_code/V4-EC2-With_VPC_for_each.tf
```

Now run the terraform commands to launch VPC and EC2 instances


```
sudo terraform init
sudo terraform validate
sudo terraform plan
sudo terraform apply
```
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/029539c3-aa62-4e49-b684-75c96afd3a83)

**To Setup Ansible**

SSH to ansible machine and install Ansible then create a host file

```
sudo -i
https://github.com/kohlidevops/devops-workshop/blob/main/lab-docs/L6-Ansible_setup.md
```

**To copy paste a private key file of Jenkins and Build slave machine**

```
cd /opt
sudo nano devopstep1.pem
//copy paste the key content
```

**To create a hosts file**

```
cd /opt
sudo nano hosts
//add the below content

[jenkins-master]
10.1.1.227

[jenkins-master:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/opt/devopstep1.pem

[jenkins-slave]
10.1.1.234

[jenkins-slave:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/opt/devopstep1.pem
```
![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/7dc84dcf-bef5-4866-83e2-6e8218ca94a2)

**To create a jenkins master setup file in ansible machine**

```
cd /opt
https://github.com/kohlidevops/devops-workshop/blob/main/Ansible/jenkins-master-setup.yaml
ansible-playbook -i /opt/hosts jenkins-master-setup.yaml --check
ansible-playbook -i /opt/hosts jenkins-master-setup.yaml
```
After installation, access the Jenkins webUI using IP address of the Jenkins master and login then install suggessted plugins.

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/4c11aad6-182c-4679-9a4f-7e18cdf6d6a0)

**To create a jenkins slave setup file in ansible machine**

```
cd /opt
https://github.com/kohlidevops/devops-workshop/blob/main/Ansible/v1-jenkins-slave-setup.yaml
ansible-playbook -i /opt/hosts v1-jenkins-slave-setup.yaml --check
ansible-playbook -i /opt/hosts v1-jenkins-slave-setup.yaml
```

After installation, SSH to build slave machine and check the maven version

```
sudo -i
cd opt/apache-maven-3.9.4/bin/
./mvn --version
```

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/1aba3407-86e3-4ccb-bdc5-2792589d4dba)

**To Setup Jenkins Master Slave configuration in Jenkins**

```
https://github.com/kohlidevops/devops-workshop/blob/main/lab-docs/L7-Jenkins_master_and_slave_setup.md
```

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/791dd0fa-569d-4c70-b545-5c7400b8cf74)

You can check the maven slave logs thorugh - maven slave node - select - logs

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/ffa0df46-326f-42de-9f17-2ab24c120ceb)

If you ssh to maven build slave machine then you can see the jenkins directory under /home/ubuntu/

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/a4c8a0d7-5588-4e9f-affe-964c45f15ff8)

I can test the free style project

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/b45b5121-4d1f-45ed-a73f-ee73f37be345)

In build steps - execute shell

```
echo "Hello! I'm a Slave System" >> /home/ubuntu/maven.txt
```

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/eb78d430-f9aa-4173-bd4f-561779cd64eb)

Then save and apply -> build the test job

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/6bf87b0d-84fc-491b-85c1-9440f2d975cf)

**To create a first Jenkinsfile job**

Create a new pipeline job and use below Jenkinsfile

Pipeline - Definition - Pipeline script

```
pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/kohlidevops/tweet-trend-new.git'
            }
        }
    }
}
```
Then save and apply -> To run the build

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/af4eb2fa-8586-4d48-84ce-1024385995c4)

If you can ssh to maven build slave machine, you can see the workspace folder

![image](https://github.com/kohlidevops/DevOps-Project-2/assets/100069489/f331156f-2833-4070-81b5-2e51896b9989)



