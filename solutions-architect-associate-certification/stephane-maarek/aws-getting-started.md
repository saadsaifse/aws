## Getting Started With AWS

* 2002: Launched internally
* 2004: Launched publicly with SQS
* 2006: Re-launched SQS, S3, and EC2
* 2007: Launched in Europe

### AWS Use-Cases:

* Enterprise IT, Backup and Storage, Big data analytics
* Website hosting, mobile and social apps
* Gaming servers


### AWS Global Infrastructure

* AWS Regions
* AWS Availability Zones
* AWS Data Centers
* AWS Edge Locations/Points of Presence

Everything can be viewed here: https://aws.amazon.com/about-aws/global-infrastructure/regions_az/


#### Region
AWS region is a physical location around the world that has multiple availability zones. 

> Which region should we choose? 

Depends on: 
* Compliance: data governance, legal requirements? data never leaves a region without explicit permission
* Proximity to customers: reduced latency
* Available services: not all services are available in every region
* Pricing: pricing varies with regions. It is transparent in service pricing page



#### Availability Zones

* Each region has many AZs
* Usual number is 3, min is 2, and max is 6. 
* Each zone is a discrete data center with redundant power, networking, and connectivity
> AWS doesn't tell us the number of data centers in an availability zone
* AZs are isolated from disasters
* AZs are connected with high-bandwidth network

#### Points of Presence (Edge Locations)

* 216 points of presence 
    * 205 edge locations 
    * 11 regional caches
    * in 84 cities across 42 countries
* content is delivered to end users with lower latency

#### AWS Console

AWS global services:

* IAM
* Route S3 (DNS Service)
* CloudFront (Content Delivery Network)
* WAF (Web Application Firewall)

Most AWS services are region-scoped e.g.

* EC2 (IaaS)
* Elastic Beanstalk (PaaS)
* Lambda (Function aaS)
* Rekognition (SaaS)

Note: Region table exists to checkout the services in a region



