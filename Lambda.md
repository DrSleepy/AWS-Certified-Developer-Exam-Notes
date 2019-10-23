# Lambda

Lambdas are serverless, region based functions that run on demand.

1. Scales out (not up) automatically
2. Functions are independent, 1 event = 1 function
3. Multiple events can run in parallel
4. Can call other lambda(s)
5. 1,000 concurrent lambda executions per region (default)
   5.1 Exceeding the 1,000 limit will throw TooManyRequestsException (HTTP 429)
   5.2 Limit can be increased by contacting AWS Support Center
6. By default, lambda will not have access to any resources living inside a private subnet on a VPC.
   Lambda access must be configured:
   6.1 Private subnet ID
   6.2 Security ID (with required access)
   6.3 Lambda uses this information to set up Elastic Network Interface (ENI) using an available IP address from your private subnet

# Lambda - Triggers

1. API Gateway
2. AWS IoT (Internet of Things)
3. Alexa Skills Kit
4. Alexa Smart Home
5. Application Load Balancer
6. CloudWatch Events
7. CloudWatch Logs
8. CodeCommit
9. Cognito Sync Trigger
10. DynamoDB
11. Kinesis
12. S3
13. SNS
14. SQS

# Lambda - Supported Languages

1. Nodejs
2. Java
3. Python
4. C#
5. Go

# Lambda - Debugging

AWS X-Ray allows you to debug what is happening in a complex lambda architecture.
