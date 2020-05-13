# Amazon Virtual Private Cloud
Amazon Virtual Private Cloud (Amazon VPC) provides logically isolated networks
within your AWS account. These networks are software defined and can span all of the
Availability Zones within a specific AWS Region.

In a region you can create VPCs. Each VPC contains subnets and each subnet must be mapped to an AZ.

## Connecting to Other Networks
By default, an Amazon VPC is an isolated network. Instances within an Amazon VPC
cannot communicate with the internet or other networks until you explicitly create connections.

### Amazon VPC Connection Types
* Internet Gateway: 
    * A highly available connection that allows outbound and inbound
requests to the internet from your Amazon VPC
* Egress Only Internet Gateway:
    * A special type of internet gateway for IPv6 that allows outbound traffic
and corresponding responses but blocks inbound connections
* Virtual Private Gateway
    * Allows you to establish a private connection to your corporate network
by using a VPN connection or through Direct Connect (DX)
* Amazon VPC Endpoints
    * Allows traffic from your Amazon VPC to go to specific AWS services or
third-party SaaS services without traversing an internet gateway
* Amazon VPC Peering
    * Privately routes traffic from one Amazon VPC to another Amazon VPC
by establishing a peer relationship between this VPC and another VPC
* AWS Transit Gateway
    * Allows you to centrally manage connectivity between many VPCs and
an on-premises environment using a single gateway

### **IP Addresses**
There are four different types of IP addresses available
for use with Amazon VPC.

## Private IP Addresses
Private IP addresses are IPv4 addresses that are not reachable from the internet. These
addresses are unique within a VPC and used for traffic that is to be routed internally within
the VPC, for private communication with corporate networks, or for private communication
with other VPCs.

When an instance is assigned a private IPv4 address, this address last even when the instance is stopped.

## Public IP Addresses
The public IP address is an IPv4 address that is reachable from the internet. This address only last while the instance is running. 

## Elastic IP Addresses
An Elastic IP address is similar to a public IP address in that it is an IPv4 address that is
reachable from the internet. However, unlike public IP addresses, you manage the association
between instances and Elastic IP addresses. You control when these addresses are
allocated, and you can associate, disassociate, or move these addresses between instances
as needed.


## IPv6 Addresses
In addition to IPv4 addresses, you can associate an Amazon-provided block of IPv6
addresses to your VPC. When you enable IPv6 in your VPC, the network operates in
dual-stack mode, meaning that IPv4 and IPv6 commutations are independent of each
other. Your resources can communicate over IPv4, IPv6, or both.


## Subnets
When you launch an Amazon EC2 instance into a subnet, its primary network interface
assigns a private IPv4 address automatically from the CIDR range assigned to the subnet.
Typically, you create at least two types of configurations for subnets in a VPC. The first
is for subnets in which you place instances that you want to reach directly from the internet.
This could be an instance running as a web server, for example. Subnets of this type
are known as **public subnets.**

The **second type** of configuration is usually a subnet that backend instances use that
must be accessible to your other instances but should not be directly accessible from the
internet. Subnets of this type are known as **private subnets**. For example, if you had
an instance that was dedicated to running a database, such as MySQL, you could place
that instance in a private subnet. It would be accessible from the web server in the public
subnet, but it would not accept traffic from the internet.


## Route Tables
Unless explicitly associated with a specific route table, subnets associate with a
default route table called the main route table. By default, the main route table includes
only the local route. This means that subnets that are associated with the default route
table have no connection to the internet. They can route traffic privately only within the
Amazon VPC.

## Network Access Control Lists
In addition to routes, network access control lists (network ACLs) allow an administrator
to control traffic that enters and leaves a subnet. A network ACL consists of inbound
and outbound rules that you can associate with multiple subnets within a specific Amazon
VPC. Network ACLs act as a stateless firewall for traffic to or from a specific subnet.

## Network Address Translation
Network address translation (NAT) allows for instances in a private subnet to make outbound
requests to the internet without exposing those instances to inbound connections
from internet users. To provide NAT for outbound requests from private subnets, you can
use an Amazon EC2 instance configured to perform NAT or a NAT gateway. The instances
in the private subnet maintain their own private IP addresses and effectively share the public
IP address of the NAT when making internet requests.

## Monitoring Amazon VPC Network Traffic
You can monitor the network flows within your Amazon VPC by enabling Amazon VPC
Flow Logs. You can then publish these logs to Amazon CloudWatch Logs or store them as
log files in Amazon Simple Storage Service (Amazon S3). Enable Amazon VPC Flow Logs
on a particular Amazon VPC, on a subnet, or on a specific elastic network interface, such
as for an Amazon EC2 instance.




### Summary
* These topics are not covered to much in the exam
* All new accts come with default VPC
* VPC are per Account per Region
* Subnets are per VPC per AZ
* Some AWS resources can deployed in VPC while others can't

## Exam Essentials
**Know** the basics of Amazon EC2, such as resource types, instance types, AMIs, and storage.
Be familiar with launching and connecting to Amazon EC2 instances. Understand the
resource types of Amazon EC2 instance types. Be familiar with the purpose of an AMI
in relation to launching an instance. Understand the distinction between persistent and
ephemeral storage related to a particular Amazon EC2 instance.

**Know** about user data, instance metadata, and credentials. Be familiar with using user
data to customize the software by executing scripts on instances. Any scripts or code running
on an instance can use the Amazon EC2 metadata service to discover the instance
configuration. Use IAM roles to provide AWS Cloud API credentials automatically to code
running on an Amazon EC2 instance.

**Know** how Amazon EC2 communicates with Amazon VPC. Understand the relationship
between an EC2 instance and the Amazon VPC network. There may be questions
that ask you to troubleshoot issues related to connecting to an Amazon EC2 instance. Be
familiar with how Amazon VPC enables communication between Amazon EC2 instances
within the same Amazon VPC and isolates those instances from other Amazon VPCs.
Recognize how route tables, network access control lists, and security groups control network
traffic.

**Know** about public and private subnets. Within an Amazon VPC, you must be able to
distinguish between public and private subnets. Public subnets allow you to assign public
IPv4 addresses to Amazon EC2 instances. By contrast, instances in a private subnet have
only private IP addresses. The key distinction is that public subnets have a route table entry
that forwards internet-bound traffic to an internet gateway. Private subnets do not have
a direct route to the internet. Instead, these subnets have a route that forwards internetbound
traffic through a NAT gateway or NAT instance.