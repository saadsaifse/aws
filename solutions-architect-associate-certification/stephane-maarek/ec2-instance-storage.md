### EC2 Instance Storage

#### EBS Volume

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
  
