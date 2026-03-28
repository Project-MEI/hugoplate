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

I decided to go with [Proxmox VE](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) since considered free (once you disable the NAG screen), but most importantly the versatility it offers if I decide to play with unfamiliar operating systems and the amount of functionality it has over something like TrueNAS or Unraid.

I also just had a lot of time to burn so Proxmox was the perfect choice for me to learn about devops and sysadmin in general.

---

## The Workloads

I run a few virtual machines and segregate workloads based on the application types and what services they're running. Most runs Debian server with all apps running in Docker and managed via Dockhand. One VM is running the free version of ZimaOS for non important apps that I can easily add or remove. Critical apps like Adguard (DNS Server) or Semaphore UI (Ansible UI) I run as LXC containers on the Proxmox host (courtesy of https://community-scripts.org/). I don't do clustering or High Availability (HA), I'm not that senile yet.

---

## Backup Strategy

I run Proxmox Backup Server (PBS) as an LXC container and backup all of the VMs to it, with a mounted drive set as datastore. The same drive I then have mounted on another LXC running Duplicati, configured to sync my backups to an offsite S3 bucket. Since PBS and Duplicati deduplicates backup on its own, it save time and storage cost. Eventually, I seek to run PBS on its own separate machine but for now this setup works for non catastrophic failures since I can quickly recover snapshot and files in case of a data loss.

---

## What's next

When the time comes for me to go senile I'll eventually explore high availability and cluster my setup. I also plan to add a dedicated GPU and connect it via Oculink to that Mini PC and run some AI models on it when GPU prices make sense again.