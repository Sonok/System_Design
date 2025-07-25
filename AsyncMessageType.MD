# Asynchronous Messaging Patterns

Asynchronous messaging patterns are communication techniques that allow systems and services to interact without blocking operations, enabling scalability, fault tolerance, and better resource utilization.

---

## 1. Message Queuing (Point-to-Point)

In this pattern, a producer sends messages to a queue, and each message is consumed by only one consumer.

```mermaid
sequenceDiagram
    participant Producer
    participant Queue
    participant Consumer

    Producer->>Queue: Send message
    Queue->>Consumer: Deliver message
```

---

## 2. Publish/Subscribe (Pub/Sub)

In this pattern, a publisher sends messages to a topic. All subscribers to that topic receive a copy.

```mermaid
graph TD
    Publisher --> Topic
    Topic --> Subscriber1
    Topic --> Subscriber2
```

---

## 3. Queueing Model vs. Pub/Sub Model (Video Processing Example)

This represents the flow of a video processing pipeline using both queueing and publish/subscribe models.

```mermaid
flowchart TD
    subgraph Queueing_Model
        Uploader1[Video Uploader] --> MQ1[Messaging System]
        MQ1 --> Transcoder[Video Transcoder]
        Uploader1 --> Storage1[Object Storage]
        Transcoder --> Storage2[Object Storage]
    end

    subgraph PubSub_Model
        Transcoder --> MQ2[Messaging System]
        MQ2 --> DB[Database]
        MQ2 --> Cache[Cache]
        MQ2 --> Notif[Notification Service]
        MQ2 --> CDN[CDN]
    end
```
---

## 4. Competing Consumers

Multiple consumer instances process messages from a shared queue in parallel.

```mermaid
flowchart TD
    Uploader[Video Uploader] --> Queue
    Queue --> T1[Transcoder Instance 1]
    Queue --> T2[Transcoder Instance 2]
    Queue --> Tn[Transcoder Instance N]
```

---

## 5. Request/Response Messaging

Asynchronous communication with response tracking using `replyTo` and `correlationId`.

```mermaid
sequenceDiagram
    participant Uploader
    participant Transcoder
    participant CallbackQueue

    Uploader->>Transcoder: Request (replyTo: abc, correlationId: 123)
    Transcoder->>CallbackQueue: Response (correlationId: 123)
```


---

## 6. Priority Queue

### Native Support in a Single Queue:

```mermaid
flowchart TD
    Uploader --> PQueue[Priority Queue]
    PQueue --> Transcoder
    PQueue:::priority

    classDef priority fill:#ffe6cc;
```

### Separate Queues for Each Priority:

```mermaid
flowchart TD
    Uploader --> Q1[Queue (Priority 1)]
    Uploader --> Q2[Queue (Priority 2)]
    Q1 --> T1[High Priority Transcoder Pool]
    Q2 --> T2[Low Priority Transcoder Pool]
```

---

## 7. Claim Check Pattern

Stores large payloads externally and passes references in messages.

```mermaid
flowchart TD
    Uploader --> Queue1[Queue]
    Uploader --> Storage[Shared Storage]
    Queue1 --> Transcoder
    Transcoder --> Storage
```

- The queue contains a small message with a reference to the large file stored in shared storage.
- Transcoder retrieves the actual file using the reference.


---

