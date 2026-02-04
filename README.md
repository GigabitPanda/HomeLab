# Proxmox Home Lab

![Status](https://img.shields.io/badge/status-operational-success)
![OS](https://img.shields.io/badge/host%20os-Debian%20Bookworm-blue)
![Proxmox](https://img.shields.io/badge/Proxmox-VE%208.x-orange)

> **Status:** ✅ Proxmox VE successfully installed, network-stable, and ready for VM creation

This repository documents the **initial setup and troubleshooting journey** of building a Proxmox-based home lab from an old laptop. The goal of this documentation is to provide a **clear, honest, and reproducible record** of the installation process, including *every major obstacle encountered and how it was resolved*.

---

#  README.md

## Table of Contents

1. [Project Overview](#project-overview)
2. [Hardware Specifications](#hardware-specifications)
3. [Goals & Use Cases](#goals--use-cases)
4. [Installation Summary](#installation-summary)
5. [Final System State](#final-system-state)
6. [Key Takeaways](#key-takeaways)
7. [Next Steps](#next-steps)

---

## Project Overview

This project repurposes an older laptop into a **Proxmox Virtual Environment (VE) home lab**. Proxmox serves as the bare‑metal hypervisor, providing a foundation for virtual machines, containers, and future self‑hosted services.

The system is intended to be:

* Always-on (24/7)
* Stable and reproducible
* Suitable for learning Linux, virtualization, and homelab fundamentals

---

## Hardware Specifications

* **CPU:** Intel i5
* **Memory:** 12 GB RAM
* **Storage:** ~443 GB SSD
* **Form Factor:** Laptop (repurposed)

---

## Goals & Use Cases

* Learn Linux system administration
* Learn virtualization (VMs & containers)
* Host services at home
* Build a foundation for Docker, media servers, and experimentation
* Create a long-term learning homelab

---

## Installation Summary

* Proxmox VE installed directly on bare metal
* BIOS configured for virtualization and UEFI boot
* Proxmox Web UI accessible from local network
* Networking, DNS, and package repositories fully stabilized

---

## Final System State

###  Architecture Overview

```
[ Home Router / Gateway ] 192.168.1.xxx
           │
           │  (Ethernet)
           ▼
┌────────────────────────────┐
│  Proxmox Host (Laptop)     │
│  Debian 12 (Bookworm)      │
│                            │
│  vmbr0  ── 192.168.1.xx    │
│     │                      │
│     ├── Ubuntu Server VM   │
│     │     192.168.1.xxx    │
│     │                      │
│     └── (Future VMs/LXC)   │
│                            │
│  Web UI: :8006             │
└────────────────────────────┘
           │
           ▼
[ Admin PC / Browser ]
```

---

* ✅ Proxmox VE installed and operational
* ✅ Correct subnet and gateway configuration
* ✅ Stable DNS configuration
* ✅ Community (no-subscription) repositories enabled
* ✅ Debian **bookworm** only (no testing/unstable repos)
* ✅ Clean `apt update` / `apt upgrade`
* ✅ Proxmox VE installed and operational
* ✅ Correct subnet and gateway configuration
* ✅ Stable DNS configuration
* ✅ Community (no‑subscription) repositories enabled
* ✅ Debian **bookworm** only (no testing/unstable repos)
* ✅ Clean `apt update` / `apt upgrade`

---

## Key Takeaways

* Proxmox host must live on the **same subnet as the router** unless routing is explicitly configured
* `vmbr0` is the correct interface for the host IP
* Enterprise repositories will break `apt` without a subscription
* DNS misconfiguration can masquerade as network failure
* Mixing Debian releases (`trixie` + `bookworm`) is dangerous

---

## Lessons Learned / Gotchas

* **If the Web UI loads on `127.0.0.x` but not remotely, it is almost always networking or DNS**
* `inet manual` on physical NICs is *normal* in Proxmox
* Always verify DNS with `ping deb.debian.org`, not just IPs like `8.8.8.8`
* Proxmox defaults are enterprise-focused; homelabs must intentionally switch repos
* Fixing the root cause is better than reinstalling — nearly everything here was recoverable

---

## Next Steps

* Proxmox host must live on the **same subnet as the router** unless routing is explicitly configured
* `vmbr0` is the correct interface for the host IP
* Enterprise repositories will break `apt` without a subscription
* DNS misconfiguration can masquerade as network failure
* Mixing Debian releases (`trixie` + `bookworm`) is dangerous

---

## Next Steps

* Create first Ubuntu Server VM
* Learn LXC containers
* Install Docker & Portainer
* Build a media server (Jellyfin / Plex)
* Implement backups and snapshots

---
