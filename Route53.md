# Route53

Route53 is Amazon's DNS (Domain Name System) service.
Registered domain names take up to 3 days to complete.

It allows you to map your domain names to the following services:

1. EC2 instances
2. Load Balancers
3. S3 Buckets

## Route53 Records

A Route53 record is simply mapping the domain name (abc.com) to a type of record

There are 12 different records:

1. A (address record)
2. AAAA (IPv6 address record)
3. CNAME (canonical name record)
4. CAA (certification authority authorization)
5. MX (mail exchange record)
6. NAPTR (name authority pointer record)
7. NS (name server record)
8. PTR (pointer record)
9. SOA (start of authority record)
10. SPF (sender policy framework)
11. SRV (service locator)
12. TXT (text record)

**Naked Domain Name / Zone Apex Record**

Both 'naked domain name' and 'zone apex record' mean the same thing
It simply means referring to a domain name without 'www'

## Alias Record

An alias record is created for the naked domain name and typically has a type of A or AAAA, but they work like a CNAME record.
You can create an alias record to route traffic to selected AWS resource such as an S3 bucket (configured to work as a website), ELBs, CloudFront and many other services.
