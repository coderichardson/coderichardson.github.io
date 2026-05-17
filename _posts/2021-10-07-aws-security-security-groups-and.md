---
title: "AWS Security Groups and Network ACLs"
date: 2021-10-07 02:23:00 +0000
tags:
  - "Cloud"
  - "AWS"
  - "Networking"
  - "Cybersecurity"
---

### Introduction

Today we're covering some basic but very important elements of AWS Security -- Security Groups and Network ACLs.

### Security Groups

Security Groups are a fundamental security feature in AWS. They help protect EC2 instances, Lambda scripts, Load Balancers, containers (Amazon ECS), AWS Transfer Family, and much more. They are the "last line" of defense in a lot of cases as well, so they're important to understand and get right.

Security Groups operate similarly to a firewall by limiting the flow of traffic. Security Groups do this to and from whatever they are attached to (technically they attach to network interfaces but those are attached to the things in AWS you're looking to protect). By default, Security Groups allow all outbound traffic and deny all inbound traffic. You then create or delete rules, but any rules created are Allow rules. In other words, there are no Deny rules. Access is granted to a specific CIDR range (e.g. 192.168.1.10/32, 192.168.1.1/24) or to another Security Group.

|  |
| --- |
|  |
| Security Group showing HTTP and SSH traffic from any source being allowed inbound. |

There are a lot of rules surrounding Security Groups and it's important to be aware of them. I'll highlight some of them below, but refer to the [AWS documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) for a comprehensive list.

- Security group rules enable you to filter traffic based on protocols and port numbers.
- Security groups are stateful—if you send a request from your instance, the response traffic for that request is allowed to flow in regardless of the inbound rules. This also means that responses to allowed inbound traffic are allowed to flow out, regardless of the outbound rules.
- You can add and remove rules at any time. Your changes are automatically applied to the instances that are associated with the security group.
- When you associate multiple security groups with an instance, the rules from each security group are effectively aggregated to create one set of rules. Amazon EC2 uses this set of rules to determine whether to allow access.
- When you specify a security group as the source or destination for a rule, the rule affects all instances that are associated with the security group.

Security Group organization can get out of hand quickly in a production environment. If you're not careful you can end up with a ton of different Security Groups and/or Security Groups that are overly permissive! Here are some of my tips to help keep things in check:

- Plan a Security Group's use. Don't create one-off Security Groups just because it's easy.
- Know what traffic you're wanting to allow and create the Security Group rules accordingly. Follow least privilege.
- Remember that Security Groups allow for rules with other Security Groups -- not just IP addresses. This can simplify traffic flow depending on your environment's architecture.

#### Network ACLs

Another fundamental AWS security feature -- Network ACLs (NACLs). Where Security Groups are attached to instances, NACLs are attached to subnets. They also share the responsibility of filtering traffic and offering protection within your AWS VPC. That's where most of the similarities stop however:

- Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
- A network ACL has separate inbound and outbound rules, and each rule can either allow or deny traffic.
- Network ACLs are stateless, which means that responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa).
- A network ACL contains a numbered list of rules. We evaluate the rules in order, starting with the lowest numbered rule, to determine whether traffic is allowed in or out of any subnet associated with the network ACL. The highest number that you can use for a rule is 32766. We recommend that you start by creating rules in increments (for example, increments of 10 or 100) so that you can insert new rules where you need to later on.
- Your VPC automatically comes with a modifiable default network ACL. By default, it allows all inbound and outbound IPv4 traffic and, if applicable, IPv6 traffic.

|  |
| --- |
|  |
| Network ACL showing inbound and outbound rules. |

### Conclusion

I've included a simple diagram below which shows where Network ACLs and Security Groups play their roles -- the subnet and individual instance respectively. (I've excluded things like route table, Internet gateways, etc for the sake of simplicity).

These features are your "bread and butter" for blocking unwanted traffic to or from sections of AWS. They're also important to keep in mind while troubleshooting any communication issues in your environment.

![](/assets/img/posts/aws-security-security-groups-and/01.png)