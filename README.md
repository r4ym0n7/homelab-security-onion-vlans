# homelab-security-onion-vlans

# Home Lab: VLAN-Segmented Network with Security Onion

A home lab built to practice network segmentation and network security
monitoring. Containerized services (including Plex) run in Docker, and
Security Onion on a separate VM monitors traffic for intrusion detection
and analysis.

## Goals
- Practice VLAN design and segmentation between trusted, server, and lab devices
- Run Security Onion for network security monitoring (NSM) and intrusion detection
- Generate and investigate realistic traffic and alerts
- Document the build so it can be reproduced

## Architecture

[Insert a diagram: draw.io, Excalidraw, or the simple ASCII version below]

    Router / Firewall
        |
    Managed Switch (802.1Q trunk)
        |-- VLAN [10] Trusted    : [personal devices]
        |-- VLAN [20] Servers    : [Docker host: Plex and other containers]
        |-- VLAN [30] Lab / IoT  : [lab devices or untrusted devices]
        |-- VLAN [99] Management : [Security Onion management, hypervisor]

    Security Onion VM
        |-- Management interface -> VLAN [99]
        |-- Monitoring (sniffing) interface -> [SPAN/mirror port or tap]

## Components
| Component | Purpose | Notes |
|---|---|---|
| [Hypervisor: e.g., Proxmox / VirtualBox / VMware] | Hosts VMs | [version] |
| Docker host | Runs containerized services | [OS] |
| Plex (container) | Media server, realistic service traffic | [image, ports] |
| Security Onion VM | NSM, IDS alerts, traffic analysis | [version, resources] |
| [Router/firewall] | Inter-VLAN routing and rules | [model/software] |
| [Managed switch] | VLAN trunks and port mirroring | [model] |

## VLAN plan
| VLAN | Name | Subnet (example) | Purpose |
|---|---|---|---|
| [10] | Trusted | 192.168.10.0/24 | [ ] |
| [20] | Servers | 192.168.20.0/24 | [ ] |
| [30] | Lab/IoT | 192.168.30.0/24 | [ ] |
| [99] | Management | 192.168.99.0/24 | [ ] |

## Inter-VLAN firewall rules (summary)
- [Trusted -> Servers: allow Plex port only]
- [Lab/IoT -> Trusted: deny]
- [Lab/IoT -> Internet: allow]
- [Management reachable only from Trusted]

## Security Onion setup
- Deployment type: [Standalone / Import / Eval]
- Monitoring interface: [how traffic is mirrored: SPAN port, tap, or virtual switch mirror]
- Management interface: [VLAN]
- Rule set(s) enabled: [e.g., ET Open]

## What I tested
- [Traffic generated: e.g., port scan from the lab VLAN with nmap against my own devices]
- [Alerts observed and what they showed]
- [Whether segmentation rules blocked what they should]

## Findings and lessons learned
- [What worked]
- [What broke and how I fixed it]
- [Tuning: false positives, noisy rules, resource limits]

## Improvements planned
- [e.g., add Sigma-based detections, centralize logs, add DNS filtering]

## Reproducing this lab
1. [Create VLANs on router and switch]
2. [Configure trunk/access ports]
3. [Deploy Docker host and Plex container]
4. [Install Security Onion and configure the monitoring interface]
5. [Verify with test traffic]

## Notes
- All testing was done on my own network and devices.
- IP addresses, hostnames, and identifiers in this repo are examples or sanitized.
