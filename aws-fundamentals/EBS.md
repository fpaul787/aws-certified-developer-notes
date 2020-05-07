# Elastic Block Storage

You can create persistent storage volumes for your EC2 instances with the
Amazon Elastic Block Store (Amazon EBS) service to provide block storage devices for
Amazon EC2 instances. Certain instance types enable you to mount volumes based on an
instance store, which is temporary storage local to the host machine.

#### Persistent Storage
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

