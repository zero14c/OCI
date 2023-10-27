## Overview of Queue
___`Oracle Cloud Infrastructure (OCI) Queue`__ is a __`fully managed serverless service`__ that helps __`decouple systems`__ and enable __`asynchronous operations`__. 
Queue handles __`high-volume transactional data`__ that requires independently processed messages __`without loss or duplication`__. Queue supports transparent, 
__`automatic scaling`__ based on throughput for __`producers`__ and __`consumers`__. 
Queue uses __`open standards`__ to support communication with any client or producer with minimal effort.

The OCI Queue service is built on __four principles__:

__`Publishing`__
Messages can be published to a queue by one or more producers, each with a retention period. 
If retention isn't specified, the message expires using a retention period defined at the queue level. 
A message contains a payload in the form of a string.

__`Consuming`__
Multiple consumers can consume messages from a single queue. 
Consumer count can scale along with the rate of messages being published. 
After a message is delivered to a consumer, the message is hidden from other consumers for a pre-defined amount of time, 
which is known as its visibility timeout.

__`Updating`__
If processing a message takes longer than expected, 
consumers can extend the visibility timeout of a message. 
Extending the visibility timeout prevents the message from being returned to the queue and being delivered to another consumer.

__`Deleting`__
After a message has been delivered to and processed by a consumer, 
the message must be deleted to prevent redelivery to another consumer.

### Benefits
The Queue service provides the following benefits.

#### Application Decoupling
Queue helps decouple applications and systems by using event-driven architecture. 
Decoupling ensures that individual application components can scale independently and that as new application components get built, 
they can publish or subscribe to the queue.

A diagram representing a producer sending messages to multiple queues consumed by a consumer.

#### Reliable Message Processing
Queue guarantees that a message is never lost, even if the consumer is unavailable for consumption. A published message is persistent until it's either deleted or expired.

If a message isn't consumed successfully, it's sent to a dead letter queue (DLQ). 
Dead letter queues let you isolate problematic messages to determine why they're failing. 
Isolating and consuming problematic messages in this way can guarantee successful delivery to a consumer application at least once. 
See Dead Letter Queues for more information.

#### Open Standards
Queue can be called using RESTful API (with an Open API specification) definition or by using the industry standard STOMP protocol.
