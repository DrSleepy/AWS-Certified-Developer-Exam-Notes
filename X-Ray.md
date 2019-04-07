# X-Ray

AWS X-Ray is a service that helps debug complex lambdas by collecting data about a request.
You can visualise your serverless application showing you what your performance bottlenecks are

# X-Ray - SDK Main Uses

1. Interceptors to add to your code to trace incoming HTTP requests
2. Client handlers to instrument AWS SDK clients that your application uses to call other AWS Services
3. A HTTP client to use to instrument calls to other internal and external HTTP web services

# X-Ray - Integration

Works with the following services:

1.  Elastic Load Balancing
2.  AWS Lambda
3.  API Gateway
4.  EC2
5.  Elastic Beanstalk

# X-Ray - Languages

1. Java
2. Go
3. Nodejs
4. Python
5. Ruby
6. .Net
