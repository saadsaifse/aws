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


