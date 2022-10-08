---
title: Create Tokenized Asset
description: Create a tokenized asset on Nexus
published: true
date: 2022-10-08T16:21:05.980Z
tags: guides
editor: markdown
dateCreated: 2022-10-05T08:26:17.959Z
---

# Create Tokenized Asset

### What is Asset Tokenization

`Asset Tokenization` also referred as `Asset Backed Tokens` or `Tokenized Assets` is a new concept that uses digital tokens to fractionalize ownership of assets such as property, jewellery or fine art and uses contracts on blockchain to manage these ownership rights

This guide will help users to create a ***Tokenized Asset*** using the Nexus Interface.

Before we start to create an asset tokenization, users need to be familiar with some of the concepts and parameters used.

To tokenize an asset, user needs to create the asset and token as per the guides linked below.

-   [Create Asset](/en/guides/create-asset)
-   [Create Token](/en/guides/create-token)

> Name the Asset and Token accordingly so they can be identified easily.

## Create Asset Tokenization

To create a tokenised asset using the Interface follow the steps below:

Open the Nexus Interface, make sure the wallet is fully synched. Log into the user account (Sigchain).

In the Overview page, at the bottom click on the "*User"* module. This opens the *User* page.

In the User page, on the left side click on the "*Assets*" tab.

Under the Assets page, all the assets owned by the user account / Sigchain will be listed.

Click on the Asset which is to be tokenized, this opens the "Asset Details" page.

![](/asset_details.png)

Asset Details

At the bottom right of this page click on "Tokenize". This will open the "Tokenize" page.

In this window you can choose the Token to tokenize the asset with, the available tokens list can be accessed using the drop down arrow.

Once the appropriate token is selected, click on the "Tokenize" button on the bottom of the page.

## Asset Payout

The main utility of tokenized assets is to enable fractional ownership and to share the revenue with the token holders. To send the payout to the token holders the user sends NXS equivalent in value to the revenue generated, to the asset address and it will be automatically be distributed as per the percentage token holdings of each holder.

{% hint style="warning" %}  
The payout is distributed taking the maxsupply as 100% of the tokens. If any tokens are still in the token generation address, the percentage of payout corresponding to the balance tokens will be returned to the sender.