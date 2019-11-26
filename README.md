Introduction:
Basic mode: free
Developer mode 29$/month: one contact can exange by email with support
Entreprise 100$/month: instant exchange 7/7 24/24 support for stratégique production purpose

# IAM:
## IAM
- Region is global : universal
- root account completly admin
- new users have no permission by default
- new users have access key ID, secret key (for programmatic access) and password (fo console)

## BILLING ALARM
- CloudWatch and SNS (simple notification service)
- How can you get automatic auth for billing: Create billing alarm on cloudWatch and SNS  to send notification by email through a topic

## S3
- Safe place to store files
- Object based storage
- File can be from 0 to 5TB
- Files in buckets (folders)
- A bucket has a universal unique name and web adress
- consist of : key (name) value (content sequence of bytes), and version ID (for versionning), metadata (data about data), subresource (access control and Torrent)
- S3 data consistency:  Read after write is consistente (for puts) you'll be enable to read the data, evential consistency (for overwrite put and delete that can take time to propagate) you may get older version for a moment.
S3 SLA 99.99 availability, garanty, 99.9999999% durability
- S3 has : Tiered sotrage, lifecycle management, Versionning, Encryption, MFA delete, secure access through Access control list, and Bucket policies
- Storage CLasses: S3 std (same as discussed before), S3 - IA (Infrequently Access, lower fee but fast access when needed, charged for retreival fees) , S3 One Zone - IA (No data resilience through AZ, lower cost), S3 - IT (intelligent Riering: optimize costs moving data to must cost effective tier, whitout impact on performance), S3 Glacier (Archive, super cheap, retreival time form minutes to hours rather than milliseconds for others), S2 Glacier Deep Archive (lower cost, retreival within 12h)
- Charging: Storage, Requests, Storage  management Pricing, Data transfer, Transfer accelecratin, Cross Region Replicaiton
- S3 transfer acceleration from user to S3, use CloudFront edge location
- Bucket in region but S3 main dashboard is global
- Change storage class is possible on object or bucket
- Encryption: In transit (SSL/TLS), at rest server side enryption (SSE - S3, SSE - KMS key anagement servive, SSE - C Customer provided key)
- Versioning: Cannot be disabled once enabled, intergrates with lifecycle rules, allows MFA
- Uploading new version makes files not public access again, it changes permissions exept for old version
- Sum of bucket size, is some of versions of all the objects
- Delete an opbject it just make a delete marker, wich is a new version, old version keep saved. Deleting delete marker retores the file
- Lifecycle rule automate transition to tier sotrage, and manage expiry of objects and works with versionning buckets (applied to current and previous if selected)
- Replication can be done for all bucket or using prefix, on same or different account , during replication can change storage Classes
- Replication doesnt replicat old objects even when versionned. it replicates only new files and new version of old files
- REplication doesnt apply on delete marker

## CloudFront
- A global universal service
- Edge location caching for different origins EC2, S3, Route53 etc.
- Distribution name of CDN a collection of Edge locations separate frm AWS Regions/AZ
- CloudFront can be used to delever entire website, dynamic static and streaming resources. Example: RTMP Meadia straeming (as Flash media etc), Web Distribution.
- Edge locations is not Read only, and has TTL for caching.
- Caching clear (invalidate cache) is charged

## Snowball
- Snowball : tranfer huge amounts of data. 50Tb or 80T with encryption capacity
- Snowball edge : 100TB with computing capacities
- Snowball snowmobil : Exabytes of data
- Snowball can import and export to and from S3

## Storage Gateway
- virtual or physical appliance that connects on-promise datacenter to cloud storage.
- it comes also as vm for vmware exsi or Microsoft hyper-v
- it has three types : file Gateway as NFS/SMB than can be stored into s3, Volume Storage (block) as ISCSI that stores volumes (all data is stored backed up as S3 EBS into S3) as snapshots or only cached volume (that backsup only frequently accessed data, and Virtual Tape Lobriry (vtl) that backsup tapes into S3. 

# EC2
## INTRODUCTION
- Élastic compute resources
- 3 types of pricing: on demand by hour or second, reserved ( 1 to 3 years) then you pay as you go. less expensive ( it had 3 typez standard 75% less, convertible to change type of machine 54% less, and schedulable you reserve only scheduled time.
- many types of resources : FIGHTDRMCPXZAU F(financial analysis big data) I (IOPS fast storage as noSQL) G (GRAPHICS) H (High disk as DB) T ( low cost) D (Disk) R (High Ram) P (GRAPHICS) X (High RAM) Z (high ram and cpu) A (arm based) U (bar-metal)

## EC2
- root disk cannot be encrypted at starting time, else disks can
- terminating security is disabled by default. you need to enable it

## SG
- a security group rule takes effect immediately
- a security group is stateful, when inbound rule is createe outboud is created too (not showed tto interface)
- security groups disable everything by default, you can only allow
- in contrast NACL ((network access control list on vpc) allws to configure allow and block rules. and also it's stateful you need to configure inbound and outboud for each rule.

## EBS
- see image for types. [EBS types](https://github.com/saberkan/AWS/blob/master/Screenshot_2019-11-14-09-06-32-690_com.udemy.android.jpg)
- When creating an image from a volume you need to define virtualization tech. there is HVM (Hardware virt. machine) which the default and harware assistant virt., and Paravirtualization tech. 
- You may use hvm because it supports almost all type of instances while pv does not. 
- a volume is always in the same az than the instance. 
- root volume is deleted by default when instance terminated. others are not by default.
- volume type and size can be edited with out need to restart. 
- to migrate a volume EC2 to another az. you need to create image of it. then deploy it to another az. 
- to migrate a volume EC2 to another region. you need to take snapshot and then copy it to other region. 
- volume exists under ebs, and snapshots under s3

## AMI Types
- To lunch a EC2 instance, you can filter by architecture, OS, and storage type
- 2 types of storage, Block EBS from EBS snapshot, or Instance store volumes from a template (ephemeral storage).`
- You can add many instance stores at creating time, but not later in contrast of EBS
- You cannot stop instance store istance, you can only reboot or terminate
- If instance store instanec failed, you lose the data. When reboot you dont loose data.

## Encrypted root device
- Now you can create crypted device volume root
- At the beggining it wasn't the case, you had to create the instance, snapshot the volume, and copy the volume to encrypted volume, and create an instance form it.
- You cannot create an uncrypted snapshot from crypted volume
- you can share snapshots with other AWS accounts or public only if they are unencrypted

## CloudWatch
- Can monitor performance Compute resources (EC2, ELB, Autoscaling groups, Route 53 healthchecks), Sotrage (EBS, Storage gatways and cloudfront)
- on EC2 : CPU, NEtwork, Disk, Status check
- Be carreful to not be confused with CloudTrail (monitor api calls to AWS, audit) that increase AWS user actions not metrics, IP source from where the call was made
- Every 5mmin by default, you can put 1min by turning on detailed monitoring
- You can create alarms which trigger notifs
- You can create Dashboards, alarms, or source Events, and aggregate logs

## CLI
- CLI is universal with programmatic access
- .aws/credentials for storing credentials, and .aws/config for configuration

## IAM roles
- You can create roles and attach them to EC2 instance, user..
- Roles are more secure than storing access and secret key on isntance
- Role are made from policies, Version, Statement (Effect: Allow for example, Action, resource)

## Instance metadata
- inside instance run curl http://169.254.169.254/latest/user-data it shows the bootstrap script
- curl http://169.254.169.254/latest/meta-data/.. (many options network, metrics, local-ipv4, public-ipv4)
- metadata used to get information about instance

## EFS (elastic file system)
- support NFSv4
- you pay as you use no pre-provisionning required
- can scale to petabytes, can support thousands of concurrent NFS connections
- Data can be stored accross different AZ whithin region
- Read after write consistency
- file storage for EC2 (can be shared accross many instances)
- you can show AZ accross which EFS will be available in VPC
- you can enable lifecycle management, what to do if file where not accessed for x days, and where moving them
- you need to add inboud rule (2049)port nfs to access EFS from the EC2 
- you need to mount it folowing instructions given by aws
yum install amazon-efs-utils; sudo mount -t efs fs-xxx:/ /var/xxx, or nfs. you can use -o for tls encryption

## placement groups 
- A way to place EC2 instances
- Clustered placement group (group instances close together): group of instances whithing single AZ for application with low network latency, high network throughput or both. Only certain isntances can be in C. P. G. => when you want instance be close together within 1 zone.
- Spread placement group: distinct underlying hardware, for applications that have small number of critical instances that should be separated from each other. within multiple zones also
- Partitionned placement group: similar to S. I. G. ensure each parition within a placement group has it's own rack (netwok and power source), allowing to isolate impacte of harware failure.
- So basically 1 instance in spread placement, but many in Partitionned placement. that's the main difference.
- a clustered placement group can span multiple AZ. also can other types.
- name of placement group must be uique accross AWS account.
- only certain type can be launched in placement group (Compute optimized, GPU, memory optimized, storage optimized)
- you cant merge palcement group, and you can add exiting instance to placement group (create ami from existing instance and launch it into placement group)
- Spread placement groups have a specific limitation that you can only have a maximum of 7 running instances per Availability Zone

# Databases
## Intro
- RDS: relational databases. uses multizone for failover, and read replicas for performance
- read replicas has different url, and limit is 5.
- RDS: OLTP (ONLINE TRANSACTION PROCESSING) to make one business request (sql, mysql, postgres, oracle, aurora, mariadb)
- Dynamodb: non relational databases
- Redshift: datawarehouseing for BI
- Redshift: OLAP (ONLINE ANALYTICS PROCESSING) FOR MORE COMPLICATED QUERIES THAT NEEDS MANY REQUESTS
- ElasticCache: for caching most accessed information (memcached or redis) which improve performance of app.

## Backup and encryption
- read replicas can have read replicas.
- you can create read replicas for multizone db
- you can create replica to different zone or even region
- each replica has it's endpoint
- elasticcache and read replicas are used for performance. 
- replocas for heavy reading and elastic for same data reading
- there is 2 kind of backups : automated whithin a daily based has a retention from 1 to 35 days. it uses the last snapshot and applies transactions logs of the day to it. it backs up the data and all the transactions. then snapshot db stored into s3. 
- db encryption goes into all underlying read replicas and snapshots and automated backups. and uses aws kms
- the restored will be always a new Instance whith different endpoint.
- to apply read replicas, you need to enable backups firs
- a read replicas can be promoted to master but it breaks the replica
- aurora doesn't have multizone because it's has an resilient architecture already for dr (disaster recovery) and failover

## Dynamodb
- no sql
- spread across different regions
- stored on ssd storage
- has eventual consistency read as default for reading equal or more then a second after writing
- and strongly consistent read for les than one second read

## RDS
- uses node 160G, and adding to it until 180 nodes
- 1 leader and other computes. the leader does distribution of data and queries
- charged only on compute nodes. 
- backups from 1 to 35 days. 
- only on 1 az.
- keep at least 3 copies. original data, nodes replicas, and s3.
- can also asynchrounsly copy data to other region for DR.
- use encryption at transit time, and aes-256 at rest time.
- uses column compression since data is same type it takes less space than rds

## Aurora
- aws proprietary mysql db
- uses 2 replicas whithin each zone in 3 zones so 6 replicas
- handles write even whith 2 loses, and read at 3 loses
- you can make it as replicas of mysql db, or make mysql replicas for it but it impacts performance
- to migrate from mysql to aurora and visversa, 2 solution, create replicas and promote the replica, or create snapshot and create db from snapshot. 
- create snapshot allows also to create db into other aws account 

## Elasticache
- increase db and app performance
- uses memcached for horizontally scalling and simple use case
- or redis for scalling different types pf data sub/pub strategy, backups, multizone etc.
- exam question will be like how to increase db performance ( answer: by using replicas or cache)

# Route53
## DNS
- a résolution of domaine name goes through top level for example (.com) that gives a NS record to the domain registrar. and once in ns name server. 
we find a SOA (start of authority) that gives A recors for each domain and ip adress (PTR) for reverse. 
at that level you may find CNAME to resolve domaine name to another. but this doesn't work with apex records (toto.com) you need to use Alias record. 
- For exam ELBs doesn't have IP by default. you resolve them with DNS name
- For exam always choose alias record rather cname when it comes to ec2

## Register a domaine name
- you can buy it in Amazon
- it could take 3 days to appear in hosted zones

## Simple domaine record
- one domaine record to multiple ip adress. 
- the resolution is done randomly. be careful about ttl (the client dns keeps the same ip for ttl)

## Weighted routing policy
- Split traficc accorsing to weight, for example: 10% to us-east-1 and the rest to ue-east-1
- you can set healthchecks in individual records
- when EC2 fail healthcheck associated to the entry, it will not be served
- healthcheck can be associated to SNS record

## Latency based routing
- Balancing according to latency of user (region)
- health check can be attachd to every policy except simple

## Failover policy
- Active passive set up. if primary fails switch to secondary
- fail checked against healthcheck

## Geo-localisation routing
- where traffic will be send based on geographic location of user, for example queries from europe to europ ec2 etc.
- location can be done on continent or countries

## Geo-proximity
- You create complicated flows to to resources based on users location and resources.
- it uses trafic flows, You need to create a trafic policy

## Multivalue answer policies
- configure Route53 to return multivalues for each record.
- you can check the health on each resource, so route53  return only healthy resources
- Basically it's like simple but allows to attach healthcheck also


# VPC 
## Intro
- A logical section of aws cloud, allows you to create virtual networks
- you can do peering between vpcs but no transit peering
- by default 192.168/16 or 10.0.0.0/8 or 172.16.0.0/16 are private cidrs you can use

## labs
- when creating vpc, you get routing table, network acl and security groups created by default 
- then you need to create subnets, by default they don't have public ip assigned, thus you need to enable it if you want it to be accessible. 
- you can only have 1 internet gatway per vpc
- a subnet is attached to one availability zone
- sécuriy groups can't span vpc
- aws reserve 5 ips for e1ch subnet, one for breascast, one for network id, one for dns, one for router and one for future use
- to allow communication between private and public subnet, you need to attach a security group on the instance that allows the source (public subnet)

## NAT 
- to allow an instance from private subnet to access internet. you need to create a nat instance on public subnet, then create a for private subnet that goes to internet across the nat instance.
- nat instance is only a type of ec2 instances, nat gateway is a failover cluster of nat. both allows a private subnet to access internet.
