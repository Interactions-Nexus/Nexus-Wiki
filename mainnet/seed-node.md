---
title: Seed Nodes
description: How to run a seed node for mainnet
published: true
date: 2022-10-31T05:29:35.341Z
tags: nodes
editor: markdown
dateCreated: 2022-10-29T01:44:48.577Z
---

1.  **Seed Node definition**: A seed node is first node that other nodes connect to when they first come online. The seed node helps new nodes get the list and location of all the other nodes in the swarm.  Once the new node has the list, it will begin connecting itself into the mesh.

2. Seed Node Minimum Requirements - 
	
    - High availability - Your node should be always on and available
    - Publicly reachable - Your node needs to have a publicly reachable IP and firewall open on the ports listed below
    - High Bandwith - Your node needs to have a high-bandwidth always on Internect connection
    - Resolvable DNS name
    
    A typical low-cost VPS or shared hosting server will usually meet these requirements

3.  In order to make a see node, first follow the directions to create a Mainnet Node: [Run a Mainnet Node](https://wiki.nexus.io/en/mainnet/run-a-mainnet-node)

4.  Once you have your node running, there are a few additional steps:
    -   Add the following to nexus.conf:

```plaintext
#Unified time synchronization
unified=1
#Allow all IP's to connect to your node
llpallowip=*.*.*.*:9324
#Increase your maximum connections
maxincoming=303
maxconnections=333
```

-   Open ports 9324/tcp (unified time) and 9888/tcp (main data port)

```plaintext
sudo ufw allow 9324/tcp
sudo ufw allow 9888/tcp
```

5.  Ensure your node has a resolvable DNS name pointing to it.
6.  Contact an admin for the seed node working group to join the working group. Admins are:
    -   @aeonwise
    -   @Radient4751
7.  Once you are in the working group, we will add your node's DNS name to [seeds.cpp](https://github.com/Nexusoft/LLL-TAO/blob/merging/src/LLP/seeds.cpp) on GitHub.