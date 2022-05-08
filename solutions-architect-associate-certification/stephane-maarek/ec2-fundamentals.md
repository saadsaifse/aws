## EC2 Fundamentals

### AWS Budget Setup

* Have to enable access to other IAM users (is off by default)
* Setting a budget will enable the Cost Explorer
* Alerts and actions can be set when budget is created

### EC2 Basics

* Most popular AWS offering
* Elastic Compute Cloud = Infrastructure as a Service
* Not just one service but composed of many services
  * Renting virtual machines (EC2)
  * Storing data on virtual drives (EBS)
  * Distributing load across machines (ELB)
  * Scaling the service using an auto-scaling group (ASG)
* OS can be Linux, Windows, MacOS
* CPU level?
* RAM?
* Storage?
  * Network attached (EBS, EFS)
  * Hardware (EC2 Instance store)
* Network card? 
  * speed of the card, public IP?
* Firewall rules? security group?
* Bootstrap script (EC2 user data)
  * Installing software, updating etc. or any startup commands
  * Runs as a root user and only once

### EC2 Instances Types

* Compute optimized starts with C
* Memory optimized starts with R (Ram)
* Storage optimized instances
* Instance type comparisons https://instances.vantage.sh/

### EC2 Security Groups and Classic Ports Overview

* Control how traffic is allowed into or out of EC2 instances
* Security groups only contain allow rules
* Security group rules can reference by IP or by security group
* Acting as firewall on EC2 instances
* They regulate
  * Access to ports
  * Authorised IP ranges 
  * Inbound/outbound traffic control 
* Locked down to region/VPC combination
* Live outside of EC2. Not an app in EC2
* Timeout error is received if security group is blocking it
* Connection refused is an EC2 level error
* Ports to know:
  * 22 = SSH
  * 21 = FTP
  * 22 = SFTP (Secure)
  * 80 = HTTP
  * 443 = HTTPS
  * 3389 = RDP (Remote desktop protocol)

### SSH to EC2
* SSH, Putty, EC2 Instance Connect (web based)
* The private key installed while setting up an EC2 instance has too open permissions (0644) that results in a warning and a permission denied error upon ssh
  * to fix `chmod 0400 <key-file.pem>`


### EC2 Instance Roles

* Never never ever enter your AWS creds in EC2 instance since anyone can connect to that EC2 instance and retrieve your `aws configure` credentials
* Instead assign an IAM role to the EC2 instance

### EC2 Instance Purchasing Options

* On-demand instances
* Reserved (1 & 3 years)
  * long workloads
  * convertible reserved instances (long workloads with flexible instances)
* Saving Plans (1 & 3 years) 
  * commitment to an amount of usage, long workload
* Spot instances
  * short workloads, cheap, can lose instances (less reliable)
* Dedicated hosts
  * book an entire physical server, control instance placement
  
### Spot Instances
* Get up to 90% discount
* Define the max spot price and get the instance while current sport price < max spot price
* You have 2 minutes grace period to stop or terminate it once the spot price increases every hour
* Spot blocks won't be supported after Dec 31, 2022 but that feature used to block the instance from 1 to 6 hours without interruptions
* Good for batch jobs, data analysis, workloads resilient to failures
* One time or persistent request for the spot instance
  * Persistent request gets the instance back until the valid until date while the one time instance will be lost after the first interruption
  * Cancelling a spot instance request doesn't terminate the spot instance
  * First cancel the spot request and then terminate the instances manually

### Spot Fleets

* Ultimate way to save money
* Set of spot instances and optionally on-demand instances
* Define multiple launch pools such as instance type, OS, AZ
* Fleet stop launching instances when reaching max cost
* Strategies:
  * lowestPrice (cost optimization, short workloads)
  * diversified (greater availability, long workloads)
  * capacityOptimized (optimal capacity for the number of instances)
* Spot fleet will automatically request spot instances with the lowest price


 