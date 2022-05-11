## EC2 Instance Storage

### EBS Volume

* Elastic Block Store Volume
* A network drive you can attach to your instance while they run
* Allows to persist data even after the instance is terminated
* Can only be mounted to one instance at a time
* Just like a network USB drive
* Free tier: 30 GB of general purpose SSD or Magnetic per month
* It's not a physical drive, instead a network drive so that it can be removed and attached to other instances
* It's locked to an AZ, so the EBS cannot move between regions without first taking a snapshot
* Have a provisioned capacity (GBs, and I/Opts)
* The drive's size can be increased over time
* Multiple EBS volumes can be attached to an instance
* EBS volume can also remain unattached -- just like a usb stick
* The deletion is controlled by Delete on termination attribute
  * By default the root EBS volume is deleted 
  * Any other attached EBS volumes are not deleted
  

### EBS Snapshots

* Snapshots are the backup
* Not necessary to detach from EC2 instance, but recommended
* Can copy snapshots across AZ or region
* Snapshot can be used as another EBS in other AZ
*  EBS Snapshot archive is to store the EBS snapshots which is 75% cheaper
   *  Takes 24-72 hours for restoring the archive
* Recycle bin for EBS snapshots
  * Setup rules to retain the deleted snapshots, to recover after an accidental deletion
  * Retention can be specified from a day to a year


### AMI

* Amazon machine image 
* A customization of EC2 instance
  * Add own software, configurations, OS, monitoring, etc.
* AMIs are built for specific regions but can be copied across regions 
* EC2 instances can be launched from a public AMI (AWS provided) or using your own AMI or from AWS marketplace


### EC2 Instance Store

* Disk space directly connected to the EC2 store instead of network attached EBS
* Is high-performance disk
* Storage would be lost if EC2 instance is stopped or terminated (ephemeral)
* Not durable store. Use cases: cache, scratch data, temp content
* Risk of data loss if hardware fails

### EBS Volume Types

* 6 types
  * gp2/gp3 (SSD): general purpose volumes
  * io1 / io2 (SSD): Highest-performance SSD volume for mission-critical
  * st1 (HDD): Low cost HDD volume for frequently accessed, throughput intensive workloads
  * sc 1 (HDD): Low cost HDD volume for less frequently accessed workloads

* EBS volumes are characterized in size, throughput, IOPS (I/O ops per sec)
* Only gp2/gp3 and io1/io2 can be used as boot volumes

#### Volume type use-cases

* General purpose SSG
  * cost-effective, low latency
  * system boot volumes, development and test environments
* 1 GiB - 16 TiB
* gp3
  * Baseline of 3000 IOPS and throughput of 125 MiB/s
  * Can increase IOPS up to 16000 and throughput up to 1000 MiB/s independently
* gp2
  * Small gp2 volumes can burst IOPS to 3000
  * Size of the volume and IOPS are linked, max IOPS is 16000
  * 3 IOPS per GB means at 5334 GB, we are at the max IOPS

* Provisioned IOPS (PIOPS) SSD
  * Apps that need more than 16000 IOPS
  * Great for DB workloads
  * io1/io2 (4 GiB - 16 TiB)
  * Max PIOPS: 64000 for Nitro EC2 instances and 32000 for other
  * Can increase PIOPS independently from storage size
  * io2 Block Express (4GiB - 64 TiB)

* Hard Disk Drives (HDD)
  * Cannot be a boot volume
  * 125 MiB to 16 TiB


### EBS Multi-Attach

* Attache same EBS volume to multiple EC2 instances in the same AZ
* Each instance has full read/write permissions
* Use-case:
  * Achieve higher application availability in clustered Linux applications (ex. Teradata)
  * Apps that must make concurrent write operations
* Must use a file system that's cluster-aware (not XFS, EX4, etc..)


### EBS Encryption


