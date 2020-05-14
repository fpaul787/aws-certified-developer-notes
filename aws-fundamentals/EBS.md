# Elastic Block Storage

You can create persistent storage volumes for your EC2 instances with the
Amazon Elastic Block Store (Amazon EBS) service to provide block storage devices for
Amazon EC2 instances. Certain instance types enable you to mount volumes based on an
instance store, which is temporary storage local to the host machine.

## Persistent Storage
For Amazon EC2 instances, Amazon EBS provides persistent block storage. Similar to a
hard drive, block storage volumes provide read/write access at a block level and can be
formatted with a file system. Also, you can attach each EBS volume
to a single instance at a time. Amazon EBS is suitable for installing operating systems and
applications and for data that you want to store persistently. You can also encrypt the
volumes.
When you create an EBS volume, you provision a specific size for the storage volume.
You choose from several types of volumes with different underlying storage technologies
and performance options. You can increase the size of the volume later, even while it is
being used by a running instance.


EBS volumes automatically replicate the data for a particular volume within the same
Availability Zone as your Amazon EC2 instance. To increase durability of your data, you
can use Amazon EBS to make point-in-time snapshots of an EBS volume. Data for Amazon
EBS snapshots is automatically replicated across multiple Availability Zones within a
region, and these snapshots can be used to create new volumes. If there’s an accidental
delete or other application error, snapshots enable you to recover your data.

## Amazon EBS Volumes
*Amazon EBS volumes* persist independently from the running life of an Amazon EC2
instance. After a volume is attached to an instance, use it like any other physical hard drive.

It is a network drive(not physical). Uses the network to communicate the instance, so there might be some latency.


#### Provisioned capacity 
* You get billed for all the provisioned capacity
    * If you provision 1GB but use 500mb, you still get charged for 1GB



Amazon EBS provides the following volume types, which differ in performance characteristics
and price so that you can tailor your storage performance and cost to the needs of
your applications.

**SSD-backed volumes**       Solid-state drive (SSD)–backed volumes are optimized for transactional
workloads involving frequent read/write operations with small I/O size, where the
dominant performance attribute is IOPS.

**HDD-backed volumes**       Hard disk drive (HDD)–backed volumes are optimized for large
streaming workloads where throughput (measured in MiB/s) is a better performance measure
than IOPS.

**EBS Volume Types**

**GP2 (SSD):** General purpose SSD volume that balances price and performance for a
wide variety of workloads

**IO1 (SSD):** Highest-performance SSD volume for mission-critical low-latency or highthroughput
workloads

**ST1 (HDD):** Low cost HDD volume designed for frequently accessed, throughputintensive
workloads

**SC1 (HDD):** Lowest cost HDD volume designed for less frequently accessed workloads

## Amazon EBS Snapshots
* EBS Volumes can be backed up using “snapshots”

* Snapshots only take the actual space of the blocks on the volume

* If you snapshot a 100GB drive that only has 5 GB of data, then your EBS
snapshot will only be 5GB

* Snapshots are used for:
   * Backups: ensuring you can save your data in case of catastrophe
   * Volume migration:
        *   Resizing a volume down
        *   Changing the volume
        *   Encrpyt a volume

## EBS Encryption
For simplified data encryption, create encrypted Amazon EBS volumes with the Amazon
EBS encryption feature. All Amazon EBS volume types support encryption, and you
can use encrypted Amazon EBS volumes to meet a wide range of data-at-rest encryption
requirements for regulated/audited data and applications.

Amazon EBS encryption uses *256-bit Advanced Encryption Standard (AES-256)
algorithms and an Amazon-managed key infrastructure called AWS Key Management
Service (AWS KMS).* The encryption occurs on the server that hosts the Amazon EC2
instance, providing encryption of data in transit from the Amazon EC2 instance to
Amazon EBS storage.

## EBS vs Instance Store
Amazon EC2 instance store is another type of block storage available to your Amazon EC2
instances. It provides temporary block-level storage, and the storage is located on disks that are physically attached to the host computer (unlike Amazon EBS volumes, which are
network-attached).

* Pros:
    * Better I/O performance
* Cons:
    * On termination, the instance store is lost
    * You can’t resize the instance store
    * Backups must be operated by the user
    

**Overall, EBS-backed instances should fit most applications workloads**

## Summary 
* EBS can be attached to only one instance at a time
* EBS are locked at the AZ level
* Migrating EBS volume across AZ means first creating a snapshot of it, then screating it in other AZ
* EBS backups use IO and you should not run them while your application is handling a lot of traffic
* Root EBS Volumes of instances get terminated by default if the EC2 instance gets terminated. (you can disable this option)