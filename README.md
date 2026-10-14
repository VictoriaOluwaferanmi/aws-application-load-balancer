# AWS EC2 Load Balancing Demo

## Overview

This project demonstrates the deployment of a highly available web application architecture using two Amazon EC2 instances behind an AWS Application Load Balancer (ALB).

Apache was configured on both web servers, and the load balancer was set up to distribute incoming HTTP traffic across registered instances through a target group.

The project focuses on load balancing, health checks, network access control, and troubleshooting connectivity between AWS resources.

## Architecture

User Browser → Internet → Application Load Balancer → Target Group → EC2 Web Server 1 / EC2 Web Server 2

## Technologies Used

- Amazon EC2
- AWS Application Load Balancer
- Target Groups and Health Checks
- AWS Security Groups
- Ubuntu Linux
- Apache HTTP Server

## Infrastructure Components

### 1. EC2 Web Servers

Deployed two EC2 instances running Ubuntu Linux and configured Apache to serve web content.

Each server was configured with a distinct response to help identify which instance handled incoming requests.

### 2. Application Load Balancer

Created an internet-facing Application Load Balancer to receive incoming HTTP requests and forward them to the registered web servers.

### 3. Target Group

Configured a target group using HTTP on port 80, registered both EC2 instances, and configured health checks to monitor their availability.

### 4. Security Groups

Configured security group rules to control traffic between the load balancer and web servers.

- Allowed HTTP traffic to the load balancer on port 80.
- Allowed HTTP traffic to the web servers from the load balancer's security group.
- Restricted SSH access to an authorised administrative IP address.

## Deployment and Configuration

Installed Apache on both EC2 instances:

```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable --now apache2
```

Verified the Apache service locally:

```bash
curl http://localhost
```

Configured each server to return a distinct web page, allowing requests to be traced to the responding instance.

## Testing and Validation

The deployment was tested by accessing the Application Load Balancer's DNS name through a web browser.

Validation included:

- Confirming that the Apache web servers were running.
- Checking target group health status.
- Testing HTTP access through the load balancer.
- Troubleshooting security group rules when connectivity issues occurred.

Because load balancing does not guarantee that each successive request reaches a different server, repeated requests and server-specific responses can help demonstrate traffic distribution.

## Challenges and Resolution

During configuration, connectivity issues occurred between the load balancer and the EC2 instances.

The issue was traced to security group configuration. Reviewing and correcting the rules helped establish the required communication between the load balancer and the web servers.

## Author

**Victoria Oluwaferanmi**

Cloud Engineering | AWS | Linux | Networking | Automation

[GitHub Profile](https://github.com/VictoriaOluwaferanmi)