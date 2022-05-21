## High Availability and Scalability: ELB & ASG

### Vertical Scaling
* Increase instance size = (scale up /down)
    * From: t2.nano 0.5G of RAM
    * To: u-12tbl.metal - 12.3TB of RAM
  
### Horizontal scaling
* Increase number of instances = (scale out/in)
  * Auto scaling group
  * Load balancer
  
### High Availability 
* Run instances for the same application across multi-AZ
  * Auto scaling group
  * Load balancer


### Elastic Load Balancer

* Load balances are servers that forward traffic  to multiple servers (EC2 instances) downstream
* ELB is a managed load balancer
  * Guarantee of working LB
  * Upgrades, maintenance, high availability are taken care of
  * Few configuration knobs
* Integrated with many AWS offerings / services
  * EC2, EC2 auto scaling groups, AWS ECS
  * AWS certificate manager (ACM), CloudWatch
  * Route 53, AWS, WAF, AWS Global Accelerator

### Types of load balancer on AWS

* 4 types of load balancers
  * Classic load balancers v1
  * Application load balancers v2
  * Network load balancer (v2 - new generation)
  * Gateway load balancer 2020 (operated at layer 3 network layer)
* Recommended to use the latest generation
* Can be setup as as internal (private) or external (public) ELBs


### Classic load balancers (Deprecated)

* Supports TCP (layer 4), HTTP & HTTPS (Layer 7)
* Health checks are TCP or HTTP based 
* Fixed hostname (xxx.regio.elb.amazonnews.com)

### Application load balancer

* Load balances multiple http applications
* supports web sockets and https
* Routing tables to different target groups
  * based on path in url
  * based on hostname in url
  * based on the query string
* Great for micro-services and container based applications
* Has a port mapping feature to redirect to a dynamic port in ECS
  
#### ALB Target Groups
* EC2 instances (can be managed by an auto scaling group) - HTTP
* ECS task (managed by ECS itself) - HTTP
* Lambda functions - HTTP request is translated into a JSON event
* IP addresses - must be private IPs
* ALB can route to multiple target groups
* Health checks are done at the target group level


* ALB has a fixed hostname
* The application servers don't see the IP of the client directly, but instead it is in the x-forwarded-for http header of the request
* Port and proto can also be found in x-forwarded-port and x-forwarded-proto respectively


### Network Load Balancer

* Work at the network layer 4 (low-level)
* Forward TCP/UDP traffic to instances
* Handle millions of request per seconds
* Less latency ~100ms (vs 400ms for ALB)
* NLB has a static IP per AZ, and supports assigning Elastic IP
* Not included in the free tier

### Gateway Load Balancer

* Deploy, scale, and manage a fleet of 3rd party network virtual appliances in AWS
* E.g., firewalls, intrusion detection, packet inspection, etc.
* Operates at the lower level (layer 3) -- IP packets
* Combines the following:
  * Transparent network gateway -- single entry/exit for all traffic
  * Load balancer -- distributes traffic to virtual instances
* Uses the GENEVE protocol on port 6081

### Cross-Zone Load Balancing

* Balancing the load equally between the instances in all AZ
* Application load balancer
  * Always on  (can't be disabled)
  * No charges for inter AZ data
* Network load balancer
  * Disabled by default
  * You pay chargers for inter AZ data if enabled
* Classic load balancer
  * Disabled by default
  * No charger for inter AZ data, if enabled 

### SSL in Elastic Load Balancer
* SSL and TLS (newer)
* Uses X.509 certificate
* Can manage using ACM (AWS Certificate Manager)
* Can also upload your own certificate
* Must specify a default certificate
* Clients can use SNI (Server Name Indication)

#### SNI (Server Name Indication)
* How do you load multiple SSL certificates on a single webserver to be able to host multiple websites
* Requires the client to indicate the hostname of the target server in the initial SSL handshake
* The server finds the correct certificate or return the default one
* Only for ALB, NLB, CloudFront
* Does not work with CLB


### Connection Draining/Deregistration delay

* The time to complete "in-flight requests" while the instance is de-registering or unhealthy
* The instance will finish the existing requests in the draining time
* Load balancer will send new requests to the new EC2 instances
* The delay is usually 1 to 3600 seconds (default: 300 seconds)
* Can be disabled (set value to 0)
* Set a low value if requests are short

### Auto Scaling Group (ASG)

*  Scale out or scale in automatically based on some configuration
* Ensures a min/max number of EC2 instances are running
* Automatically register new instances to a load balancer
* ASG and load balancers work hang in hand
* Launch configuration
  * AMI + instance type
  * EC2 user data
  * EBS volume
  * Security groups
  * SSH key pair
  * Min/max size, initial capacity
  * Network + subnet information
  * Load balancer information
  * Scaling policies
* Auto Scaling Alarms
  * Based on CloudWatch metrics
  * Alarm trigger scale out or scale in alarms
* Auto Scaling Rules
  * Target avg CPU usage
  * Number of requests on the ELB per instance
  * Average network in/out
  * Custom metrics
    * No. of connected users
    * Send custom metric from application on EC2 to CloudWatch using PutMetric API
    * Create CloudWatch alarm to react to low/high values
    * Use the alarm to trigger the scaling policy for ASG
* IAM roles attached to an ASG will get assigned to EC2 instances
* ASG are free. You pay for the underlying resources being launched
* ASG will also auto-create new instances if any instance gets terminated

#### ASG Scaling Policies

* Dynamic Scaling Policies
  * based on the CPU utilization of the instances e.g., >70% of processor usage etc.
  * based on request count per target
  * based on a schedule
* Predictive Scaling
  * Forecast the load and schedule ahead
* Scaling Cooldowns
  * After any scaling activity, a cooldown period starts (default 300 seconds)
  * During cooldown, ASG will not launch or terminate additional instances (to allow metrics to stabilize)

### ASG - For Solutions Architect

* Find AZ that has most number of instances
* Terminate the ones that has the oldest launch configuration
* Lifecycle hooks
  * Ability to perform extra steps before the instance goes in service (Pending state)
  * Same before an instance is terminated
* Launch template vs. Launch Configuration
  * Both define AMI, instance type, Security groups, etc.
  * Launch configuration is legacy that must be created every time
  * Launch templates are newer and can have multiple versions. Has more features too

