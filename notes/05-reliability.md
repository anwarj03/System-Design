# 05 — Reliability

Source lessons: [Redundancy & Failover](https://designed-to-scale.vercel.app/#/redundancy/1) · [Rate Limiting](https://designed-to-scale.vercel.app/#/rate-limiting/1) · [Timeouts & Retries](https://designed-to-scale.vercel.app/#/timeouts-retries/1) · [Observability](https://designed-to-scale.vercel.app/#/observability/1)

## Redundancy and failover

If a request needs every component in a chain, overall availability is lower than any one component's. Remove single points of failure by replicating across independent failure domains, not merely duplicating instances on one host. Define recovery time and acceptable data loss, and rehearse failover. Canaries limit the blast radius of a bad change; multiple regions add resilience and complexity.

## Rate limiting

Shared capacity needs a fairness policy. Token buckets allow bursts within a sustained rate; fixed or sliding windows are simpler options with different boundary behavior. Distributed gateways must coordinate or approximate per-tenant budgets. Return retry guidance and shed low-priority load during overload.

## Timeouts, retries and bulkheads

Every remote call needs a deadline. Retry only transient failures, with bounded attempts, exponential backoff and jitter; otherwise clients amplify an outage. Idempotency keys make retried writes safe. Circuit breakers pause calls to a failing dependency; bulkheads isolate pools so one slow path cannot consume every worker. Pass deadlines downstream.

## Observability

Metrics show trends and percentiles, logs record events, and distributed traces connect spans across services. Tie alerts to user-facing objectives rather than noisy infrastructure signals alone. Add request IDs and useful dimensions while controlling cardinality and sensitive data. After incidents, record impact, timeline, causes and actions without blame.

**Self-check:** Which failure domains are independent? What prevents retries becoming a storm? Which trace span identifies the slow dependency?
