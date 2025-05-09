---
tags:
  - zerotomastery
  - aws
---

**Date created**: 2025-04-13
## Outline

- [[#Setting up an AWS Account]]
- [[#Section 1 Cloud Fundamentals|Cloud Fundamentals]]
- [[#Section 2 Security and Compliance|Security & Compliance]]
- Technology
- Billing and Pricing
- Exam Prep



## Setting up an AWS Account

>[!warning] If you forget your root password and cannot re-authenticate by any other means, you will be permanently locked out of your account. You will need to use a new email to create another account.

Initially, you will set up a root user with unrestricted access. Later, you will learn to create IAM users within the account with restricted access.

[Link to AWS Console](https://console.aws.amazon.com)


[[#Outline |to top ⤴️]]

## Section 1: Cloud Fundamentals

[ZTM Practice Quiz Answers](https://academy.zerotomastery.io/courses/learn-aws-cloud-practitioner/lectures/39263514)

#### Required components to run a website

- Compute: Servers
- Database: Usernames, customer information, inventory
- Storage: Images, Documents
- Network: Connect to users
- Security: Order info, credit card numbers

#### Moving to the Cloud

AWS solves the problem of reaching many users around the world by offering data centres in key places and 'pay for what you use' pricing models, creating reliable, maintainable, and scalable infrastructure.

#### Foundational Services

- The Compute service in AWS is called _Elastic Compute Cloud (EC2)_. Basically, the computers in the cloud. 
- The Database services are _Relational Database Service (RDS)_; i.e. PostgreSQL, SQLite, and _DynamoDB_ ; i.e. MongoDB. 
- The Storage service is _Simple Storage Service (S3)_
- The Networking Service is _Virtual Private Cloud (VPC)_
- The Security service is _Identity and Access Management (IAM)_, where you can create and manage internal users and permissions.

#### Benefits of the cloud

| **Term**                | **Description**                                                                                 | **Example**                                                                                        |
| ----------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| _Elasticity_            | The ability to adapt to workload changes (usually dynamic, short-term)                          | Amazon.com handling a huge spike in traffic on Prime Day                                           |
| _Scalability_           | The ability to handle increased workloads by adding resources (usually more static, long-term)  | Scale up a database because the size has grown over time                                           |
| _High availability_     | The ability to continue functioning even if some components fail                                | When a power outage causes one data center to go down, traffic is routed to another                |
| _Reliability_           | The ability to function consistently and correctly when expected                                | 99.99% uptime for EC2 instances during a given month                                               |
| _Agility_               | The ability to rapidly develop, test and launch applications to deliver business value          | Launch a new business application in days rather than months                                       |
| _Global reach_          | The ability to get closer to your customers through a global infrastructure                     | 26 geographic regions around the world                                                             |
| _Pay-as-you-go-pricing_ | Only pay for what you use, and only when you need it                                            | An EC2 instance only used for 2 hours; only pay for 2 hours                                        |
| _Economies of scale_    | Because of their size, AWS can purchase things more cheaply than an individual organization can | Amazon purchases servers at a fraction of the cost that you could, and pass the savings on to you. |

#### Economics of AWS

_Total Cost of Ownership_ = Upfront cost (Capital Expense "CapEx") + Cost to operate ("OpEx")
- AWS pays the CapEx and removes some of the OpEx

You can reduce your costs by using right-sized infrastructure through a customised EC2 machine, automating server on/off state, using AWS to handle compliance scope, and using Managed services such as RDS for creating databases instead of manually creating one.

#### AWS Well-Architected Framework

The AWS Well-Architected Framework is a framework for designing cloud systems in AWS with best practices in mind.

- [ ] Review [Foundational Pillars of AWS Cloud Adoption](https://aws.amazon.com/cloud-adoption-framework/) - specifically the Six Pillars and General Design Principles

**These 4 design principles are specifically called out**
- _Design for failure_: Assume that everything can failure and prepare just in case
- _Decouple components_: Components of a system should be capable of acting independently of each other
	- Example: A photo sharing app that fails if the photo-processing service fails. Also called a _monolithic_ or _tight coupling_ design approach.
	- Better Example: A photo sharing app that sends images to a queue where the photo-processing service polls for new images. If the service fails, the app is able to send to the queue for the service regains function. Also called a _microservices_ or _loose coupling_ approach.
- _Implement elasticity_: The system should scale itself to upwards to handle large amounts of traffic, as well as scale down to adjust to reduced demand.
- _Think parallel_: Instead of running one job for a long period on one server, split the work among more servers.

#### AWS Cloud Adoption Framework (CAF)

The Cloud Adoption Framework (CAF) leverages AWS experience and best practices to transform and accelerate business outcomes by using AWS.

- [ ] Complete CAF Assessment

![A diagram depicting AWS CAF foundational capabilities.](https://docs.aws.amazon.com/images/whitepapers/latest/overview-aws-cloud-adoption-framework/images/cloud-adoption-2.png)


[[#Outline |to top ⤴️]] 

## Section 2: Security and Compliance

### Shared Responsibility Model

You share responsibilities with AWS. You are responsible for security **IN** the cloud of customer data, access, operating systems, network & firewall configuration, authentication, network protection and more. AWS is responsible for Security **FOR** the cloud compute, storage, database, networking, availability, regions, edge locations and more. Responsibilities can vary depending on what managed services you use.


_Shared Responsibilities in various types of systems. AWS Managed highlighted in italics_

| **Infrastructure as a Service (IaaS)** | **Platform as a Service (PaaS)** | **Software as a Service (SaaS)** |
| -------------------------------------- | -------------------------------- | -------------------------------- |
| Applications                           | Applications                     | _Applications_                   |
| Data                                   | Data                             | _Data_                           |
| Runtime                                | _Runtime_                        | _Runtime_                        |
| Middleware                             | _Middleware_                     | _Middleware_                     |
| Operating System                       | _Operating System_               | _Operating System_               |
| _Virtualization_                       | _Virtualization_                 | _Virtualization_                 |
| _Servers_                              | _Servers_                        | _Servers_                        |
| _Storage_                              | _Storage_                        | _Storage_                        |
| _Networking_                           | _Networking_                     | _Networking_                     |

### Identity and Access Management (IAM)

> Identity and Access Managament (IAM) is the service used to securely control access to your AWS resources. It controls authentication (who) and authorization (what they can do)

>[!info] IAM Identity Center (formerly SSO) is a separate service that provides a single login across all AWS accounts (via AWS Organizations). This would allow you to, for example log into different accounts for testing and production, cloud-based applications such as Microsoft 365, EC2 instances running Windows, SAML 2.0-enabled applications. You can also use multiple identity providers, including the built-in, Okta, and Active Directory providers. 

#### IAM Users

>Services ➡️ IAM ➡️ Users ➡️ Create User

It is best practice when creating a user that will have access to the AWS Management Console to manage their access with Identity Center. However, recall that Identity Center requires setting up an Organization. For testing and small personal projects, creating an IAM user is easier. You should also enable prompting users to create a new password at the next sign-in (again, in production).


| **Root User**                     | **IAM User**                     |
| --------------------------------- | -------------------------------- |
| One per account                   | Multiple per account             |
| Unrestricted access               | Users can be deleted or disabled |
| Difficult to restrict or revoke   | Easy to restrict access          |
| _Can perform the following tasks_ |                                  |
| Close an AWS Account              |                                  |
| Change and AWS support plan       |                                  |
| Change AWS account settings       |                                  |

It is best practice to always work from an IAM account and not the root account unless absolutely necessary. The IAM should be setup with the minimum permissions required to complete the job. Do not create or delete any access keys for the root account. Finally, always enable multi-factor authentication.

[[#Outline |to top ⤴️]] 

#### IAM User Groups

User groups allow you to segment users into groups and apply different policies and permissions to them.

[[IAM User Groups]]
#### IAM Roles

An IAM role is similar to a user (an identity with permissions), except that they do not have passwords or keys, and can be assumed, temporarily, by anyone who needs it. 

Roles can be thought of as "hats"; i.e. Parent, Software Engineer, Home Chef. 

Roles are essential when a user needs customised access to different services. Instead of creating a new IAM user and hard-coding the user credentials, you **should** create custom roles for each application and assign the appropriate roles to your EC2 instance.

#### IAM Policies

A policy says who can do what to which resources and when.

_Example_: "Allow IAM users to rotate their credentials programmatically and in the console"
_Another example_: "Allow a user to start and stop an EC2 instance"

```json
// Sample policy

{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow", // default is "deny"
			"Action": [
				"ec2:StartInstances",
				"ec2:StopInstances"
			], // corresponds to an AWS API call
			"Resource": "arn:aws:ec2:*:*:instance/*", // The resource name you want to apply permission to. * is a wildcard.
			"Condition": {
				"StringEquals": {
					"aws:ResourceTag/Owner": "${aws:username}" // Optional named condition named with key/value pair
				}
			} 
		},
		{
			"Effect": "Allow",
			"Action": "ec2:DescribeInstances",
			"Resource": "*"
		}
	]
}
```

You can view policy permissions in either _Summary_ form or _JSON_ by going to IAM > Policies > Permissions. You can also see entities using the policy, version history, and the last accessed date.

>[!tip] It is recommended to not add policies directly to a User, but to a Group.

#### Multi-Factor Authentication (MFA)

Multi-factor authentication requires two or more "factors" to authenticate a user, such as password, phone/hardware token, or a fingerprint.

**Three types of MFA Devices**
- Virtual MFA device for smartphone or tablet (i.e. Google Authenticator, Authy, Microsoft Authenticator)
- Universal Second-Factor (U2F) Security Key (i.e. Yubikey)
- Other hardware MFA device (i.e. Gemalto)

>[!tip] It is best practice to use MFA on the root account and optionally for IAM accounts. You manage your MFA devices at Profile > Security Credentials

#### Access Keys and password policies

Access keys are required for programmatic access to AWS resources (such as using the AWS CLI). They can be found under IAM > Users > Security Credentials. Access keys should be created by IAM users (with the correct permissions), and not with the root user account. Keys cannot be retrieved if lost.

You can define a custom password policy from IAM > Account Settings > Change Password Policy.

### AWS Security, Identity, & Compliance Services

>[!tip] See the [AWS Exam Guide]([https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)) index for topics covered, including this one

#### AWS Shield

A **Distributed Denial of Service (DDoS)** attack is when a malicious party uses multiple infected computers to make millions or billions of request to a website, overloading the server by preventing requests from being received or delivered.

**AWS Shield** includes a free standard service to protect all customers from most common DDoS attacks, while the advanced version protects against more sophisticated attacks and integrates with other services like Cloudfront, Route 53, and Elastic Load Balancing. Advanced also includes AWS Web Application Firewall (WAF) at no cost.

#### AWS Web Application Firewall (WAF)

**AWS Web Application Firewall** lets you:
- Configure rules to allow, block, monitor/count requests.
- Set rules for IP addresses, country of origin, presence of a script, URL strings, etc.
- Examples: Blocking known IP addresses of hackers, rate-limiting incoming requests

#### AWS Key Management System (KMS)

| **At Rest**                                | **In Transit**                                       |
| ------------------------------------------ | ---------------------------------------------------- |
| Data that's stored or archived on a device | Data being transferred from one location to another  |
| _Examples_                                 | _Examples_                                           |
| _S3 bucket_                                | _Moving data from an EC2 instance to an S3 bucket_   |
| _Hard disk_                                | _Moving data from an on-premises data center to AWS_ |
| _Database_                                 |                                                      |

Encryption uses algorithms to encrypt and decrypt information. The key is what is used to decrypt the message. The **AWS Key Management System** manages the encryption hardware, software and keys, as well as integrating with many AWS services.

The **AWS CloudHSM** or **Hardware Security Module** is a service where AWS provisions the hardware and you manage everything else. In this service, AWS cannot access or recover your keys. It is considered more secure than AWS KSM.

##### Types of Keys

| **AWS Managed**         | **Customer Managed**                | **Custom Key Stores** |
| ----------------------- | ----------------------------------- | --------------------- |
| AWS creates and manages | You (customer) create and manage    | Created with CloudHSM |
| _Used by AWS Services_  | Can create policies to rotate keys  | You own and manage    |
| - aws/lambda            | Specify who can use and manage keys |                       |
| - aws/cloud9            | Supports "bring your own key"       |                       |
| - aws/s3                |                                     |                       |
>[!warning] Keys cannot be deleted immediately, you must define a minimum waiting period of 7 - 30 days.

#### AWS Certificate Manager (ACM)

Certificates are used to identify a server as reputable and ensures communication between the user and server is encrypted. This uses what is called Transport Layer Security, which replaces Secure Sockets Layer (SSL)

**AWS Certificate Manager (ACM)** allows you to provision, manage, and deploy public and private SSL/TLS certificates.

#### AWS Secrets Manager

**AWS Secrets Manager** is the recommended way to protect secrets (e.g., user names, passwords, API keys) needed by your applications and services. It is a paid service.

It is best practice to rotate your secrets when presented with the option.

#### Amazon Macie

Personally Identifiable Information (PII) is any information that can be used to identify a person, such as name, email address, phone number, etc. Compliance rules state how this information should be protected.

**Amazon Macie** works with the S3 Storage buckets by identifying and analyzing PII data using machine learning and pattern matching and using its findings to automate workflows and remediation (into CloudWatch or EventBridge, for example).

#### Amazon Inspector

**Amazon Inspector** automates scans EC2 Instances and ECR Repositories for software vulnerabilities and network exposure, assigns a risk score, and integrates with Security Hub and EventBridge for automated workflows.

#### Amazon GuardDuty

**Amazon GuardDuty** continuously analyses network, account, and data access from Cloudtrail Managament, S3 events, VPC Flow, and DNS Logs, then uses machine learning to identify and prioritise threats, and finally automates workflows with Cloudwatch and Lamda functions.

#### AWS Config

**AWS Config** allows you to inventory, record and audit the configuration of your AWS resources. 

_For example you can:_
- Inventory all your S3 buckets, and when one of them becomes publicly accessible, receive an alert.
- Receive an alert when an unauthorised port opens on a security group
- During a compliance audit, show when configurations change

It is a paid service.

#### AWS Security Hub

**AWS Security Hub** pulls everything together into a consolidated place where you can view and take actions on security issues.

It requires [[Zero to Mastery - AWS Certified Cloud Practitioner#AWS Config | AWS Config]], works across accounts, and aggregates data from many other services. It is also a paid service.

#### Amazon Detective

**Amazon Detective** works with the findings of [[Zero to Mastery - AWS Certified Cloud Practitioner#Amazon GuardDuty|Amazon GuardDuty]], CloudTrail logs, and VPC Flow logs during an incident response to automatically distil and organise data into a graph model.

It builds a linked set of data using machine learning, statistical analysis, and graph theory. This data can be used to provide visualisations, context, and detailed findings in Security Hub or GuardDuty to locate the root cause of the issue.

#### AWS Artifact

**AWS Artifact** is a free self-service portal to access AWS's internal compliance reports and agreements.

[[The Var Keyword]]

## Section 3: Technology

### Technology

#### Ways to Work with AWS

You can work with AWS in the following ways:
1. The AWS Console - *seen previously*
2. The AWS SDK (Software Developer Kit) 
3. Command Line Interface (CLI)
4. AWS Cloudshell (CLI in the browser)

#### Installing the CLI

Google search for *AWS CLI download* and choose the latest version for your system.

Confirm the installation using `aws --version` in the terminal.

#### Configuring the CLI

You must first configure your credentials by running aws configure to run any commands. It will then ask for:
1. AWS Access Key ID
2. Secret Access Key
3. Default region
4. Output format

The Access and Secret keys can be generated in IAM (Be sure to be logged in as an IAM user, not root). You may only have a maximum of two keys at any given time. The region is located in the top right dropdown of your AWS Console. The output format can be `json` (default), `yaml`, `stream`, `text`, or `table`.

*Sample Commands*
`aws s3 ls` - List S3 buckets
`aws iam list-users` List IAM users

> [AWS CLI Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)

#### AWS Cloudshell

You can access AWS Cloudshell from the terminal icon at the top right of the AWS Console. It may not be available in all regions.
### Compute

### Storage

### Networking & Content Delivery

### Databases

### Analytics

### Deploying/Managing Infrastructure

### Monitoring

### Support

## References / Sources

[AWS Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)
[AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
[Foundational Pillars of AWS Cloud Adoption](https://aws.amazon.com/cloud-adoption-framework/)
[AWS Shared Responsibility Model] [https://aws.amazon.com/compliance/shared-responsibility-model]
[AWS Security, Identity and Compliance Products](https://aws.amazon.com/products/security](https://aws.amazon.com/products/security)


