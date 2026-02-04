# 🛠️ troubleshooting.md

## Table of Contents

1. [Boot & BIOS Issues](#boot--bios-issues)
2. [Network Configuration Failures](#network-configuration-failures)
3. [Web UI Not Reachable](#web-ui-not-reachable)
4. [APT & Repository Errors](#apt--repository-errors)
5. [DNS Misconfiguration](#dns-misconfiguration)
6. [Debian Version Mismatch](#debian-version-mismatch)

---

## Boot & BIOS Issues

**Symptoms:**

* USB not booting
* MBR/GPT confusion

**Cause:**

* Mismatch between BIOS boot mode and partition scheme

**Resolution:**

* UEFI boot → GPT
* Legacy boot → MBR
* Secure Boot disabled
* Virtualization enabled

---

## Network Configuration Failures

**Symptoms:**

* Proxmox unreachable from browser
* Ping timeouts

**Cause:**

* Host IP set to wrong subnet

**Resolution:**

```text
Proxmox IP: 192.168.1.xx/24
Gateway:    192.168.1.xxx
```

---

## Web UI Not Reachable

**Verified working services:**

```bash
systemctl status pveproxy
ss -ltnp | grep 8006
curl -k https://127.0.0.x:8006
```

**Conclusion:**

* Proxmox services were running correctly
* Issue was network configuration, not Proxmox itself

---

## APT & Repository Errors

**Symptoms:**

* `apt update` failed to fetch
* Invalid response errors

**Cause:**

* Enterprise repositories enabled without subscription

**Resolution:**

* Disabled enterprise repos
* Enabled community repo:

```text
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
```

---

## DNS Misconfiguration

**Symptoms:**

* Cannot resolve domain names
* `Temporary failure resolving ...`

**Cause:**

```text
nameserver 127.0.0.1
```

**Resolution:**

```text
nameserver 192.168.1.xxx
nameserver 1.1.1.1
nameserver 8.8.8.8
```

Also set DNS permanently via:

* Proxmox Web UI → Node → System → DNS

---

## Debian Version Mismatch

**Symptoms:**

* `trixie` and `bookworm` mixed
* Duplicate repo warnings

**Cause:**

* Debian testing repositories enabled

**Resolution:**

* Replaced all `trixie` references with `bookworm`
* Ensured Debian repos exist in **one place only** (`debian.sources`)

---

## Final Note

This troubleshooting log exists to show that **system administration is iterative**, and real learning happens during failure analysis. Every issue here contributed directly to a deeper understanding of Linux, networking, and Proxmox.

---

## Proxmox Troubleshooting

```md
# Troubleshooting

## Portainer refused to connect

**Symptoms**
- Browser showed connection timeout
- `curl https://127.0.0.1:9000` SSL errors

**Cause**
- Port 9000 is HTTP, not HTTPS
- Firewall rules not enabled at correct Proxmox level
- UFW initially disabled

**Fix**
- Accessed via `http://<VM-IP>:9000`
- Enabled firewall rules at VM level
- Enabled UFW and allowed port 9000/tcp

---

## Proxmox Web UI stopped loading

**Cause**
- Firewall rule accidentally blocked port 8006

**Fix**
- Restored rule allowing TCP 8006 from LAN
