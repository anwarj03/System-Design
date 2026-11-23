# 07 — Security

Source lessons: [Authentication](https://designed-to-scale.vercel.app/#/authentication/1) · [Authorization](https://designed-to-scale.vercel.app/#/authorization/1) · [Encryption & Secrets](https://designed-to-scale.vercel.app/#/encryption/1)

## Authentication

Authentication establishes identity; authorization decides what it may do. Store passwords with a dedicated slow hashing function and unique salt, never plaintext or reversible encryption. Protect login against credential stuffing; support multi-factor authentication or passkeys. Design reset flows carefully. Sessions and tokens need expiry, revocation strategy and secure transport.

## Authorization

Check permission on every server-side request and against the specific object and action. A valid login does not imply access to every record. Enforce tenant boundaries in service logic and, where suitable, database policies. Use least privilege for users and services, validate writable fields, log sensitive access, and never trust client-supplied roles or hidden UI controls.

## Encryption and secrets

TLS protects traffic and authenticates endpoints; certificates need renewal monitoring. Encrypt stored data where it reduces risk, while keeping keys separate and access controlled. Use managed secret storage, rotation and narrow scopes; never commit credentials. Tokenization can reduce exposure of sensitive identifiers. End-to-end encryption limits what the server can inspect or recover.

**Self-check:** What can a leaked password table enable? Where must object ownership be checked? Which components can decrypt protected data?
