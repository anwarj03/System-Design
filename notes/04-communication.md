# 04 — Communication

Source lessons: [REST, RPC & GraphQL](https://designed-to-scale.vercel.app/#/apis/1) · [Message Queues](https://designed-to-scale.vercel.app/#/queues/1) · [Pub/Sub & Events](https://designed-to-scale.vercel.app/#/pubsub/1) · [Real-time Updates](https://designed-to-scale.vercel.app/#/realtime/1)

## API styles

An API contract specifies operations, inputs, outputs, errors and compatibility. REST organizes around resources and HTTP semantics; GraphQL lets clients shape reads but needs query-cost limits; RPC expresses procedure calls and suits internal contracts. Choose around client needs, network round trips, payload size and tooling. Paginate large collections, bound expensive queries and evolve fields compatibly.

## Queues and events

A queue decouples a request from slow work: producers enqueue jobs and consumers process later. Acknowledgement after completion, retries and a dead-letter path reduce silent loss, but handlers should be idempotent because redelivery is normal. Backlogs absorb spikes temporarily; monitor their age and drain rate. Partitions can preserve order per key, while global order limits parallelism.

Pub/sub lets one event reach multiple subscribers without a publisher synchronously calling each one. This reduces direct coupling but introduces eventual effects, schema evolution, replay and duplicate handling. A transactional outbox closes the gap between committing database state and publishing its event.

## Real-time delivery

Polling is simple but sends empty requests. Long polling holds a request until data or timeout. Server-sent events provide one-way updates; WebSockets provide bidirectional sessions. Persistent connections need routing, heartbeats, reconnect behavior and per-user fan-out. Offline clients need durable message storage and cursor-based sync; presence is approximate and can expire.

~~~mermaid
flowchart LR
    Client --> API[API request]
    API --> DB[(Database)]
    DB --> Outbox[Outbox]
    Outbox --> Bus[Event broker]
    Bus --> W[Worker]
    Bus --> N[Notification subscriber]
~~~

**Self-check:** What delivery guarantee does a consumer need? How will it handle retries? Which users need a persistent connection?
