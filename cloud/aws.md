## AWS

#### VPC
A VPC (Virtual Private Cloud) is a virtual network logically isolated from other
virtual networks in the AWS cloud. You can control whether the network is
directly routable to the Internet.

Within a VPC, you have complete control over your virtual networking
environment, including selection of your own IP address range, creation of
subnets, and configuration of route tables and network gateways.

A subnet specifies a particular range of IP addresses and exists within an AZ.
A public subnet is exposed to the Internet, while a private subnet is
unreachable from the Internet.

For example, you can create a public-facing subnet for your webservers that has
access to the Internet, and place your backend systems such as databases or
application servers in a private-facing subnet with no Internet access.



<br />
#### Amazon EC2
Amazon Elastic Compute Cloud (EC2) is a web service that provides resizable
computing capacity in the cloud.

* You can increase or decrease capacity within minutes.
* You have root access to each of your instances.
* You can choose among multiple *instance types*, hardware specs, OS and such.
* 99.95% availability SLA.

An EC2 instance have a private IP address, only visible within the VPC. It might
also have one or several public IP addresses.

Each EC2 instance is placed into a particular subnet.

<br />
#### AMI
An Amazon Machine Image (AMI) is a template that contains a software
configuration (OS, application server, other apps). From an AMI you can
launch an *instance* which is a copy of the AMI running as a virtual server
on a host computer in Amazon's data center.

When you launch an instance, you select the *instance type*.

You can assign your instance using its public dns name or public IP address.

<br />
#### Security group
A security group acts as a firewall for your instance. It controls inbound
and outbound traffic. You can specify multiple security groups when you
launch your instance.

![alt tag](http://docs.aws.amazon.com/gettingstarted/latest/awsgsg-intro/images/security_group.png)

<br />
#### Amazon Route 53
It is a highly available and scalable cloud DNS web service.
It allows you to route your visitors to your websites by translating a domain
name (www.mywebsite.com) to the IP address of your instance.

You can register your domain name within Route 53 and map it to an AWS
resource.

<br />
#### Auto scaling
Helps you maintain application availability and allows you to scale your EC2
up or down automatically according to conditions you define.

Auto scaling can increase the amount of EC2 instances during demand spikes
and decrease capacity during lulls to reduce costs.

<br/ >
#### ELB
Elastic Load Balancing distributes incoming application traffic across multiple
EC2 instances.

ELB ensures that only healthy EC2 instances receive traffic by detecting
unhealthy instances and rerouting traffic across the remaining healthy
instances.

ELB automatically scales its request handling capacity to meet the demands
of application traffic.

It offers integration with Auto Scaling.

<br />
#### S3
Amazon Simple Storage Service is a data storage service that handles vast
amounts of data and large number of concurrent requests.

You store your data in containers called buckets. You can set up permissions
per bucket. A bucket can contain any number of objects of any type.

You can group objects using folders. The folder is part of the key of an object.
You can of course have a tree of folders.

You can access an object via the URL:
http(s)://domain/bucket_name/object_key

Domain is either `s3.amazonaws.com` or `s3-region-code.amazonaws.com`.

<br />
#### Amazon RDS
Provides a fully-managed relational database that scales to large
datasets. It is easy to scale the database storage and compute resources
and provide read replicas. Choose between MySQL, PostgreSQL and others.

A DB instance is the basic building block of RDS. It is an isolated database
environment in the cloud. When you launch a DB instance, you select the DB
engine and the hardware specs of the instance. You also specify a security
group for it.

<br />
#### Regions and Availability Zones
Amazon EC2 is hosted in multiple locations world-wide.

Each _region_ is a separate geographic area.

Each region has multiple, isolated locations known as _AZ_. The AZs within a
region are connected via low-latency links. There is no such connection between
regions.

When you launch an instance, you can select an AZ or let AWS
choose one for you. If you distribute your instances across multiple
AZs and one instance fails, you can design your application so that an instance
in another AZ can handle requests.

<br />
#### CloudFormation
AWS CloudFormation gives developers and systems administrators an easy way
to create and manage a collection of related AWS resources, provisioning and
updating them in an orderly and predictable fashion.

It is a way to capture everything you can do in the AWS Web Console as a single
JSON file. This means you can "version control" and "code review" your AWS
infrastructure settings.

*OpsWorks* accomplishes the same infrastructure management as CloudFormation,
but at one higher level of abstraction, and with a special focus on application
deployment.

*Elastic Beanstalk* accomplishes the same infrastructure management as
CloudFormation and OpsWorks, but at the highest level of abstraction.

<br />
## Tips

#### Multi-AZ for high availability
An EC2 instance can fail for several reasons:
* the instance itself could fail, or its underlying hard drive volume could
become corrupted.
* The physical machine on which the EC2 instance resides could fail.
* The data center within which the physical machine is located could fail.

You should assume that any of the above will eventually happen. If you run
your service on a single EC2 instance in a single AZ, your service will be
down when any of those failures happen. That is why you should run your services
across multiple AZ.

<br />
## Resources
http://docs.aws.amazon.com/gettingstarted/latest/awsgsg-intro/awsgsg-intro.pdf
https://www.airpair.com/aws/posts/building-a-scalable-web-app-on-amazon-web-services-p1
