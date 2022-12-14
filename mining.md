---
title: Mining
description: 
published: true
date: 2022-10-19T11:35:15.086Z
tags: mining
editor: markdown
dateCreated: 2022-10-06T10:10:39.620Z
---

# Mining

Nexus has a three consensus channels, two mining `hash`, `prime` and the third is the `stake`. Anyone can mine on Nexus and does not need permission. The Nexus developer team has a dedicated mining developer team to maintain the miner and pools.

## Mining Support:

For any help or support related to mining, join our Telegram channel linked below:

[NexusMiners](/https://t.me/NexusMiners)

## Mining Channels:

* **Prime Mining:** GPU - Supports both Solo & Pool.
* **Hash Mining:** GPU or FPGA’s - Supports both Solo & Pool.

> **Good to Know:** We don't recommend CPU prime or hash mining as it is not profitable and only used for testnet mining.
{.is-info}

### Solo Mining:

Solo means single or individual mining. It requires the miner to be connected to the Nexus wallet. The wallet and miner can be run on the same or a separate computer especially when mining with FPGA’s.&#x20;

> **Good to Know:** Solo mining is not profitable for prime and hash, unless you have a very big mining setup.
{.is-info}

### Pool Mining

Pool mining is similar to group mining, and the miner has to be connected to a mining pool. The miner is directly connected to the pool, and the mining rewards are paid to miners depending on the percentage of individual hash rate. There are fees to mine on a pool and that is deducted from the mining payouts.&#x20;

## Mining Pools For Nexus:

The mining team maintains open mining pools for miners:

## Prime Pool:

Link to the prime pool webpage:

[primepool.nexus.io](https://primepool.nexus.io)

The Nexus mining team has made available an open prime pool. To use this pool copy the below lines in the miner config.

```
    "wallet_ip" : "primepool.nexus.io", 
    "port" : 50000,
```

## Hash Pool:

The Nexus mining team has made available an open hash pool.  To join the pool, use the below lines in the miner config.

```
    "wallet_ip" : "hashpool.nexus.io", 
    "port" : 50000,
```

Link to the hash pool webpage:

[hashpool.nexus.io](https://hashpool.nexus.io)


## Compatible Mining Hardware

The NexusMiner can use CPU, GPU for Prime and FPGA for Hash mining. CPU mining is not recommended as it is not efficient.

### GPU:

If using GPU mining, the NexusMIner V1.5 supports both nvidia and AMD GPU's. The CUDA cores from Nvidia are fully supported and work efficiently. AMD support has been enabled recently only for prime only on linux and will take some time to be fully efficient.&#x20;

> **Good to Know:** AMD GPU support is still in its early days and will be improved in the future
{.is-info}

To get the best out of the nvidia graphics cards, we highly recommend to use the latest graphics drivers and [MSI Afterburner](https://www.msi.com/Landing/afterburner/vga).


> Do not install the Nvidia content creator drivers, the miner will not work properly.
{.is-warning}

## FPGA:

FPGA miners for Nexus are only available from [Blackminer](https://www.hashaltcoin.com/en/miners). These miners can only be used for Hash mining.

### Mining Calculator:

To get a better understanding of the mining efficiencies of different hardware, use the mining calculator linked below:

[Mining Calculator Link](https://primepool.nexus.io/mining\_calc/)

## Chapters
- [Mining on Windows *How to mine on windows*](/en/mining/mining-on-windows)
- [Mining on Linux *How to mine on linux*](/en/mining/mining-on-linux)
- [Miner Configuration *How to configure the miner*](/en/mining/miner-config)
- [Hash-Rate Table *This is the Nexus mining hash rate table*](/en/mining/hash-rate-table)
{.links-list}
