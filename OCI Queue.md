## Overview of Queue
__`Oracle Cloud Infrastructure (OCI) Queue`__ is a __`fully managed serverless service`__ that helps __`decouple systems`__ and enable __`asynchronous operations`__. 
Queue handles __`high-volume transactional data`__ that requires independently processed messages __`without loss or duplication`__. 
Queue supports transparent, __`automatic scaling`__ based on throughput for __`producers`__ and __`consumers`__. 
Queue uses __`open standards`__ to support communication with any client or producer with minimal effort.

__`Oracle Cloud Infrastructure (OCI) Queue`__ 
is a __`fully managed serverless service`__ 
helps __`decouple systems`__ and enable __`asynchronous operations`__.
handles __`high-volume transactional data`__ that requires independently processed messages __`without loss or duplication`__.
__`automatic scaling`__
uses __`open standards`__

The OCI Queue service is built on __four principles__:

__`Publishing`__
Messages can be published to a queue by one or more __producers__, each with a __retention period__. 
If retention isn't specified, the message expires using a retention period defined at the queue level. 
A __message__ contains a __payload__ in the form of a string.

__`Consuming`__
Multiple __consumers__ can consume messages from a single queue. 
Consumer count can scale along with the rate of messages being published. 
After a message is delivered to a consumer, the message is hidden from other consumers for a pre-defined amount of time, 
which is known as its __visibility timeout__.

__`Updating`__
If processing a message takes longer than expected, 
consumers can __extend the visibility timeout of a message__. 
Extending the visibility timeout prevents the message from being returned to the queue and being delivered to another consumer.

__`Deleting`__
After a message has been delivered to and processed by a consumer, 
the message must be __deleted to prevent redelivery__ to another consumer.

### Benefits
The Queue service provides the following benefits.

#### Application Decoupling
Queue helps __`decouple applications`__ and systems by using __`event-driven architecture`__. 
Decoupling ensures that individual application components can __`scale independently`__ and that as new application components get built, 
they can publish or subscribe to the queue.

![A diagram representing a producer sending messages to multiple queues consumed by a consumer.](https://docs.oracle.com/en-us/iaas/Content/queue/images/queue-overview.png)

#### Reliable Message Processing
__Queue guarantees that a message is never lost__, even if the consumer is unavailable for consumption. 
__A published message is persistent until it's either deleted or expired.__

If a message isn't consumed successfully, it's sent to a __`dead letter queue (DLQ)`__. 
Dead letter queues let you isolate problematic messages to determine why they're failing. 
Isolating and consuming problematic messages in this way can guarantee successful delivery to a consumer application at least once. 
See Dead Letter Queues for more information.

#### Open Standards
Queue can be called using __RESTful API__ (with an Open API specification) definition or by using the industry standard __STOMP protocol__.

### Concepts
The Queue service uses the following concepts.

#### message
A message is an element in a queue that contains a __`payload`__ in the form of a __`string`__. 
The string can be in any format, including XML, JSON, CSV, a Base64-encoded binary message, and even compressed formats such as gzip. 
Producers and consumers should agree upon the message format. Each message is processed independently.

#### producer
A client which sends messages to the queue.

#### consumer
A client which receives messages from a queue. The consumer is also responsible for deleting messages from the queue after the messages are received.

#### channel
An ephemeral destination within a queue that can be created on demand. 
Messages can be published to a specific channel within a queue, 
and consumers can retrieve messages from specific channels. For more information, see Channels.

#### maximum retention period
The length of time that a queue retains a message until the message is automatically deleted by the system, if not deleted by a consumer. Maximum retention period is configurable to values of 10 seconds to 7 days at the queue level. The default value is 1 day.

#### delivery count
The number of times that a message is delivered to a consumer upon request.

#### maximum delivery attempts
The number of times that a message is delivered to a consumer, but not updated or deleted, before it's sent to a dead letter queue (DLQ). Maximum delivery attempts is configurable to values of 1-20 at the queue level. For more information, see delivery count.

#### polling timeout
The length of time that a consumer will wait for messages to consume. Increasing the polling timeout reduces the number of times a consumer requests messages from the queue but the response indicates that there are no available messages to consume. Polling timeout is configurable to values of 0 to 30 seconds at the queue level, and consumers can set the value when requesting messages. The default value is 30 seconds. For more information, see long polling.

#### visibility timeout
The length of time during which a message received from the queue by one consumer isn't visible to other consumers. Visibility timeout is configurable to values of 1 second to 12 hours at the queue level, and consumers can set the value when requesting messages. The default value is 30 seconds. For more information, see message locking.

#### visible messages
The number of messages currently in a queue that are available for consumption.

#### in-flight messages
The number of messages delivered to a consumer but not yet deleted. In-flight messages are unavailable for redelivery until their visibility timeout has passed.

#### dead letter queue
If a message isn't consumed successfully, and has more delivery attempts than the configured maximum delivery attempts, the message is transferred to a dead letter queue (DLQ). For more information, see Dead Letter Queues.

### Guarantees
The Queue service provides the following guarantees.

- A successfully published message is guaranteed to be durable until it's either deleted or its retention period has passed. The publication of a message is considered successful when the Queue service sends back an acknowledgment to the producer. It does not matter whether the response was received.
- A message within the visibility timeout is guaranteed not to be delivered to another consumer until that timeout expires.
- A message will not be deleted by the Queue service before its retention period is over. A consumer can process and delete a message during its retention period.

### Authentication and Authorization
Each service in Oracle Cloud Infrastructure integrates with IAM for authentication and authorization, for all interfaces (the Console, SDK or CLI, and REST API).

An administrator in your organization needs to set up groups, compartments , and policies  that control which users can access which services, and which resources, and the type of access they have. For example, policies control who can create users, groups, and compartments, or who can create and manage virtual deployments.

- If you're a new administrator, see Getting Started with Policies.
- For details about writing policies for this service, see Queue Policies.
- For details about writing policies for resources in other services, see Policy Reference.

### Ways to Access Queue
You can access Queue by using the Console (a browser-based interface), Oracle Cloud Infrastructure CLI, or REST APIs.

Instructions for all three methods are included throughout this guide.

- The OCI Console is an easy-to-use, browser-based interface. To access the Console, you must use a supported browser.
- The REST APIs provide the most functionality, but require programming expertise. API Reference and Endpoints provide endpoint details and links to the available API reference documents including the Queue APIs.
- OCI provides SDKs that interact with Queue.
- The Command Line Interface (CLI) provides both quick access and full functionality without the need for programming.
- To use the OCI CLI or REST APIs, you can either set up your environment, or use Oracle Cloud Infrastructure Cloud Shell.
    - To use the CLI or REST APIs in Cloud Shell, sign in to the Console. See Using Cloud Shell and the OCI CLI Reference.
    - To install the OCI CLI in your environment, follow the steps in the Install CLI Quickstart.
    - When using REST APIs, refer to REST API documentation and API Reference and Endpoints.

### Service Limits
When you sign up for Oracle Cloud Infrastructure, a set of service limits is configured for your tenancy. The service limit is the quota or allowance set on a resource. Review the following service limits for Queue resources.

Resource |	Details
-|-
Queues |	10 per tenancy per region
Channels per queue |	256 per queue
Maximum PutMessage request size	|512 KB and 20 messages
Maximum GetMessage response size	|2 MB and 20 messages
Maximum message size	|128 KB
Maximum number of in-flight messages	|100,000 per queue
Maximum messages per queue	|Unlimited 
Message retention	|Maximum: 7 days<br>Minimum: 10 seconds<br><br>Default: 1 day
Message visibility timeout |	Maximum: 12 hours<br>Minimum: 0 seconds at message level<br>Minimum: 1 second at queue level<br><br>Default: 30 seconds
Maximum concurrent GET requests	|1,000 requests per second per queue
Maximum message operations	|1,000 requests per seconds per API per queue
Maximum data rate	| Ingress per queue: 10 MB/s<br>Egress per queue: 10 MB/s
Polling timeout	| Maximum: 30 seconds<br>Minimum: 0 seconds
STOMP throughput |	10 MB/s per STOMP connection
Storage	|20 GB per tenancy<br>2 GB per queue

See Service Limits to learn more about service limits and find instructions for requesting a limit increase. To set compartment-specific limits on a resource or resource family, administrators can use compartment quotas.



Overview of Policy Syntax
The overall syntax of a policy statement is:

allow <subject> to <verb> <resource-type> in <location> where <condition>
For example, you can specify:

A group or dynamic group by name or OCID as the <subject>. Or, you can use any-user to cover all users in the tenancy.

inspect, read, use, and manage as the <verb> to give a <subject> access to one or more permissions.

As you go from inspect > read > use > manage, the level of access generally increases, and the permissions granted are cumulative. For example, use includes read plus the ability to update.

A family of resources such as virtual-network-family for the resource-type. Or, you can specify an individual resource in a family such as vcns and subnets.

A compartment by name or OCID as the <location>. Or, you can use tenancy to cover the entire tenancy.

One or more conditions in <condition>, which must be met for access to be granted. For multiple conditions, you can use any or all.

A condition consists of one or more variables. A variable can be relevant to the request itself (for example, request.operation) or to the resource being acted upon in the request (for example, target.queue.id). To illustrate, to allow a group to manage a specific workspace and not any other workspace:

allow group <group-name> to manage queues in compartment <compartment-name> where target.queue.id = '<queue-ocid>'
Or, to allow a group to manage all Queue resources in the tenancy:

allow group <group-name> to manage queues in tenancy
For more information about creating policies, see Getting Started with Policies and Policy Reference.

Resource-Types
To give users access to Queue resources, create IAM policies with Queue resource types.

For access to all Queue resources, use the queues resource type.

If you don't want users to manage queues, but you do want them to produce to a queue or consume from a queue, use the following individual resource types:

queue-push
queue-pull
See Policy Examples for more information.

Supported Variables
The Queue service supports all the general variables, plus those listed here.

For more information about general variables supported by OCI services, see General Variables for All Requests.

Variable	Variable Type	Source
target.queue.id	Entity (OCID)	Request
Details for Verbs + Resource-Type Combinations
There are various Oracle Cloud Infrastructure verbs and resource-types that you can use to create a policy.

The following tables show the permissions and API operations covered by each verb for Queue. The level of access is cumulative as you go from inspect to read to use to manage. A plus sign (+) in a table cell indicates incremental access compared to the cell directly above it, whereas "no extra" indicates no incremental access.

queue
queue-push
queue-pull
Permissions Required for Each API Operation
The following table lists the API operations for Queue in a logical order, grouped by resource-type.

The resource-types are queues, queue-push, and queue-pull.

For information about permissions, see Permissions.

Required Permissions
API Operation	Permissions Required to Use the Operation
ListQueues	QUEUE_INSPECT
CreateQueue	QUEUE_CREATE
GetQueue	QUEUE_READ
DeleteQueue	QUEUE_DELETE
MoveQueue	QUEUE_MOVE
UpdateQueue	QUEUE_UPDATE
ListWorkRequests	QUEUE_INSPECT
GetWorkRequest	QUEUE_READ
ListWorkRequestErrors	QUEUE_INSPECT
ListWorkRequestLogs	QUEUE_INSPECT
GetStats	QUEUE_READ
PutMessages	QUEUE_PRODUCE
GetMessages	QUEUE_CONSUME
UpdateMessage	QUEUE_CONSUME
DeleteMessage	QUEUE_CONSUME
Policy Examples
Learn about Queue IAM policies using examples.

For administrators, the following policy lets the specified group do everything with queues and related Queue service resources:

Allow QueueManagers to manage queues in compartment <compartment_name>
Use the following policies to let a specified group produce to or consume from a queue:

Allow QueueProducers to use queue-push in compartment <compartment_name>
Allow QueueConsumers to use queue-pull in compartment <compartment_name>
Use the following policy to let a specified group inspect and read queue details:

Allow QueueReaders to read queues in compartment <compartment_name>

