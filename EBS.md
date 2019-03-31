# EBS - Elastic Block Storage

EBS is simply a hard disk (used for storage).
It works hand in hand with EC2 as EBS (or storage) are attached to EC2 instances.

1. Is used to store files on an EC2 instance or even run a DB on the EC2 instance amongst other things
2. EBS is highly available meaning its data is replicated into different availability zones in case of any failures on the primary
3. Root Device Volume - is the primary volume used on the instance and is not one of the replicated volumes

## EBS Volume Types

### SSD

1. General Purpose SSD (GP2) -
   1. Balances prices and performance
   2. Has a ratio of 3 IOPS per GB with up to 10,000 IOPS
   3. If you see a question in the exam saying you've got less than 10,000 IOPS, you probably want to pick GP2 Volume Type
2. Provisioned IOPS SSD (IO1) -
   1. Used for intensive applications such as a large relational or NoSQL database
   2. Use this is you need more than 10,000 IOPS

General rule:
Need under 10,000 IOPS? use GP2
Need more than 10,000 IOPS? use IO1

### Magnetic (HDD)

3. Throughput Optimized HDD (ST1) -
   1. Used for big data, data warehouse, log processing
   2. CANNOT BE USED AS ROOT VOLUME. MUST BE AN ADDITIONAL VOLUME
4. Cold HDD (SC1) -
   1. Lowest Cost Storage used for infrequent access
   2. CANNOT BE USED AS ROOT VOLUME. MUST BE AN ADDITIONAL VOLUME
5. Magnetic (Standard) -
   1. Is the lowest cost per GB of ALL EBS
   2. Legacy EBS that is used for infrequent access
   3. Is the only magnetic (HDD) that can be a root volume
