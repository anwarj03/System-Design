# 09 — Whole systems

Source lessons: [HLD & LLD](https://designed-to-scale.vercel.app/#/hld-lld/1) · [URL Shortener](https://designed-to-scale.vercel.app/#/design-url-shortener/1) · [News Feed](https://designed-to-scale.vercel.app/#/design-news-feed/1) · [Chat System](https://designed-to-scale.vercel.app/#/design-chat/1)

## HLD and LLD

High-level design maps services, stores, queues and trust boundaries. Low-level design specifies schemas, state transitions, APIs, concurrency and edge cases inside a component. Start at the level the question needs, state assumptions, and zoom in where a decision affects requirements. Make the contracts between levels explicit.

## URL shortener

The redirect path is read-heavy and latency-sensitive; link creation can be slower. Define collision-safe code generation, expiration and abuse needs. Store code-to-destination mappings, cache hot redirects, choose redirect semantics intentionally, and move click analytics off the critical path. Shard only when measured size or write volume requires it.

## News feed

Feeds trade off fan-out on read against fan-out on write. Pulling at read time saves work for users who never open a feed but can make reads expensive. Pushing post IDs to follower inboxes speeds common reads, while celebrities create hot fan-out jobs. A hybrid path, cursor pagination and rebuildable derived data handle skew. Eventual freshness is often acceptable if requirements permit it.

## Chat system

Persistent gateways route live connections; a registry maps users to gateways. Persist messages before delivery, attach sequence or cursor data, and let clients deduplicate retries. Offline delivery and multi-device sync require durable history. Group chats amplify fan-out; presence and typing can be approximate. State delivery semantics instead of promising exactly-once transport.

~~~mermaid
flowchart TD
    U[Client] --> G[API or connection gateway]
    G --> S[Service layer]
    S --> D[(Durable data)]
    S --> Q[Queue or event stream]
    Q --> W[Async workers]
    W --> C[Cache or derived views]
~~~

**Interview sequence:** clarify functional and quality requirements; estimate load; define APIs and data; draw the simplest viable architecture; test its critical path against scale, failure and consistency; explain tradeoffs and the next bottleneck.

**Self-check:** Why can a feed tolerate delayed updates while chat emphasizes order and durability? Which path should be optimized first for each system?
