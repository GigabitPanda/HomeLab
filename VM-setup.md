#  vm-setup.md

## Ubuntu Server VM Build Guide (Proxmox)

This guide documents the **standard Ubuntu Server VM** used as the first workload on this Proxmox host.

---

## VM Creation Settings

### General

* **Name:** ubuntu-server
* **Resource Pool:** None

### OS

* **ISO:** Ubuntu Server 22.04 LTS / 24.04 LTS

### System

* **BIOS:** Default (SeaBIOS)
* **Machine:** q35
* **SCSI Controller:** VirtIO SCSI
* **QEMU Guest Agent:** Enabled
* **TPM:** Disabled

### Disks

* **Bus:** SCSI
* **Storage:** local-lvm
* **Size:** 32 GB

### CPU

* **Cores:** 2
* **Type:** host

### Memory

* **RAM:** 2048–4096 MB

### Network

* **Bridge:** vmbr0
* **Model:** VirtIO

---

## Ubuntu Installer Choices

* Installation type: **Ubuntu Server (not minimized)**
* Network: **DHCP (default)**
* Storage: **Use entire disk + LVM**
* SSH: **Install OpenSSH server**
* Featured snaps: **Skip**

---

## Post-Install Checklist

```bash
sudo apt update && sudo apt upgrade -y
ip a
ip route
```

* Confirm network connectivity
* Confirm SSH access
* Snapshot VM before further changes

---

**End of documentation.**
