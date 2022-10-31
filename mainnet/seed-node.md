---
title: Seed Nodes
description: How to run a seed node for mainnet
published: true
date: 2022-10-31T11:56:47.271Z
tags: nodes
editor: markdown
dateCreated: 2022-10-29T01:44:48.577Z
---

# Seed Nodes

This guide will help you to setup a new seed node or convert an existing node to a seed node.

## What is a seed node?
When a new wallet comes online, it cannot automatically self discover and connect to the Nexus network, this is where seed nodes come to the rescue. The seed node DNS is hadcoded in the software and when a new wallet launches it connects to these seed nodes and gets the list of all the other nodes. Once the new node has the list, it will begin connecting itself to peers with the best connections and becomes part of the network.

## Minimum Requirements
A typical low-cost VPS or shared hosting server will usually meet these requirements.

- High Availability - The node should be always on and available.
- Publicly Reachable - The node needs to have a publicly reachable IP and firewall open on the ports listed below.
- High Bandwith - The node needs to have a high-bandwidth always on Internect connection.
- Resolvable DNS name - We can list the node with one of the seed node DNS.
    
To setup a new node, follow the directions to create a mainnet node in the link below: 

- [Run a Mainnet Node *How to setup a mainnet CLI node*](https://wiki.nexus.io/en/mainnet/run-a-mainnet-node)
{.links-list}

## Seed Node Configuration
Once you have your node running, follow the additional steps below:

1.  Add the following to nexus.conf:

```plaintext
#Unified time synchronization
unified=1
#Allow all IP's to connect to your node
llpallowip=*.*.*.*:9324
#Increase your maximum connections
maxincoming=303
maxconnections=333
```
2. Open ports 9324/tcp (unified time) and 9888/tcp (main data port)

```plaintext
sudo ufw allow 9324/tcp
sudo ufw allow 9888/tcp
```

3.  Ensure your node has a resolvable DNS name pointing to it.
4.  Contact an admin for the seed node working group to join the working group. Admins are:
    - <a href="https://t.me/aeonwise" target="_blank">@aeonwise</a>
    - <a href="https://t.me/Radient4751" target="_blank">@radient</a>
   
5.  Once you are in the working group, we will add your node's DNS name to [seeds.cpp](https://github.com/Nexusoft/LLL-TAO/blob/merging/src/LLP/seeds.cpp) on GitHub.