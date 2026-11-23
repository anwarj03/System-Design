# 01 — Foundations

Source lessons: [How a Request Travels](https://designed-to-scale.vercel.app/#/request-lifecycle/1) · [Latency & Throughput](https://designed-to-scale.vercel.app/#/latency-throughput/1) · [Napkin Math](https://designed-to-scale.vercel.app/#/napkin-math/1)

## How a request travels

A page load crosses name resolution, connection setup, an HTTP request, application and database work, response transfer, then often more asset requests. Total time accumulates along the critical path. Measure phases separately before optimizing: a slow query and a far-away user can look similar but need different fixes.

~~~mermaid
sequenceDiagram
    participant B as Browser
    participant D as DNS
    participant A as Application
    participant DB as Database
    B->>D: Resolve name (if uncached)
    D-->>B: Address
    B->>A: Connect and request
    A->>DB: Read or write
    DB-->>A: Result
    A-->>B: Response
    B->>A: Request additional assets
~~~

Compare cold and warm requests; inspect DNS, connection, time to first byte, payload size and follow-up requests; trace downstream calls; test from more than one region.

## Latency and throughput

Latency is the duration of one operation; throughput is completed work per unit time. More capacity can raise throughput without making an individual request faster. As utilization nears capacity, queues grow and tail latency rises. Averages hide slow users, so track percentiles such as p50 and p99. Fan-out makes tails matter because an operation waiting for many services is likely to encounter a slow one. Batching can improve throughput while adding wait time.

## Napkin math

Estimate orders of magnitude before selecting infrastructure. Convert daily users and actions into average requests per second, then apply a peak multiplier. Estimate storage from event volume × bytes × retention, and bandwidth from request rate × response size. Include indexes, replicas, growth and headroom. The goal is to expose weak assumptions, not predict exact bills.

**Self-check:** What distinguishes server work from network delay? Why can average latency improve while p99 worsens? Which estimate could change the architecture most?
