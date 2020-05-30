# EFS - Elastic File System

* Managed NFS (network file system) that can be mounted on many EC2 instances

* EFS workds with EC2 instances in **multi-AZ**.

* Highly available, scalable, expensive.

* Can be encrypted using KMS.

Could be cheaper to use rather than EBS based on well you manage your data.

#### Use Cases
* Content Management
* Web Serving
* Data Sharing
* Word Press

EFS is only compatible with Linux based AMI (not windows) because it is a POSIX
file system.

#### Performance & Storage Classes
* EFS Scale
    * Grow to Petabyte-scale network file system, automatically
* Performance mode(set at EFS creation time)
    * General purpose(default): latency-sensitive use cases (web server, CMS, etc...)
    * Max I/O - higher latency, throughput, highly parallel (big data, media processing)
* Storage Tiers (lifecycle management feature - move file after N days)
    * Standard: for frequently accessed files
    * Infrequent access(EFS-IA): cost to retrieve files, lower price to store.

