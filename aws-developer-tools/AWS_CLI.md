# Development with AWS Services

#### AWS CLI

* **NEVER EVER PUT YOUR PERSONAL CREDENTIALS ON AN EC2** 
* If the EC2 is compromised, so is your personal account
* IAM Roles can be attached to EC2 instances


#### AWS EC2 Instance Metadata
Allows AWS EC2 instances "to learn about themselves" **without using an IAM Role for that purpose** The URL is http://169.254.169.254/latest/meta-data
*  You can retrieve the IAM Role name from the metadata, but you CANNOT
retrieve the IAM Policy.
* Metadata = Info about the EC2 instance
* Userdata = launch script of the EC2 instance
