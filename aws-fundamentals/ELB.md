# Elastic Load Balancer

## What are Load Balancers?
Servers that forward internet traffic to multiple servers (EC2 Instances) downstream. An integral part to directing and managing traffic amoung your instances. For your applications to have high performance and high availability for your users, you will need a load balancer.

 ## Why are they used?

 * Spread load acroos multiple downstream instances
 * Expose a single point of access (DNS) to your application
 * Handle failures of downstream instances
 * Do regular health checks to  your instances
 * High availability across zones
 * Separate public traffic from private traffic


 ## Types of Load Balancer on AWS
 <h5>AWS has **3 kinds of Load Balancers**</h5>

* Application Load Balancer
    * Provides advanced request routing targeted at delivery
of modern application architectures, including microservices and container-based
applications. It simplifies and improves the security of your application by ensuring
that the latest Secure Sockets Layer (SSL)/Transport Layer Security (TLS) ciphers and
protocols are used at all times. 
    * The Application Load Balancer operates at the request
level (Layer 7) to route HTTP/HTTPS traffic to its targets: Amazon EC2 instances,
containers, and IP addresses based on the content of the request. It is ideal for
advanced load balancing of HTTP and HTTPS traffic.
    * The application servers don't see the IP of the client directly
        * The true IP of the client is inserted in the header X-Forwarded-For
        * We can also get Port (X-Forwarded-Port) and proto (X-Forwarded-Proto)

* Network Load Balancers
    * Operates at the connection level (Layer 4) to route
TCP traffic to targets: Amazon EC2 instances, containers, and IP addresses based
on IP protocol data. It is the best option for load balancing of TCP traffic because
it’s capable of handling millions of requests per second while maintaining ultra-low
latencies. Network Load Balancer is optimized to handle sudden and volatile traffic
patterns
while using a single static IP address per Availability Zone. It is integrated
with other popular AWS services, such as AWS Auto Scaling, Amazon Elastic Container
Service (Amazon ECS), and AWS CloudFormation. Amazon ECS provides
management for deployment, scheduling, and scaling, and management of containerized
applications.
* Classic Load Balancers
    * Provides basic load balancing across multiple Amazon
EC2 instances and operates at both the request level and the connection level. The
Classic Load Balancer is intended for applications that were built within the
EC2-Classic network. When you’re using Amazon Virtual Private Cloud (Amazon
VPC), AWS recommends the Application Load Balancer for Layer 7 and Network
Load Balancer for Layer 4).
    * This LB is deprecated


## Health Checks
Health Checks are crucial for Load Balancers. Health Checks allow the load balancer to determine if the instances it forwards traffic to are available to reply to requests. 

## Load Balancer
* Any Load Balancer (CLB, ALB, NLB) has a static host name. Do not
resolve and use underlying IP
* LBs can scale but not instantaneously – contact AWS for a “warm-up”
* NLB directly see the client IP
* 4xx errors are client induced errors
* 5xx errors are application induced errors
* Load Balancer Errors 503 means at capacity or no registered target
* If the LB can’t connect to your application, check your security groups.






