# Auto Scaling Groups

The load on your website and application can change spontaneously. The benefits of using the Cloud is that you can quickly create and get rid of servers. 

#### What are Auto Scaling Groups?
They scale out (add EC2 instances) to match an increased load. Additionally, they Scale in (remove EC2 instances) to match a decreased load. Auto Scaling Groups (ASG) also ensure we have a minimum and maximum number of machines running. ASG also have the ability to register new instances to a load balancer. 

#### Characteristics

* Launch Configuration
   * AMI + Instance Type
   * EC2 User Data
   * EBS Volumes
   * Security Groups
   * SSH Key Pair

* Min Size / Max Size / Initial Capacity
* Network + Subnets Information
* Load Balancer Information
* Scaling Policies


#### Alarms
You can scale ASG based on CloudWatch alarms
The alarm monitors a metric(like Average CPU).


#### Summary
* Scaling policies can be on CPU, Network… and can even be on custom metrics or
based on a schedule (if you know your visitors patterns)
* ASGs use Launch configurations and you update an ASG by providing a new launch
configuration
* IAM roles attached to an ASG will get assigned to EC2 instances
* ASG are free. You pay for the underlying resources being launched
* Having instances under an ASG means that if they get terminated for whatever
reason, the ASG will restart them. Extra safety!
* ASG can terminate instances marked as unhealthy by an LB (and hence replace
them)
