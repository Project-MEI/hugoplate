---
title: "The Sirin homelab project"
meta_title: "The Sirin homelab project"
description: "this is meta description"
date: 2022-04-04T05:00:00Z
image: "/images/project-mei/sirin.png"
categories: ["Projects"]
author: "Raiden"
tags: ["homelab", "homeserver", "sirin"]
draft: false
---

## 🖥️ Hardware Overview

Everything runs on a compact yet powerful **mini PC**, protected by a **UPS (Uninterruptible Power Supply)** to guard against power outages and ensure graceful shutdowns.

- **CPU**: AMD Ryzen 7 8845HS (8 cores / 16 threads)  
- **Memory**: 64GB DDR5 RAM @ 4800MHz  
- **Storage**:
  - **2× 4TB HDDs in RAID 1** for data-heavy apps and redundancy
  - **1× SSD for Proxmox VE OS**
  - **1× SSD dedicated to VM disk storage**
- **Network**: 800 Mbps download / 200 Mbps upload fiber connection  
- **Router**: Standard consumer router, handling DHCP, NAT, and internet routing for the homelab.

This setup provides a solid balance of performance, power efficiency, and uptime protection.

---

## 🧱 Proxmox: The Foundation

At the base of the system is **Proxmox VE**, an open-source hypervisor. It allows me to run and manage virtual machines and containers with fine-grained control, backups, snapshots, and automation support.

---

## 🧩 VM Breakdown by Role

Each VM is purpose-built to keep workloads cleanly separated:

- **🛰️ Network VM**  
  Handles internal network services like **AdGuard Home**, **Tailscale**, and custom DNS/routing.

- **🎮 Game VM**  
  Hosts multiplayer game servers such as **Minecraft** and **Palworld**, optimized for performance.

- **💾 Storage VM**  
  Runs apps that need high-capacity storage like **Nextcloud**, **Immich**, or backup services. Connected to the RAID 1 array.

- **⚙️ Apps VM**  
  General-purpose utility server running **CasaOS**, which provides a GUI for easy Docker container management.

- **💻 Dev VM**  
  My testing and development VM. App deployments here are managed with **Dokploy**.

---

## 🧪 Automation with LXC + Ansible

I run a lightweight **LXC container** that hosts **Ansible Semaphore**, a web-based frontend for running Ansible playbooks. I use this to automate deployment tasks, container updates, and infrastructure changes.

---

## 🐳 Container Management Tools

Each VM runs apps using **Docker**, with different management layers depending on its role:

- **CasaOS** on the Apps VM for easy GUI-based deployment.
- **Dokploy** on the Dev VM for Git-driven YAML deployments.
- **Portainer** on the other VMs for visual container management and orchestration.

---

## 💾 Backup & Sync Strategy

To keep my data safe and recoverable:

1. I use **Proxmox disk snapshots** to back up all VMs regularly.
2. Snapshots are then **synced to a remote S3 bucket**, giving me offsite protection.

---

## 🔐 Why This Setup Works for Me

- **Separation of Concerns**: Each VM has a clear purpose, making things easier to manage.
- **Security**: App isolation through VMs and containers reduces risk.
- **Automation**: Ansible + Dokploy = faster, reproducible deployments.
- **Resilience**: RAID 1 storage, snapshots, and S3 backups give peace of mind.
- **Learning-Friendly**: Mimics production infrastructure for learning and experimentation.

---

## ⚙️ What’s Next?

Eventually, I’d like to:

- Add centralized logging and alerting  
- Automate snapshot rotation and cleanup  
- Explore lightweight LXC containers for smaller services  
- Maybe experiment with Kubernetes down the line  

For now, the setup is stable, fun, and extremely useful.

---

Thanks for reading! 🚀
