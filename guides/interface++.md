---
title: Interface - Tritium++
description: 
published: false
date: 2022-12-04T16:45:20.808Z
tags: 
editor: markdown
dateCreated: 2022-10-05T08:30:29.035Z
---

# Nexus Interface - Tritium++

The Tritium++ (5.1) is the latest update to the Nexus core, which brings some major changes, features and a fully overhauled API layer. This update also required a major update to the interface.

> This guide is for Interface version 3.1.0 and beyond which has the Tritium++ embedded core.  
{.is-info}

## Introduction

In simple words `Interface` is the official desktop wallet which helps normal users to create user accounts/profiles, create accounts, tokens, assets, invoices, stake to secure the network and transact with other users. The Interface is available for windows, mac, linux and can be run on low powered SBC's like the Raspberry Pi. `NXS` the cryptocurrency powering the network is not compatible with any other third-party wallet or hardware wallets due to the disparate architecture that manages keys and assets on-chain resembling a cloud service, along with increased security standards compared to other blockchains (512 bit keys compared to 256 bit keys).

The Interface is modular and consists of the `Core` and the `user interface`. This helps normal users to access all features easily install and transact with graphical interface and empowers advanced users to run the core as a daemon on servers or headless machines and access using the Interface in manual core mode or API's. This version also supports the lite mode which will make it spossible for users to be start transcating in a few minutes of installing the wallets. Additional features can be enabled by the use of modules (extensions) in a safe sandboxed environment. 

The Interface supports both, Tritium++ and the Legacy chain. This is enabled by the two modes and the user can switch between the Tritium++ and legacy modes.

&nbsp;

## New Features - Core
 
- Query DSL
- Contract Templates
- Templated API
- Object Modelling
- Dynamic Indexing Services
- New Profiles API, Sessions API, & Register API
- Complete API overhaul, performance is multiples faster.
- Operators such as sum, sdev, array, etc.
- Recursive sorting and filtering
- Data modelling such as unique, array, etc.
- Safemode for key generation security
- autotx for background processing
- Client mode support for mobile wallet.
- Peer-to=Peer (P2P) marketplace.
- Optional SSL.

&nbsp;

 ## New Features - Interface
 - Can be run as a lite node or as a full node.
 - QR code integration for seamless transactions.
 - Optional SSL for secure communication.

The Interface can be run in two modes, users can switch between the two modes from settings:
   - Lite Mode (Default)
   - Full Mode

## Lite Mode (Default)
This mode enables normal users to connect to the Nexus network fast and easily. In the lite mode the interface connects directly to the Nexus network and downloads the lite blockchain (block headers & profile info) which at the time of writing is approximately 300MB in size. The user should be able to transact within 5 min of installing the wallet, depending on internet connection. The lite mode connects directly to the Nexus network peers unlike other lite wallets which connect to third party proxy servers. This mode is useful for users who transact occasionally or HODL.

## Full Mode
In this mode the node will act like a full node which requires the full blockchain to be downloaded from peers and verified. The database is approximately 16GB in size at the time of writing. Stakers, miners, seed nodes and Dapp backend nodes will run as full nodes.


> For users still using legacy chain, we recommend you migrate to Tritium.
{.is-info}

If any user is facing issues with the Nexus Interface, or need assistance on anything related to Nexus, we will be happy to help, on the `Nexus Support` telegram channel linked below:

 - <a href="https://t.me/NexusSupport" target="_blank">NexusSupport</a>
 

## Chapters

- [Overview *The Wallet Homepage*](/en/guides/interface++/overview)
- [User Module *The User Module - Accounts, Staking, Tokens, Names and Assets*](/en/guides/interface++/user-module)
- [Send *The Send Module - Send NXS & Tokens*](/en/guides/interface/send)
- [Transactions *The Transactions Module*](/en/guides/interface/transactions)
- [Address Book *The Address Book*](/en/guides/interface/address-book)
- [Console *The Interface Console - For advanced users*](/en/guides/interface/console)
- [Settings *The Settings Module*](/en/guides/interface/settings)
- [Create User Account *How to create a User Profile or Account*](/en/guides/interface/create-user-account)
- [Create a NXS Account *How to create a NXS account*](/en/guides/interface/create-a-nxs-account)
{.links-list}

 