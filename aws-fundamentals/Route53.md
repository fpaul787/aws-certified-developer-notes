# Amazon Route 53

## What is Amazon Route 53
Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web
service. It is designed to give developers and businesses an extremely reliable and cost-effective
way to route end users to internet applications by translating names like w ww.example.com
into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other.
Amazon Route 53 is fully compliant with IPv6 as well.

## AWS Common Records
* A: URL to IPv4
* AAAA: URL to IPv6
* CNAME: URL to URL
* Alias: URL to AWS resource

Alias over CNAME works better for AWS resources

## Features of Route53
* Load balancing (through DNS - also called client load balancing)
* Health checks (limited)
* Routing policy: simple, failover, geolocation, geoproximity, latency, weighted


## Things you should know
* The record types
* Prefer Alias records over CNAME for AWS resources

