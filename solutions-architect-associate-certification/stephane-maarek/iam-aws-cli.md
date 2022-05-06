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


 