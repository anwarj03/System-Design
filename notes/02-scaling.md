# 02 — Scaling

Source lessons: [Vertical vs Horizontal](https://designed-to-scale.vercel.app/#/vertical-horizontal/1) · [Load Balancing](https://designed-to-scale.vercel.app/#/load-balancing/1) · [Stateless Services](https://designed-to-scale.vercel.app/#/stateless/1) · [Caching](https://designed-to-scale.vercel.app/#/caching/1) · [Content Delivery](https://designed-to-scale.vercel.app/#/cdn/1)

## Scale up or out

Vertical scaling gives one machine more CPU, memory or I/O and is operationally simple, but has a ceiling and leaves a large failure domain. Horizontal scaling adds instances and can improve capacity and redundancy when work is distributable. It adds coordination, routing and load-skew concerns. Autoscaling follows demand; pre-scaling helps with known spikes because new capacity takes time to become healthy.

## Load balancing

A load balancer gives clients one entry point and routes traffic across healthy instances. Round robin is simple; least-connections or workload-aware routing can help when request costs vary. Health checks remove unhealthy instances; readiness and connection draining protect deployments. The balancer needs redundancy too. Layer 7 routing uses request details at additional complexity.

## Stateless services

If an instance keeps session state only in its own memory, a later request routed elsewhere may fail. Sticky sessions mask this but complicate failover and rebalancing. Put durable shared state in a shared store, or carry appropriately signed state in a token. Store uploads in shared object storage rather than one server's local disk.

## Caching

Cache-aside reads the cache first, falls back to the source on a miss, then fills the cache. A high hit rate reduces repeated database work. Define freshness, TTL and invalidation behavior explicitly. Bound memory and prevent stampedes with request coalescing or jittered expiry. Negative caching can reduce repeated misses. Never share private data under an unsafe cache key.

## Content delivery

A CDN serves cacheable assets from edge locations closer to users and reduces origin load. Versioned asset names help cache releases safely. Separate public immutable content from personalized responses; cache policy must match privacy and freshness needs. An origin shield consolidates misses, but cold edges still reach the origin.

~~~mermaid
flowchart LR
    U[Users] --> LB[Load balancer]
    LB --> A1[App instance]
    LB --> A2[App instance]
    A1 --> C[(Shared cache)]
    A2 --> C
    C --> DB[(Database)]
    U --> E[CDN edge]
    E --> O[Object origin]
~~~

**Self-check:** Which state must be shared for horizontal scaling? What happens on a cold-cache spike? How do unhealthy instances stop receiving requests?
