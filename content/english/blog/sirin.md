---
title: "Sirin Homelab"
meta_title: "The Sirin homelab project"
description: "this is meta description"
date: 2022-04-04T05:00:00Z
image: "/images/project-mei/sirin.png"
categories: ["Projects"]
author: "Raiden"
tags: ["homelab", "homeserver", "sirin"]
draft: false
---

## What made me start a Homelab

- Friends needed a good server for games/I didn't want to rent
- I didn't want to play for Google Drive/Photos
- I wanted to learn about technical things like computing hardware and Linux in general
- It was at a time when I didn't have a job and had a lot of free time
- My internet and electricity is pretty stable
- Mini PC was at a good price at the time

## Hardware overview

- **Hypervisor/OS**: Proxmox VE
- **CPU**: AMD Ryzen 7 8845HS (8 cores / 16 threads)  
- **Memory**: 64GB DDR5 RAM @ 4800MHz  
- **Storage**:
  - **2× 4TB HDDs in RAID 1**
  - **1× SSD for Proxmox VE OS**
  - **1× SSD dedicated to VM disk storage**
- **Network**: 800Mbps down/200Mbps up
- **Router**: Standard ISP-provided router (need to replace this someday)
- **UPS**: Prolink 650VA model

*Note: Hardware may change since I don't update this post often

---

## What I'm running

- Pulse for monitoring Proxmox node
- Nginx Proxy Manager for internal reverse proxy
- Semaphore UI for orchestragin OS maintenance/updates
- Adguard Home for local DNS server and adblock
- Ollama for running small models for testing/learning
- Cloudflared for tunneling my public facing apps to the internet
- Duplicati for backing up PBS datastore to offsite
- Debian 12 VM for running game servers
- Debian 12 VM for running storage-heavy apps like Jellyfin
- Debian 12 VM running Dokploy for development focused apps
- Zima OS for a few generic and rarely used apps

*Note: Could be more on less since I don't update this post often

---

## How I handle backups

- I run Proxmox Backup Server as an LXC on my Proxmox host (bad, don't do it)
- I passthrough the SSD I use for backup into that LXC as datastore and back up my node to it
- I use Duplicati to back up the datastore to an S3 bucket offsite

*Note: Solution could change as I don't update this post often

---

## Future upgrades

- Probably upgrade the router (current one is WiFi 6, planning for WiFi 7 or better)
- Probably getting another system to run Proxmox Backup Server (PBS)
- Maybe a non crappy UPS that can send shutdown signal to my hardware in case electricity goes out
- Probably swap from Mini PC to ITX build