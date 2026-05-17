---
title: "Protecting Applications Using AWS WAF"
date: 2024-07-29 01:27:00 +0000
tags:
  - "Cloud"
  - "AWS"
  - "Cybersecurity"
  - "Web Applications"
---

![](/assets/img/posts/protecting-applications-using-aws-waf/01.png)
Amazon's Web Application Firewall (WAF) allows for seamless integration with existing AWS resources and easy configuration. It may have its limitations, but it provides many common protections for web applications and can be spun up very quickly.

Everything I've included below can be found in [Amazon's documentation](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html). However, I've highlighted parts that I found particularly important and left other details out.  

## **AWS WAF Classic vs AWS WAF**

If you're still on WAF Classic, you should try to migrate to AWS WAF. The "new" version has been out several years (though rules do not automatically convert and Amazon's conversion tool does not work in all scenarios). There are a number of new capabilities and features, notably managed rules. And if you have version control and infrastructure as code (IaC) implemented widely throughout your environment, rules are now JSON objects.

I will leave it at that as I suspect most people are on the current AWS WAF.

## **Resources AWS WAF Protects**

AWS WAF protects the following types of resources:

- CloudFront distributions
- Amazon API Gateways
- Application Load Balancers
- AppSync GraphQL API
- Cognito user pool
- App Runner service
- Verified Access instance

The WAF Web ACL must be in the same region as the resource it's protecting. A special case worth noting is CloudFront distributions -- you must use the US East Region when creating a WAF to apply to a CloudFront distribution.

## **AWS WAF Components**

The AWS WAF consists of the following

- Web ACLs
- Rules
- Rule Groups

**Web ACLs**

Web ACLs are the AWS WAF resource you assign to protect another AWS Resource -- for example, an Application Load Balancer. Rules, and optionally Rule Groups, that you make comprise the Web ACL are ultimately what provide the protection against resources.

![](/assets/img/posts/protecting-applications-using-aws-waf/02.png)
#### Rules

There are two types of rules that can be added to AWS WAF -- Managed and Custom. Custom rules allow you to add IP sets, a previously create Rule Group, or use Amazon's rule builder.

![](/assets/img/posts/protecting-applications-using-aws-waf/03.png)
Managed rules allow you to add a pre-defined rule(s) created by Amazon or a third-party company. This functionality along with the ease of configuration on your Web ACL are definitely the biggest takeaway from AWS WAF.

![](/assets/img/posts/protecting-applications-using-aws-waf/04.png)
Some examples of AWS Managed rules are:

- Core rule set - contains rules that protect against general vulnerabilities in web applications including those in OWASP publications.
- Anonymous IP list - blocks requests from services that obfuscate IP addresses. Tor, VPNs, etc.
- Amazon IP Reputation List - blocks requests based on IP address from those sources determined by Amazon Threat Intelligence.
- Known Bad Inputs - Contains rules that allow you to block request patterns that are known to be invalid and are associated with exploitation or discovery of vulnerabilities.

Others, including those created by third parties, explicitly block OWASP Top 10 vulnerabilities, high profile CVE vulnerabilities, and more.

**Rule Groups** are exactly what the name implies. If you want to manage / add multiple rules together, Rule Groups help organize them and allow you to apply all the associated rules to a Web ACL.

## Managing WAF Resources - Web ACL Capacity Units (WCUs)

Web ACL Capacity Units (WCUs) are used to manage operating resources used in the AWS WAF. Each task that is performed by the AWS WAF is weighted differently depending on the amount of processing power it takes to perform that task. WCUs are the unit of measurement for this and are reflected in the various rules, rule groups, and web ACLs as well. For example, a rule that checks for specified source IP addresses will use fewer WCUs than a rule that checks requests for a regex pattern.

![](/assets/img/posts/protecting-applications-using-aws-waf/05.png)
Notice the "Capacity" column available in the list of AWS Managed Rules. This reflects the number of WCUs for each rule / rule set. This will need to be kept in mind as you add rules to your web ACL as AWS enforces a maximum of 5,000 per web ACL.

A summary of important WCU rules to note:

- The maximum capacity of a Rule Group is 5,000 WCU.

- Note that the capacity is set at rule group creation and it cannot be changed after!

- The maximum capacity of a Web ACL is 5,000 WCU.
- Different Rules have different WCU requirements. Note these as you add rules to your Web ACL.

## AWS WAF Pricing

AWS has [a pricing page for AWS WAF](https://aws.amazon.com/waf/pricing/) that will update over time. This blog post likely won't, but it is current for the time it's being written.

![](/assets/img/posts/protecting-applications-using-aws-waf/06.png)
This is straight-forward enough, but one thing to note is that asterisk at the end of the "Request" pricing explanation.

*\* You will be charged an additional $0.20 per million requests for each 500 WCUs the Web ACL uses beyond the default allocation of 1500. In addition, you will be charged $0.30 per million requests for each additional 16KB analyzed beyond the default body inspection limit. For more information about default limits, see Developer Guide.*

AWS Managed Rules have additional charges in addition to these basic charges provided here.

## Body Inspection Limits

A long-time criticism of the AWS WAF has been its 8KB body inspection limit. Thankfully, this has been [increased by AWS to 64KB](https://aws.amazon.com/about-aws/whats-new/2023/04/aws-waf-body-inspections-amazon-cloudfront-distributions/) under most circumstances. Additional details on AWS WAF's [managing body inspection limits](https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-setting-body-inspection-limit.html).

By default, AWS will forward any request that exceeds the maximum request body size to the underlying resource. This has obvious security repercussions and has been blogged and PoC'd before (I won't link anything here, but feel free to Google it).

Thankfully, AWS has [written a guide](https://docs.aws.amazon.com/waf/latest/developerguide/waf-oversize-request-components.html) on blocking requests that exceed the maximum request body. This applies to the new maximum as well.

## Conclusion

The AWS WAF is easy to setup and apply to resources, but details become noteworthy when managing rules in ACLs and their associated WCUs, keeping track of pricing assuming you don't have an infinite budget, and we never even covered [logging](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html).