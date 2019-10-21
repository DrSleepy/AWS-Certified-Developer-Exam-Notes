# CloudWatch

- CloudWatch is a monitoring service to monitor your AWS resources.
- Can be used on-premise

**What it can monitor:**

- Compute
  - Auto-scaling groups
  - Elastic Load Balancers
  - Route53 Health Checks
- Storage & Content Delivery
  - EBS Volumes
  - Storage Gateways
  - CloudFront
- Databases & Analytics
  - DynamoDB
  - Elasticache Nodes
  - RDS Instances
  - Elastic MapReduce Job Flows
  - Redshift
- Other
  - SNS Topics
  - SQS Queues
  - Opsworks
  - CloudWatch Logs
  - Estimated Charged on your AWS Bill

**Host Level Metrics - What is monitors by default on EC2:**

by default, it monitors Host Level Metrics which consist of:

- CPU (utilization)
- Network (throughput)
- Disk (I/O)
- Status Check

Anything that falls outside of the points above will fall under a 'custom metric'

**Custom Metrics / What it cannot monitor:**

It can only provide a general overview of what is being used,
but it cannot monitor details such as:

- Storage left / Storage available
- RAM utilization (unless setup as a custom metric)

Minimum granularity you can have on custom metrics is 1 minute

**How long CloudWatch Metrics are Stored:**

- use GetMetricStatistics API to retrieve metric statistics data
- Log data can be stored in CloudWatch Logs for as long as you want
- By default, CloudWatch Logs will store your log data forever
- Logs retention time for each Log Group can be changed
- You can retrieve datya from any terminated EC2 or ELB instance after its termination

**Metric Granularity:**

- Many default metrics for many default services are 1 minute
- But it can be 3 or 5 minutes depending on the service
- For custom metrics (such as RAM utilization) the minimum granularity you can have is 1 minute
- Standard monitoring is every 5 minutes
- Detailed monitoring is every 1 minute

**Alarms:**

- Alarms can be set to monitor any CloudWatch metric in your account including:
  - EC2 CPU Utilization
  - Elastic Load Balancer Latency
  - Charges on your AWS bill
- Thresholds can be set
- Actions can be set to take place if an alarm is triggered
  - Can send an SNS notification
  - Can trigger a Lambda function to delete your infrastructure
  - Much more

## CloudWatch vs CloudTrail vs AWS Config

**CloudWatch:**

- Monitors performance

**CloudTrail:**

- Used for auditing
- Monitors API calls
- Can see WHO made a table, S3 bucket, EC2 instance etc
- Can see WHEN that resource was made
- Can see WHAT resource was made
- Can see WHICH IP address provisioned it

**AWS Config:**

- Records the state of your AWS environment and can notify you of changes
- i.e Can tell you the rules of your security group from 3 weeks ago
