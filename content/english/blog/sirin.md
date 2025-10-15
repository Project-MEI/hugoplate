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

## Why a Homelab

I've always been an advocate on privacy and my dependance on third party services like Google Drive, Google Photos etc. and the increasing cost over time leads me to
wanting to self host all these services for my personal needs. Plus, one of my friend had a server that was a bit too underpowered for hosting a Minecraft server we were playing at the time, hence fueling the desire for me to finally buy the hardware and start the project.

## Hardware Overview

Everything runs on a small **mini PC**, protected by a **UPS (Uninterruptible Power Supply)** to guard against power outages and ensure graceful shutdowns.

- **CPU**: AMD Ryzen 7 8845HS (8 cores / 16 threads)  
- **Memory**: 64GB DDR5 RAM @ 4800MHz  
- **Storage**:
  - **2× 4TB HDDs in RAID 1** for data-heavy apps and redundancy
  - **1× SSD for Proxmox VE OS**
  - **1× SSD dedicated to VM disk storage**
- **Network**: 800 Mbps download / 200 Mbps upload fiber connection  
- **Router**: Standard ISP-provided router, handling DHCP, NAT, and internet routing for the homelab.

I decided to go with a mini PC instead of a desktop since the minimal space it takes and the bang for buck it offers for the performance. The model is **GMKtec K8 Plus.**

---

## The OS / Hypervisor

I decided to go with [Proxmox VE](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) since mainly it's free and I'm a cheapskate, but most importantly the versatility it offers if I decide to play with unfamiliar operating systems and the amount of functionality it has over something like TrueNAS or Unraid.

I also just had a lot of time to burn so Proxmox was the perfect choice for me to learn about sysadmin in general, and a few years later I'm pretty glad I did.

---

## VM Breakdown

Each VM is purpose-built to keep workloads cleanly separated:

- **🛰️ Network VM**  
  Handles internal networking services like **[Tailscale](https://tailscale.com/)**, **[Traefik](https://traefik.io/traefik)** etc.

- **🎮 Game VM**  
  Hosts game servers such as **[Minecraft](https://www.minecraft.net/)** and **[Palworld](https://store.steampowered.com/app/1623730/Palworld/)**.

- **💾 Storage VM**  
  Runs apps that need high-capacity storage like **[Nextcloud](https://nextcloud.com/)**, **[Immich](https://immich.app/)** etc. Connected to the RAID 1 array.

- **⚙️ Apps VM**  
  General-purpose utility server running **[CasaOS](https://casaos.zimaspace.com/)**, which provides a GUI for easy Docker container management.

- **💻 Dev VM**  
  My testing and development VM. App deployments here are managed with **[Dokploy](https://dokploy.com/)**.

---

## LXC Containers

I run a lightweight **LXC container** that host **[Semaphore UI](https://semaphoreui.com/)**, a web-based frontend for running Ansible playbooks. I use this to automate deployment tasks, container updates, and infrastructure changes.

There's also [Adguard Home LXC](https://community-scripts.github.io/ProxmoxVE/scripts?id=adguard) from the Helper Scripts repo, and [Backrest](https://community-scripts.github.io/ProxmoxVE/scripts?id=backrest) for syncing the VM backups to a remote S3 bucket.

---

## Container Management Tools

Each VM runs apps using **Docker**, with different management layers depending on its role:

- **CasaOS** on the Apps VM for easy GUI-based deployment.
- **Dokploy** on the Dev VM for Git-driven YAML deployments.
- **Portainer** on the other VMs for visual container management and orchestration.

---

## Backup & Sync Strategy

To keep my data safe and recoverable:

1. I use **Proxmox disk snapshots** to back up all VMs regularly.
2. Snapshots are then **synced to a remote S3 bucket**, giving me offsite protection.

---

That's it really, thanks for reading!
