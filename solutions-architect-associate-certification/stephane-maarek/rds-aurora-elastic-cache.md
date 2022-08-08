## RDS + Aurora + ElastiCache

* AWS managed relational database that uses SQL
* Allows to create the following databases
  * Postgres
  * MySQL
  * MariaDB
  * Oracle
  * Microsoft SQL Server
  * Aurora (AWS proprietary database)

### Advantage over running a DB server on an EC2 instance

* RDS is a managed service
  * Automated provisioning, OS patching
  * Continuous backups and restore to specific timestamp (point in time restore)
  * Monitoring dashboards
  * Multi AZ setup for DR
  * Maintenance windows
  * Scaling capability (vertical and horizontal)
  * Storage backed by EBS (gp2 or io1)
* Cannot SSH into the instances, as this is a service, not a dedicated EC2 instance

### RDS Backups`

* Automated backups
* Daily full backups during a maintenance window
* Transaction logs are backed-up by RDS every 5 minutes
* Can restore to any point in time until 5 minutes ago
* 7 days retention (max. 35 days)
* DB Snapshots:
  * Manual by the user
  * Unlimited retention time

### RDS - Storage Auto Scaling

* Scales the storage automatically based on a max threshold
* todo

