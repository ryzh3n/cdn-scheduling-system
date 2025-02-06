# 📌 Architecture & System Design

> (This section provides a high-level overview before diving into individual components.)

## High-Level System Architecture
![image](https://github.com/user-attachments/assets/2f18202f-c006-4e2a-b33b-e6ac47337e52)
- Brief diagram of how all CDN components interact.
- Overview of CDN control plane vs. data plane.

## DNS Architecture & Resolution Process
- How DNS queries are resolved in your CDN.
- Breakdown of authoritative DNS vs. edge DNS vs. recursive resolvers.
- Traffic steering strategies (latency-based, geo-based, weighted).

## System Design & Internal Components
- How CDN nodes communicate with the master control system.
- Breakdown of edge nodes, control servers, caching layers.
- The role of Jenkins, Kubernetes, Prometheus, Redis, ELK, and security layers in the system.

---

# 🔄 Failover & Traffic Routing

> (Explains how your CDN maintains uptime and handles failures.)

## Failover Mechanism
- How CDN nodes handle outages or ISP failures.
- BGP-based failover strategies (multi-ISP routing).
- DNS failover (e.g., TTL adjustments, automatic record updates).
- CDN node health checks & automatic traffic rerouting.

## Load Balancing & Request Routing
- DNS-level load balancing (geo-routing, latency-based, weighted).
- How requests are routed within a CDN node.
- Edge caching & origin fallback strategies.

---

# 🖥 How a CDN Node Works (CDN Node Key Components)

> (Detailed breakdown of a single CDN node—moved from introduction.md.)

## CDN Node Internal Architecture
- Overview of core services inside a node.
- Interactions between Nginx, Redis, cdn-agent, worker service, exporter, Filebeat, etc.

## Security & Firewall Mechanisms
- How worker service manages iptables & ipset.
- WAF rule enforcement & dynamic blocking.
