---
title: Interface - Tritium++
description: 
published: false
date: 2022-10-31T13:42:44.633Z
tags: 
editor: markdown
dateCreated: 2022-10-05T08:30:29.035Z
---

# Nexus Interface - Tritium++

The Tritium++ (5.1) is the latest update to the Nexus core, which brings some major changes, features and a fully overhauled API layer. This update also required a major  update to the interface.

> This guide is for Interface version 3.1.0 and beyond which has the Tritium++ embedded core.  
{.is-info}

## Introduction

In simple words `Interface` is the official desktop wallet which helps normal users to create user accounts/profiles, create accounts, tokens, assets, invoices and transact with other users. The Interface is available for windows, mac, linux and can be run on low powered SBC's like the Raspberry Pi. `NXS` the cryptocurrency powering the network is not compatible with any other third-party wallet or hardware wallets due to the disparate architecture that manages keys and assets on-chain resembling a cloud service, along with increased security standards compared to other blockchains (512 bit keys compared to 256 bit keys).

The Interface is modular and consists of the `Core` and the `user interface`. This helps normal users to access all features easily install and transact with graphical interface and empowers advanced users to run the core as a daemon on servers or headless machines and access using the Interface in manual core mode or API's. Additional features can be enabled by the use of modules (extensions) in a safe sandboxed environment. 

The Interface supports both, Tritium++ and the Legacy chain. This is enabled by the two modes and the user can switch between the Tritium++ and legacy modes.

The Interface can be run in two modes:
   - Lite Mode (Default)
   - Full Mode

## Lite Mode (Default)
This mode enables normal users to connect to the Nexus network fast and easily. In the lite mode the interface connects directly to the Nexus network and downloads the lite blockchain (block headers & profile info) which at the time of writing is approximately 300MB in size. The user should be able to transact within 5 min of installing the wallet, depending on internet connection. The lite mode connects directly to the Nexus network peers unlike other lite wallets which connect to third party proxy servers. This mode is useful for users who occasionaly use the wallet to transact or to HODL.

## Full Mode
In this mode the node will act like a full node which requires the full blockchain to be downloaded from peers and verified, approximately 16GB in size. Stakers, Miners, seed nodes and Dapp backend nodes have to run in full mode. Users can swit


> We recommend users to who have NXS in the legacy chain to migrate to Tritium.
{.is-info}

If any user is facing issues with the Nexus Interface, or need assistance on anything related to Nexus, we will be happy to help, on the `Nexus Support` telegram channel linked below:

 - <a href="https://t.me/NexusSupport" target="_blank">NexusSupport</a>
 

## Chapters

- [Overview](/en/guides/interface/overview)
- [User Module](/en/guides/interface/user-module)
- [Send](/en/guides/interface/send)
- [Transactions](/en/guides/interface/transactions)
- [Address Book](/en/guides/interface/address-book)
- [Console](/en/guides/interface/console)
- [Settings](/en/guides/interface/settings)
- [Create User Account *How to create a user account (Profile)*](/en/guides/interface/create-user-account)
- [Create a NXS Account *How to create a NXS account*](/en/guides/interface/create-a-nxs-account)
{.links-list}

 