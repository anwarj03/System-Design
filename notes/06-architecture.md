# 06 — Architecture

Source lessons: [Monolith vs Microservices](https://designed-to-scale.vercel.app/#/microservices/1) · [Service Discovery](https://designed-to-scale.vercel.app/#/service-discovery/1) · [Sagas](https://designed-to-scale.vercel.app/#/sagas/1) · [Batch & Stream Processing](https://designed-to-scale.vercel.app/#/batch-stream/1)

## Boundaries and service discovery

A monolith keeps calls local and deployment simple; it is often the right starting point. Split around business capabilities when independent ownership, scaling or release cadence justifies network and operations costs. Service-owned data avoids hidden coupling but requires explicit APIs, events and read models. A strangler migration replaces one capability at a time.

Instances come and go, so hard-coded addresses fail. A registry, DNS or platform mechanism maps logical names to ready instances. Health, readiness, slow start and draining are different concerns. Gateways centralize edge functions; a service mesh automates some internal transport policy but cannot fix poor boundaries.

## Distributed transactions

A database transaction cannot atomically span independent services. Two-phase commit coordinates participants but can block. A saga records local commits and compensating actions; orchestration centralizes the flow, choreography communicates via events. Compensation is a business action, not time reversal. Make steps durable and idempotent; define unknown outcomes and repair paths.

## Batch and stream processing

Batch groups bounded data and runs later, often efficiently across partitions. Stream processing handles events continuously and introduces windows, late arrivals, duplicates and state. Keep heavy analytics off the production request database. Use combiners or key salting for skew, monitor consumer lag, and choose exact or approximate results based on product needs.

**Self-check:** What pain justifies splitting a monolith? Which saga steps need compensation? How do you know a stream processor is falling behind?
