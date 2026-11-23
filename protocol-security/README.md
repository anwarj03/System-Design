# Internet Protocol Security — Study Notes

Independent notes on the nine protocols in the **Security** category of [Protocol Explorer](https://protocol-explorer-alpha.vercel.app/), designed by [Dilum Sanjaya](https://x.com/DilumSanjaya).

These notes explain the protocols in my own words. The diagrams are original Mermaid sketches; they are not screenshots or exports from the app. Use the interactive source for its animations and packet inspector.

## Contents

1. [HTTPS](https.md) — web traffic protected by TLS
2. [DNS over HTTPS](dns-over-https.md) — DNS messages carried inside HTTPS
3. [DNSSEC](dnssec.md) — authenticity and integrity for DNS data
4. [WPA3](wpa3.md) — Wi-Fi security for personal networks
5. [RADIUS and 802.1X](radius-8021x.md) — enterprise network access
6. [SSH](ssh.md) — authenticated encrypted remote access
7. [TLS](tls.md) — the secure transport channel used by many applications
8. [WireGuard](wireguard.md) — a compact, public-key based VPN
9. [IPsec](ipsec.md) — IP packet protection and VPN tunnels

## A quick map

| Protocol | Main job | Typical layer / transport | What it does not provide by itself |
|---|---|---|---|
| HTTPS | Protect web requests and responses | HTTP over TLS over TCP, usually 443 | Anonymity from the website or trustworthiness of the site |
| DNS over HTTPS | Encrypt DNS queries between client and resolver | DNS messages over HTTPS, usually 443 | DNS answer authenticity against a malicious resolver |
| DNSSEC | Authenticate DNS records and delegation chain | DNS records and signatures | Query privacy or encryption |
| WPA3 | Protect a Wi-Fi link | 802.11 link layer | End-to-end protection beyond the access point |
| RADIUS / 802.1X | Authenticate a user/device before network access | EAP over an access link; RADIUS commonly UDP 1812/1813 | Encryption of all later application traffic |
| SSH | Secure remote sessions and forwarding | TCP, commonly 22 | Safety of commands or trust in an unknown host key |
| TLS | Authenticate peers and protect an application channel | Commonly over TCP; QUIC integrates TLS 1.3 | Hiding all metadata or securing compromised endpoints |
| WireGuard | Route IP traffic through an encrypted VPN tunnel | IP over UDP; 51820 is a common default | Hiding traffic from the VPN operator or destination |
| IPsec | Authenticate and/or protect IP packets | ESP at IP layer; IKEv2 commonly UDP 500 | Application-level authorization or protection after tunnel termination |

“Typical” values are conventions, not universal requirements. Deployments can differ.

## Study prompts

- Which party can read the data at each hop?
- What identity is authenticated, and how is the trust anchor chosen?
- Does the protocol provide confidentiality, integrity, authentication, or a combination?
- What metadata remains visible?
- Where does the protected connection terminate?
- Which keys are long lived, and which are fresh per session?

## Source and attribution

Protocol-specific references are listed in each note and link to primary RFC or standards documents. App: [Protocol Explorer](https://protocol-explorer-alpha.vercel.app/). Creator: [Dilum Sanjaya on X](https://x.com/DilumSanjaya). No app screenshots or lesson text are reproduced here.
