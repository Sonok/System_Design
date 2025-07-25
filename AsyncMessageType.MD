# Asynchronous Messaging Patterns

Asynchronous messaging patterns are communication techniques that allow systems and services to interact without blocking operations, enabling scalability, fault tolerance, and better resource utilization. These patterns rely on messaging systems to handle the exchange of data.

---

## 1. Message Queuing (Point-to-Point)

In the **message queuing** pattern, a producer sends messages to a queue. Each message is consumed by only one consumer.

- **Producer**: Sends the message.
- **Queue**: Holds messages until they are processed.
- **Consumer**: Retrieves and processes messages.

**Behavior**: Only a single consumer receives each message.

**Use Case**: Background jobs, video processing pipelines, task offloading.


---

## 2. Publish/Subscribe (Pub/Sub)

In the **publish/subscribe** pattern, messages are sent to a topic by a publisher. All subscribers to that topic receive a copy of the message.

- **Publisher**: Sends messages to a topic.
- **Topic**: A logical channel for message delivery.
- **Subscribers**: Receive messages from the topic.

**Behavior**: Every subscriber receives a copy of the same message.

**Use Case**: Broadcasting notifications, event-driven systems.


---

## 3. Queueing Model vs. Pub/Sub Model



- **Queueing Model**:
  - Used for point-to-point communication.
  - A video uploader sends metadata to a queue.
  - A transcoder processes it.
  - Object storage is used to store video bytes.

- **Publish/Subscribe Model**:
  - After transcoding, the metadata is published.
  - Multiple systems (database, cache, notification service, CDN) subscribe and receive the metadata.

---

## 4. Competing Consumers

This pattern supports **parallelism and scalability** by allowing multiple consumers to compete for messages from the same queue.

- **Multiple transcoders** pull tasks from the queue.
- Messages are processed in parallel.
- System continues to work even if some consumers fail.
- More instances can be added to handle increased load.

This improves **performance**, **availability**, and **scalability**.


---

## 5. Request/Response Messaging

This pattern enables asynchronous communication while still allowing the sender to receive a response.

- **Request message** includes:
  - `replyTo`: The callback queue name.
  - `correlationId`: A unique identifier to match the response.
- The **response message** includes:
  - The same `correlationId`.

Useful for workflows where a reply is expected but blocking behavior is undesirable.



---

## 6. Priority Queue

The **priority queue** pattern allows messages to be processed based on priority levels.

### Two approaches:

1. **Native Priority Queue Support**:
   - Messages have priority levels (e.g., 1, 2).
   - A single queue holds all messages, and consumers prioritize based on embedded priority.

2. **Separate Queues for Each Priority**:
   - Each priority level has a dedicated queue.
   - Higher priority queues can be serviced by a larger pool of instances.

This allows urgent messages to be processed faster.


---

## 7. Claim Check Pattern

The **claim check** pattern solves the issue of **large message sizes**.

### Problem with Large Messages:
- Messaging systems have size limits.
- Large messages can degrade performance and memory usage.

### Solution:
- The actual payload (e.g., a large video) is stored in shared storage.
- A small message (containing a reference to the large message) is sent through the queue.
- The consumer retrieves the actual data from storage.

This optimizes messaging system performance.





---
