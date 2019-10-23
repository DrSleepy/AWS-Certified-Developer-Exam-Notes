# Simple Queue Service (SQS)

- SQS is a PULL based system (SNS is a push based system)
- Stores messages in a fail-safe queue to be processed by other services
  - fail-safe: messages will NOT be removed from the queue UNTIL it has been successfully processed
- Helps decouple services so they can run independently
- Can contain up to 256KB of data
  - data can be in any format such as JSON, XML, plain text etc
- SQS solves the issue that arises if the producer is producting work faster than the consumer can process it
- Helps a lot when working with non-serverless services to scale out
  - for example: You can provision another EC2 instance when the messages in the queue stack to over a 100
- Before being processed, messages remain in the queue from 1 minute to 14 days (default is 4 days)
- SQS queues are short-polling by default (expensive)
  - The consumer is constantly polling
  - Queue returns a response even if the queue is empty
- SQS queues has long-polling (cheap)
  - Reduces the amount of calls your consumer makes to the queue
  - Queue only returns a response once there is a message in the queue or the polling timeout is reached
  - maximum timeout is 20 seconds
- Pay-as-you-go

## Queue Types

**Standard Queue:**

- Standard queue is the default
- Allows you to have unlimited number of transactions per second
- Guarantees that a message is delivered at least once
  - Occasionally, more than one copy of a message might be delivered out of order
- Attempts to provide best-effor ordering which ensure that messages are generally deliver in the same order as they are sent, but NOT ALWAYS

**First-In First-Out (FIFO) Queue:**

- Order is strictly reserved
- Messages are only delivered one time
- Has no duplicate message in the queue
- Messages remain available in the queue until a consumer deletes it
- Supports message groups that allow multiple ordered messages within a single queue
- Limited to 300 transactions per second but have all the capabilities of the standard queue

**Delay Queue (This is a toggle - Not a seperate queue):**

- Delay delivery of new messages to a queue for a number of seconds
- Messages sent to the Delay Queue remain invisible to consumers for the duration of the delay period
- Default delay is 0 seconds, maximum is 900 (15 mins)

- Delay on Standard queue: changing the delay will only take affect on new messages incoming, not messages already on the queue
- Delay on FIFO queue: changing the delay will take affect on all new messages AND messages already in the queue

- Useful for delaying the sending of an email consisting of an online transactions to a customer

## Visibility Timeout

- When a consumer picks up a message, the message (still on the queue) becomes invisible
- If the consumer processed the message before the visiblity timeout runs out, it is then deleted from the queue
- If the consumer is not able to process the message within the visibility timeout, then the message is placed back onto the queue, which can result in the same message being delivered twice
- Default visibility timeout is 30 seconds
- Maximum visibility timeout is 12 hours
- Timeout can be increased with the 'ChangeMessageVisiblity' API call

## Managing Large messages (over 256KB to 2GB)

- Upload the queue messages to S3
- Configure SQS to read messages from S3
- Must use SQS extended Client Library (not available on normal SQS SDK)
