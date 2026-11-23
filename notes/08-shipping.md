# 08 — Shipping

Source lessons: [Testing](https://designed-to-scale.vercel.app/#/testing/1) · [CI/CD & Deployments](https://designed-to-scale.vercel.app/#/cicd/1)

## Testing

Unit tests quickly check isolated logic; integration tests exercise real dependencies; contract tests protect team boundaries; end-to-end tests verify a few critical journeys. Favor fast, stable lower-level checks and a focused set of broad scenarios. Use test doubles deliberately, remove flakiness, and add load and failure tests for resilience claims.

## CI/CD and deployment

Continuous integration runs checks on each change. Build one immutable artifact and promote it through environments. Blue-green deployment switches between versions; canaries expose a small fraction of users first. Expand-and-contract migrations preserve compatibility while old and new code overlap. Feature flags separate deployment from release. Track deployment frequency, change failure rate and recovery time.

~~~mermaid
flowchart LR
    C[Commit] --> CI[Build and tests]
    CI --> A[Immutable artifact]
    A --> S[Stage]
    S --> K[Canary]
    K -->|healthy| P[Progressive rollout]
    K -->|bad signals| R[Rollback]
~~~

**Self-check:** Which tests catch contract drift? How can a schema change support old and new application versions at the same time?
