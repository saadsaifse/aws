## EC2 - Solutions Architect Associate Level

### Elastic IPs
* EC2 instance changes its IP upon restart
* If you need to have a fix public ip for your instance, you need an elastic ip
* Elastic ip is a public ipv4 ip that you own as long as you don't delete it
* Can be attached to only one instance at a time
* Can only have 5 elastic ips per account (can be asked to increase)
* Try to avoid elastic ips
  * as they reflect poor arch decisions
  * instead use a DNS


### EC2 Placement Groups

* Defines where are EC2 instance placed
* Cluster
  * cluster instances into a low-latency group in a single AZ
* Spread
  * spread instances across underlying hardware (max 7 instances per group per AZ) - critical apps
* Partition
  * spreads instances across many different partitions (which rely on different set of racks) within an AZ. Scales to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)
  

### Elastic Network Interfaces

* Logical component in a VPC that represents a virtual network card
* ENI can have
  * primary private ipv4, one or more secondary ipv4
  * One elastic ipv4 per private ipv4
  * one public ipv4
  * one or more security groups
  * MAC address
* Can be attached separately from EC2
* Bound to AZs

### EC2 Hibernate

* Stop -- data on EBS stays intact
* Terminate -- data is lost
* Hibernate -- in-memory RAM state is preserved
  * data is saved in a file on EBS encrypted upon hibernation
* Useful for long running processes, saving the ram state, or speed up the boot
* Ram size must be less than 150 GB
* Root volume must be EBS
* Instance can not be hibernated more than 60 days
* Use the `uptime` command to check the last restart time


### EC2 Nitro

* Underlying platform for next generation ec2 instances
* New virtualization technology
* Better performance
  * higher EBS speed
  * better networking options

### vCPUS

* Each thread is represented as a virtual CPU
* vCPUs = no. of cores * no. of threads

### Capacity Reservations
* Ensures EC2 capacity when needed
* Manual or planned end-date for the reservation