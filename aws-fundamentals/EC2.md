# Amazon Elastic Compute Cloud

#### What is Amazon Elastic Compute Cloud (Amazon EC2)?
Virtual machines in the cloud. They enable you to provision computing environments called *instances*. Amazon EC2 allows you to choose the hardware resources you need. You can also control the OS and any other software that runs on the instance. With Amazon EC2 you can have several capabilities such as
* Renting many virtual machines(EC2)
* Storing data on virtual drives (EB2)
* Distributing load across machines (ELB)
* Scaling the services using an auto-scaling group (ASG)

#### Instance Types
Amazon EC2 allows you to choose your hardware resources from a broad set of preconfigured
options by selecting a specific instance type and instance size. For example, your
instance has a number of virtual CPUs (vCPUs) and a specific amount of RAM. The
*instance type* is rated for a certain level of network throughput.


#### Security Groups
Security groups control how traffic is allowed into or out of our EC2 Machines. They act as a "firewall" on EC2 instances. Security Groups control the following 
* Access to Ports
* Authorized IP ranges - IPv4 and IPv6
* Control of inbound network (from other to the instance)
* Control of outbound network (from the instance to other)

Security groups can be attached to multiple instances. 
If your application can not be accessed, then most likely it's a security group issue. All inbound traffic is **blocked** by default. All outbound traffic is **authorized** by default.

#### Instance Types
* On Demand Instance: you pay for compute capacity by the hour or the second depending on which instances you run.

* Reserved Instances: long workloads (>= 1 year)
    * Applications with steady state usage
    * Applications that may require reserved capacity
    * Customers that can commit to using EC2 over a 1 or 3 year term to reduce their total computing costs
* Convertible Reserved Instances: long workloads with flexible instances
* Scheduled Reserved Instances: launch within time window you reserve
* Spot Instances: allow you to request spare Amazon EC2 computing capacity for up to 90% off the On-Demand price.
    * Applications that have flexible start and end times
    * Applications that are only feasible at very low compute prices
    * Users with urgent computing needs for large amounts of additional capacity
* Dedicated Instances: no other customers will share your hardware
    * Instances running on hardware dedicated to your
* Dedicated Hosts: book an entire physical server, control instance placement
    * Full control of EC2 instance placement
    * More expensive
    * Useful for companies that have strong regulatory or compliance needs

#### Amazon EC2 Instance Families
* **General purpose** 
    * A balanced mix of CPU, RAM, and other resources

* **Compute optimized** 
    * A high amount of CPU, such as high-performance web servers,scientific modeling, and video encoding

* **Memory optimized**
    * A large amount of RAM, such as in-memory databases and distributed web scale in-memory caches

* **Storage optimized** 
    * A large amount of storage and input/output (I/O) throughput,such as data warehousing, analytics, and big data distributed computing

* **Accelerated computing** 
    * Dedicated Graphics Processing Unit (GPU) or Field ProgrammableGate Array (FPGA) resources, such as 3D rendering, deep learning, genomics research, and real-time video processing

#### Private vs Public IP
* Public IP:
    * Public IP means the machine can be identified on the internet (WWW)
    * Must be unique across the web
* Private IP:
    * Private IP means the machine can only be identified on a private network only
    * The IP must be unique across the private network

#### Elastic IPs
Your EC2 instance public IP can change when you stop and start the instance. If you want to avoid that and have a fixed public IP, you need an Elastic IP. 

**Caution**
You should avoid having an elastic IP. Instead the better option would be to use a random public IP and register a DNS name to it. Or use a Load Balancer and don't use a public IP.


#### EC2 User Data
You can *bootstrap* your instances using EC2 User data. Bootstraping means launching commands when a machine starts. The script is only ran once at the instance first start. These scripts are used to automate task such as 
* Installing updates
* Installing software
* Downloading common files from the internet 

*Example:* Installing Apache web server on an Amazon Linue 2 instance with a shell script provided to user data:

#!/bin/bash <br>
yum update - <br>
yum install httpd -y <br>
systemctl start httpd <br>
systemctl enable httpd <br>

#### Instance Metadata
With the instance metadata service (IMDS), code running on an Amazon EC2 instance can
discover properties about that instance. The instance metadata service exposes a special IP
address, 169.254.169.254, which you can query using HTTP to perform lookups.

*Example*

curl 169.254.169.254/latest/meta-data/ <br>
curl 169.254.169.254/latest/user-data/iam/ <br>
curl 169.254.169.254/latest/meta-data/ hostname <br>


#### Amazon Machine Image
An image to use to create your instances. These images can be build for Linux or Windows machines. They provide the template for the OS and applications on the root volume of your instance. Each AWS Region
maintains its own listing of AMIs. Any AMIs that you create are available only within a
specific region unless you copy them to other regions.

#### Accessing Instances
By default, Linux Amazon EC2 instances provide remote access through SSH, and
Windows Amazon EC2 instances provide remote access through the Remote Desktop
Protocol (RDP). To connect to these services, you must have the appropriate inbound rules
on the security group for the instance.

#### Amazon EC2 Key Pairs
An Amazon EC2 key pair has a name, and it is composed of a public key and a private key. If
you specify an Amazon EC2 key pair when you launch the instance, it secures the sign-in
credentials as part of the Amazon EC2 instance provisioning process.

#### Instance Lifecycle
An Amazon EC2 instance has three primary states: running, stopped, and terminated.
Additionally, there are intermediate states of pending, stopping, and shutting down. An
Amazon EC2 instance accrues charges for the compute resources only when it is in the **running** state. However, EBS volumes persist data even when an instance is stopped, so the
charges for persistent storage from any EBS volumes accrue independently from the state of
the instance.

### Connecting to Amazon EC2 Instances

#### Amazon EC2 Key Pairs
An Amazon EC2 key pair has a name, and it is composed of a public key and a private key.
AWS retains the public key, and it is your responsibility to store the private key securely. If
you specify an Amazon EC2 key pair when you launch the instance, it secures the sign-in
credentials as part of the Amazon EC2 instance provisioning process. For a Linux instance,
the public key from the key pair is added to the ~/.ssh/authorized_keys file for the
default user. For a Windows instance, the password for the default administrator account is
encrypted with the public key and can be decrypted with the private key.

*Example*
Using SSH with an Amazon EC2 instance
ssh -i "example-key.pem" ec2-user@[public DNS]

#### Assigning AWS API Credentials
You can assign an IAM role to an Amazon EC2 instance. The AWS Software Development
Kit (SDK) and AWS Command Line Interface (AWS CLI) can automatically discover these
credentials through the Amazon EC2 metadata service. You can skip the task of explicitly
confi guring credentials fi les on your instances during bootstrapping.
**AS PREVIOUSLY MENTIONED, DO NOT CONFIGURE EC2 INSTANCES WITH PERSONAL CREDENTIALS.**

You can associate a particular
instance profi le with many Amazon EC2 instances. However, a particular Amazon
EC2 instance can be associated with one instance profi le at a time, and an instance
profile can be associated with only one IAM role. When an instance profi le with an IAM role is associated with an instance, the Amazon
EC2 service makes the necessary calls to the AWS Security Token Service (AWS STS) automatically
to generate short-term credentials for that instance. These credentials are based
on the IAM role associated with the instance profile.




