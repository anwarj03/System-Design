# System Design Study Notes

Independent study notes for the 40-lesson interactive course [Designed to Scale](https://designed-to-scale.vercel.app/). The guide contains original summaries, checklists, self-test questions and Mermaid diagrams. Use the source course for its complete lessons and animations.

## Course notes

1. [Foundations](notes/01-foundations.md): request lifecycle, latency and throughput, estimation
2. [Scaling](notes/02-scaling.md): scale up/out, load balancing, stateless services, caching, CDNs
3. [Data and storage](notes/03-data-and-storage.md): database models, indexes, engines, replication, sharding, IDs, consistency, transactions, files
4. [Communication](notes/04-communication.md): API styles, queues, events, real-time delivery
5. [Reliability](notes/05-reliability.md): failover, rate limits, timeouts, observability
6. [Architecture](notes/06-architecture.md): service boundaries, discovery, sagas, batch and stream processing
7. [Security](notes/07-security.md): authentication, authorization, encryption, secrets
8. [Shipping](notes/08-shipping.md): tests and safe deployment
9. [Whole systems](notes/09-whole-systems.md): HLD/LLD, URL shortener, news feed, chat

## Study method

Start with requirements and rough load estimates, sketch the request path, then write down what each choice improves, what it costs and how it can fail. Revisit the self-check prompts after studying each source lesson.

## Source and attribution

The lesson order and titles are included for navigation. Source: [Designed to Scale](https://designed-to-scale.vercel.app/), by [Dilum Sanjaya](https://x.com/DilumSanjaya). Explanations and diagrams here are independently written. No course screenshots or lesson paragraphs are reproduced.

## Protocol Explorer — Security protocols

Independent notes on the nine protocols in the **Security** category of [Protocol Explorer](https://protocol-explorer-alpha.vercel.app/), designed by [Dilum Sanjaya](https://x.com/DilumSanjaya): [HTTPS](protocol-security/https.md), [DNS over HTTPS](protocol-security/dns-over-https.md), [DNSSEC](protocol-security/dnssec.md), [WPA3](protocol-security/wpa3.md), [RADIUS / 802.1X](protocol-security/radius-8021x.md), [SSH](protocol-security/ssh.md), [TLS](protocol-security/tls.md), [WireGuard](protocol-security/wireguard.md), and [IPsec](protocol-security/ipsec.md). See the [section index](protocol-security/README.md) for a comparison table and study prompts. Explanations and diagrams are independently written; no site screenshots or lesson paragraphs are reproduced.
