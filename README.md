Introduction:
Basic mode: free
Developer mode 29$/month: one contact can exange by email with support
Entreprise 100$/month: instant exchange 7/7 24/24 support for stratégique production purpose

IAM:
# IAM
- Region is global : universal
- root account completly admin
- new users have no permission by default
- new users have access key ID, secret key (for programmatic access) and password (fo console)

# BILLING ALARM
- CloudWatch and SNS (simple notification service)
- How can you get automatic auth for billing: Create billing alarm on cloudWatch and SNS  to send notification by email through a topic

# S3
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

# CloudFront
- A global universal service
- Edge location caching for different origins EC2, S3, Route53 etc.
- Distribution name of CDN a collection of Edge locations separate frm AWS Regions/AZ
- CloudFront can be used to delever entire website, dynamic static and streaming resources. Example: RTMP Meadia straeming (as Flash media etc), Web Distribution.
- Edge locations is not Read only, and has TTL for caching.
- Caching clear (invalidate cache) is charged


