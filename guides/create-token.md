---
title: Create Token
description: Create Token Using Nexus Interface
published: true
date: 2022-12-07T23:53:21.237Z
tags: guides
editor: markdown
dateCreated: 2022-10-05T08:26:11.061Z
---

# Create a Token

This guide will help users to create a **Token** using the Nexus Interface

Before we start to create a token, users need to be familiar with some of the concepts, properties, parameters and fees for tokens.

> Tokens on Nexus work completely different compared to other blockchains. There are a lot of differences which a user needs to undesrstand, so we recommend users to read this complete guide.
{.is-warning}


## Tokens on Nexus:

To create and transact tokens on Nexus, users first need to understand the different token accounts and properties:

Once the token is created, the token generation address will be listed in the "Tokens" page. This is the token generating address, and not a token account. This generating address is owned by the profile (user account) which issued the token. 

> Every user who wants to transact the token needs to create a token address linked to that particular token.
{.is-info}

Once created, the token has the following properties:
- tokenname - The global name for the token if it is created.
- maxsupply - The maximum number of tokens that will exist.
- currentsupply - The number of circulating tokens that have been distributed to token accounts.
- balance - The number of tokens that have not yet been distributed (maxsupply - currentsupply).
- decimals - No of decimal places.
- address - This is the token register address or token generation address.

### Token Generation Address

This is the register address which generates that particular token and tokens in this address are out of circulation. Tokens when sent out to a token account come into circulation. Users can send tokens back to the generation address to remove them from circulation.

### Token account:

This is a normal token account which can send or receive token from the generation address or token account. Each token account is linked only to a particular token and cannot receive any other token. Every user has to manually create a token account to transact a particular token.


> Token accounts can only receive the particular token they are linked to. They cannot accept NXS or any other token. The standard "default", "trust" or any NXS accounts cannot accept any tokens.
{.is-warning}


## Token Parameters

Token parameters are what define a token like token name, supply and decimals. Learn more about them below:

### TOKEN NAME

The token name resolves differently in tritum and tritium++.

##### Tritium

This is a local name to identify the token and is optional. This name resides inside the user account (Sigchain) and is not valid outside it.

Token name has a separate fee of `1 NXS`. Issuer can opt not to create a token name and can use the register address to access or search the Asset. This is a local name and is not valid outside the Sigchain.

> If there is a need for a unique global name (ticker) for the token, then the issuer needs to create a Global name and link it to the token.
{.is-info}


##### Tritium++ (Upcoming update)

In tritium++ this resolves to a global name (ticker) to identify the token and is optional. This name is a globally recognized name on the network. The profile which created the token with the global name will be the owner and this global name can be transferred to other profiles.

> Token global name has a separate fee of `2000 NXS`. Issuer can opt not to create a token name and can use the register address to access or search the token.
{.is-info}

### SUPPLY

This is the total number of fungible tokens that needs to be generated. The fee increases with a higher supply. Check the fees [here]

> The max supply of the token cannot be increased once the token is generated. Tokens can be burnt to remove them out of circulation.
{.is-warning}

### DECIMAL

This is the no of decimal places for the token, increasing the decimal places also increases the fee. Decimal units are required for micro transactions and is set depending upon the token usage and tokenomics.


## Token Minting Fees

The fee is based on the number of token divisible units you define (the combination of supply and decimals). There is a minimum fee of 1 NXS and the calculation is linear thereafter, so that each additional significant digit costs an additional 100 NXS. E.g.

100 units = 1 NXS

1000 units = 100 NXS

1000000 units = 400 NXS

10000000000 units = 800 NXS

For more detailed information check [Fees.](/en/economics/fees)

&nbsp;

## Create a Token

To create a token using the Interface follow the steps below:

* Open the Nexus Interface, make sure the wallet is fully synched and log into the user profile (Sigchain).
* In the Overview page, at the bottom click on the `User` module. This opens the User page.
* In the User page, on the left side click on the `Tokens` tab.
* In the Assets page click on `Create a new token`. This opens the *New Token* page.
* In this page the user has to provide three parameters which define the token. The parameters  and their details are given below:
* Once the parameters are provided, click on the `Create token` button on the bottom of the page.
* Once the token is confirmed on the blockchain, the token address will be listed in the `Tokens` page.
* To check the details of any token, click on the token address in the `Tokens` page and the token details page will open with the details.