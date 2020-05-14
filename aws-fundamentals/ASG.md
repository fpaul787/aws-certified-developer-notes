# Auto Scaling Groups

The load on your website and application can change spontaneously. The benefits of using the Cloud is that you can quickly create and get rid of servers. 

## What are Auto Scaling Groups?
They scale out (add EC2 instances) to match an increased load. Additionally, they Scale in (remove EC2 instances) to match a decreased load. Auto Scaling Groups (ASG) also ensure we have a minimum and maximum number of machines running. ASG also have the ability to register new instances to a load balancer. 

## Characteristics

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


## Alarms
You can scale ASG based on CloudWatch alarms
The alarm monitors a metric(like Average CPU).

## Scaling Policies

#### Target Tracking Scaling
* Simplest and easiest scaling policy that you can make.
* Example: You want the CPU instances in the ASG to stay at 30% or so.
   * If you are over that CPU usage, it provision more instances
   * If under, it will remove instances

#### Simple/ Step Scaling
* CloudWatch alarm is triggered (CPU > 30%) add 2 units.
* CloudWatch alarm is triggered (CPU < 10%) remove 1
   * A lot more control

#### Scheduled Actions
* Anticipate scaling based on known usage patterns
* *Example*: You know that every monday at 9am the number of instances need to increase. 

## Scaling Cooldowns
* Makes sure that ASG doesn't launch or terminate new instances before the previos scaling occurs.
* ASGs have a default cooldown, but you can also create a cooldown for the simple scaling policy.
* 


## Summary
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
