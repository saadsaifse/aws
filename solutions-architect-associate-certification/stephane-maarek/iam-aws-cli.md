## IAM & AWS CLI

* Identity and Access Management
* IAM is a global service
* Root account created by default shouldn't be used or shared

### Groups
* Users are people in the organization that can also be grouped
* Groups cannot be nested
* Users can stay without any group 
* Users can also belong to multiple groups

### Permissions

* Users and groups can be assigned JSON documents called policies 
* The policies define the permissions of the users
* Apply the least privilege principle
* Multiple policies can be applied to a user, group, etc. 
* Policy can be attached to a group , to a specific user. This is defined by the Principal in policies
  

#### Policy Structure

* Version number, always include 2012-10-17
* Id of the policy
* One or more individual statements
  * Sid is the id of statement
  * Effect of the statement e.g., allow, deny
  * Principal is the account/user/role to which the policy is applied to
  * Action is the list actions the policy allows or rejects
  * Resources are the list of resources to which the actions applied to
  * Condition is when the policy is in effect


### AWS Access

* Management Console (protected by password + MFA)
* AWS CLI (protected by access keys)
* AWS SDK (protected by access keys)
* Access keys are generated through AWS console
* Users manage their own access keys
* Access keys are secret, just like a password. Don't share them


### AWS CLI
* Tool to interact with AWS CLI
* Direct public API access of AWS services
* Can create scripts to automate the tasks
* It's open-source

### AWS SDK

* Language specific APIs
* Embedded within your application
* Also has Mobile and IoT SDKs
* AWS CLI is built on AWS SDK for Python, named Boto
* Install and use `aws configure` command to set up the cli with access key
* Try `aws iam list-user` command

 