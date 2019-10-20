# Simple Notification Service (SNS)

- SNS is a PUSH based system (SQS is a pull based system)
- Can push notifications directly to devices
- Can send SMS, email, SQS or a http endpoint
- Pay-as-you-go
- Can trigger lambda
- Pushlishes messages to topics
- One or many consumers can subscribe to topic
- Is a fan-out technology
  - 1 publisher, many consumers
- Messages are stored in multiple availability zones for high availability
