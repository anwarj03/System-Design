# 03 — Data and storage

Source lessons: [SQL vs NoSQL](https://designed-to-scale.vercel.app/#/sql-nosql/1) · [Indexes](https://designed-to-scale.vercel.app/#/indexes/1) · [Storage Engines](https://designed-to-scale.vercel.app/#/storage-engines/1) · [Replication](https://designed-to-scale.vercel.app/#/replication/1) · [Sharding](https://designed-to-scale.vercel.app/#/sharding/1) · [Consistent Hashing](https://designed-to-scale.vercel.app/#/consistent-hashing/1) · [Unique IDs](https://designed-to-scale.vercel.app/#/unique-ids/1) · [CAP & Consistency](https://designed-to-scale.vercel.app/#/cap/1) · [Consensus](https://designed-to-scale.vercel.app/#/consensus/1) · [Transactions](https://designed-to-scale.vercel.app/#/transactions/1) · [Files & Media](https://designed-to-scale.vercel.app/#/files/1)

## Choosing a store

Relational databases provide schemas, joins and mature transactions; they are a sound default when relationships and constraints matter. Document and key-value stores suit access patterns that fit their models, but trade away some relational guarantees or query flexibility. Search and analytics engines are specialists. Choose by data shape, query patterns, consistency needs and operational skill, not fashion.

## Indexes and storage engines

An index trades storage and write work for faster reads on selected access paths. Composite column order matters; mismatched predicates may not benefit. Inspect query plans. B-tree engines maintain ordered structures; LSM designs buffer writes and compact sorted files later. Both balance read, write, space and recovery costs. A write-ahead log helps recover committed changes; durability also depends on flush policy.

## Replication and sharding

Replication copies data for read scaling and fault tolerance, but replicas can lag. Route read-your-writes to a leader or use consistency tokens when needed. Failover needs safe promotion and testing. Sharding partitions data to grow write and storage capacity; choose keys that distribute load and support common queries. Hot keys, cross-shard queries, rebalancing and backups become harder. Replication copies; sharding splits.

Consistent hashing maps keys and nodes to a ring so node changes remap only a fraction of keys. Virtual nodes help balance uneven partitions; hot keys still need special handling.

## IDs, consistency and consensus

Central counters are simple but may bottleneck across shards. Random UUIDs avoid coordination but can enlarge indexes; time-ordered identifiers aid locality while exposing ordering and clock concerns. Choose based on uniqueness, sortability, compactness and decentralization.

During a network partition, a system may reject some operations to preserve strong consistency or continue with potentially stale/conflicting results. CAP describes the tradeoff under partition; consistency models form a spectrum. Quorums tune behavior. Consensus protocols use overlapping majorities to agree on a leader and log; fencing prevents an old paused leader from writing after failover.

## Transactions and media

Transactions protect invariants across concurrent changes. Prefer atomic statements or short transactions; locks and optimistic version checks prevent races. Isolation levels define which anomalies remain; constraints provide a final guard. Keep external payment calls outside long-held locks and model multi-step workflows with expiring reservations.

Store large binary objects in object storage and metadata in a database. Direct uploads can use scoped temporary URLs; multipart uploads support large files. Process variants asynchronously and deliver through a CDN. Reconcile orphaned objects, enforce private access and lifecycle old media to cheaper tiers.

~~~mermaid
flowchart TD
    App[Application] -->|records| DB[(Primary database)]
    DB -->|replication log| R[(Read replica)]
    App -->|large bytes| Obj[(Object storage)]
    App -->|metadata| DB
    User[Client] --> CDN[CDN]
    CDN --> Obj
~~~

**Self-check:** Which reads can tolerate replica lag? What makes a shard key dangerous? Which invariant must a transaction preserve?
