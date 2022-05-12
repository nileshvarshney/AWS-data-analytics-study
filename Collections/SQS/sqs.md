# Amazon Simple Queue Service (SQS)
- Fully managed Queing service
- Enable to decouple and scale microservices
- Eliminate the complexity and overhead associated with managing any queue
- Can send, store and receive messages between software components at any volume
- Standard SQS offer maximum throughput, best-effort ordering and at-least once delivery
- SQS FIFO designed to process message exactly once in the exact order that they were send.

## Standard Queue
- Unlimited throughputs
- At-least Once Delivery
- Best Effort Ordering

## FIFO Queue
- High Throughput - Support up to 300 Msg/S or If batched 10 messages per operation then 3000 Msg/s
- Exactly Once Processing
- First-In-First Out
- Name of the Queue end with .fifo

## Common SQL Features
- Payload Size 256KB of text in any format XML, JSON and unformatted text(limitation). 
- Using SQS extended Client (Java Library) and S3 send message size more than 256KB
- Send, receive or delete messages in batch of up to 10 message or 256KB
- Long Polling to save cost 
- Data retention from 1 minutes to 14 days, default retaintion 4 days.
- Send and read messages simultaneously.
- Server-side encryption (SSE) using (AWS KMS)
- Dead Letter Queues (DLQ) for not successfully processed message
- Availability 3 AZ
- No Parallel Consumption
- No MapReduce
- Auto Scaling 
- The visibility timeout is a period of time during which Amazon SQS prevents other consuming components from receiving and processing a message.

Use Cases:
- Decoupling application
- Buffer write to a database
- Handle Large load of message comming-in

*SQS can be integrated with Cloud Watch for autoscaling.*

### SQS - Consuming Message
- Poll SQS for message ( Upto 10 message at a time)
- Process the message within visibility timeout
- Delete the message after successful processing using Message ID and receipt handle.

### Securituy and reliability
- Stores all messages in multiple AZ of single Region
- Amazon SQS has its own resource-based permissions system (just like IAM)
- Amazon SQS supports the HTTP over SSL (HTTPS) and Transport Layer Security (TLS) protocols. 
- Server Size Encryption (SSE) using AWS KMS.
- SSE encrypt the body of message, and does not encrypt Queue metadata, message metadata and pre-queue metrics

### Compliance
- SQS PCI DSS Level 1 certified
- SQS HIPAA-eligible

* You can share a AWS SQS queue with other AWS user in another account. Message Queue owner will be responsible for pay. Message Queue is independent within region and they can not be shared in another region.

### Dead Letter Queue
A dead-letter queue is an Amazon SQS queue to which a source queue can send messages if the source queue’s consumer application is unable to consume the messages successfully. Dead-letter queues make it easier for you to handle message consumption failures and manage the life cycle of unconsumed messages. You can configure an alarm for any messages delivered to a dead-letter queue.




