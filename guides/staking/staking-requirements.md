---
title: Staking Requirements
description: Hardware requirements for staking
published: true
date: 2022-10-08T09:46:39.534Z
tags: guides
editor: markdown
dateCreated: 2022-10-05T08:33:03.016Z
---

# Staking Requirements

## **Operating System:**

All major Operating Systems (OS) are supported, but the community recommended OS is Ubuntu LTS or derivatives. Any Linux distribution can be used however the guides have been tailored for Ubuntu.

## **Computer Requirements:**

The daemon is tested and works flawlessly on a Raspberry Pi 3B+ with 1GB Ram, but the minimum recommendations are as follows to account for growth:

### **ARM:**

The Raspberry Pi 4B with 2GB RAM or equivalent SBC with 2GB with a min of 64 GB SD card (Daemon /CLI on Linux only).

### **x64:**

Any processor with 4GB RAM. Make sure that you have at least 30GB free hard disk space before you install the wallet.


> **Note:** The full node will download the complete copy of the blockchain database and as of today the extracted database is about 16 GB in size and grows over time. Lite nodes will only maintain block headers and signature chain data minimizing the storage impact dramatically, 250MB approximately.
{.is-info}

## **Modular Wallet Design:**

Nexus wallet includes modular functionality consisting of the interface, module framework and core. The intuitive interface provides users and businesses an easy and seamless experience. A node can also be run as a daemon exclusively with management available via API or remote interface. This is advantageous when running a staking node on a headless system like a Raspberry Pi or NUC.

## **Economical Implementations and IoT:**

The PoS fundamental principle is securing the network, and for that it provides an incentive. Node operators incur expenses with the hardware, management, bandwidth and electricity. The instructions in this section provide an optimal configuration for strict budgets and the IoT industry.

### **General Users (GUI Wallet):**&#x20;

Any computer which meets the minimum requirements, If staking is the only service planned an Intel NUC core i3 / Ryzen 3 or equivalent with 4GB RAM and 120GB SSD is recommended. If the staking computer will be used for other purposes, increase memory and disk space appropriately.


> Intel NUC or equivalent will be a good choice if looking for standalone staking node
{.is-info}



### **Advanced Users (CLI Wallet):**&#x20;

Raspberry Pi (RPI) 4 with 2/4GB, NUC or equivalent will run the headless core and users can control it via the interface from another computer. (RPI can run only the CLI daemon so command line interaction is necessary. Nexus has great step-by-step guides to aid those who are unfamiliar.)

![Nexus wallet daemon staking on a Raspberry Pi 4 takes just 243 MB of RAM and is extremely resource conservative overall.](https://nexus.io/ResourceHub/images/guide/stake-guide1.png#)The core is  very light on resources even on a Raspberry Pi 
