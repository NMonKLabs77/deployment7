# Deployment7:- Demonstrating my ability to create a DockerFile, create infrastructure with Terraform and Deploy to DockerHub

Date: 4/11/2023

Done by: Nehemiah Monrose

## Table of Contents
- [Purpose](#purpose)
- [Requirements](#requirements)
- [Steps](#steps)
- [Diagram](#diagram)


## Purpose
The purpose of this deployment is to demonstrate my ability to create a Dockerfile for my Banking Applicatiton, create an deploy an ECS infrastructure with Terraform.

## Requirements

<em><b>Instance 1:</b></em>
```
Jenkins
software-properties-common
add-apt-repository -y ppa:deadsnakes/ppa
python3.7
python3.7-venv
build-essential
libmysqlclient-dev
python3.7-dev
```

<em><b>Instance 2:</b></em>
```
Docker
default-jre
software-properties-common
add-apt-repository -y ppa:deadsnakes/ppa
python3.7
python3.7-venv
build-essential
libmysqlclient-dev
python3.7-dev
```

<em><b>Instance 3:</b></em>

```
Terraform
default-jre
Ensure you have Terraform installed on your local machine.
```
## Steps

Step 1: Banking App Dockerfile Setup

Created a Dockerfile for my Banking App that is connected to an RDS database called "mydatabase".
```
FROM python:3.7

RUN git clone https://github.com/NMonKLabs77/Deployment7.git

WORKDIR Deployment7

RUN pip install -r requirements.txt

RUN pip install gunicorn

RUN pip install mysqlclient

EXPOSE 8000

CMD [ "gunicorn", "--bind", "0.0.0.0", "app:app"]
```
<hr>

Step 2: Modify Terraform Resources

Modified the Terraform configuration files to update resource name tags and values as specified below:
```
main.tf:

Updated the #Cluster name with my desired cluster name.
Updated the #Task Definition: Family with the desired family name.
In the container_definitions section, provided values for:
name
image
containerPort
Updated execution_role_arn with the appropriate ARN.
Updated task_role_arn with the desired task role ARN.
Updated #ECS Service name with the name you prefer for my ECS service.
Provided values for container_name and container_port.
ALB.tf:

Updated the #Target Group name with my desired target group name.
Updated the port with the desired port number.
Updated the #Application Load Balancer name with my preferred name for the ALB.
```
<hr>

Step 3: Review VPC Configuration
Observed the VPC.tf file to ensure the following resources are being created:

```
2 Availability Zones (AZs)
2 Public Subnets
2 Private Subnets
1 NAT Gateway
2 Route Tables
Security Group Ports: 8000
Security Group Ports: 80
Step 5: Configure Terraform Resources
Observe the Terraform resources defined in main.tf and ALB.tf. Ensure that the following resources are created as intended:

aws_ecs_cluster
aws_cloudwatch_log_group
aws_ecs_task_definition
aws_ecs_service
aws_lb_target_group
aws_alb
aws_alb_listener
```
<hr>

Step 4: Jenkins Setup
```
Edit the Jenkinsfile:
Updated line 4 with my Docker Hub username.
Modified lines 31 and 42 with my image name.
Generated an Access Token from my DockerHub account.

In Jenkins, navigate to global credentials and enter my Docker Hub username and token. 

Installed the Docker Pipeline plugin on Jenkins.

Created a multibranch pipeline and ran the Jenkinsfile to build and deploy my application.
```

Step 5: Infrastructure and Security Assessment

After deploying my application and infrastructure, I assessed the security of my environment. I presume that the infrastructure is as secure enough for a small scale application.
<hr>

Step 6: Test Fault Tolerance
To test the fault tolerance of my infrastructure, I terminateD one of the instances created in Step 3.
<hr>

Step 7: Identify Container Subnets

Identified the subnets in which my containers were deployed. 

# Diagram

