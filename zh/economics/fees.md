---
title: 操作费用
description: Nexus 麟社公共网络 - 操作费用
published: true
date: 2022-12-13T11:46:13.624Z
tags: 
editor: markdown
dateCreated: 2022-12-13T11:46:13.624Z
---

# Fees

Nexus has fees for the various operations on the public chain like creating assets, invoices, names and tokens. This is to maintain security of the network, prevent misuse, spam and resource squatting.

> The fees are only applicable for the mainnet.
{.is-info}



The breakdown of fees for all operation types is as follows:

| Action                                          | Cost | Note  |                                   
|---|---|---|
| Sending NXS or other tokens                     |   0  |      |
| Receiving NXS or other tokens                   |   0  | If the debit being credited has contract conditions, a fee may apply for executing those conditions depending on their complexity. A fee-free threshold for conditions means that simple contract conditions such as adding an expiry to a debit will mean crediting them will be free |                                                         
| Transferring assets (NFTs) and other registers  |   0  |              |
| Claiming ownership of assets or other registers |   0  | If the register being claimed is a named register, i.e. there exists a local name for it in the previous owners signature chain, then a corresponding local name is created for it when claiming. This name creation attracts a 1 NXS fee  |
| Claiming ownership of assets or other registers |   0  | If the register being claimed is a named register, i.e. there exists a local name for it in the previous owners signature chain, then a corresponding local name is created for it when claiming. This name creation attracts a 1 NXS fee<br><br>If the transfer being claimed has contract conditions, a fee may apply for executing those conditions depending on their complexity. A fee-free threshold for conditions means that simple contract conditions such as adding an expiry to a transfer will mean claiming them will be free              |
| Creating a NXS or token account                 |   0  | If the account is given a name, there is a 1 NXS fee applied for the creation of the name register              |
| Creating an asset or other register             |  1+  | The fee is calculated based on the size of data stored in the register at 0.001 NXS per byte. However there is a minimum fee of 1 NXS and (at the time of writing) a maximum register size of 1Kb, meaning the fee will vary between 1 an 1.024 NXS         |
| Updating an asset or other register             |   0  |          |
| Creating a local name                           |   1  |          |
| Creating a global name                          | 2000 |          |
| Creating a namespace                            | 1000 |          |
| Creating a token                                |  1+  | <p>The fee calculation for creating a token is based on the number of total supply of token divisible units, which in turn is calculated from the token supply and the number of decimals in the token definition. <br>For example, a token with supply 1,000,000 and 2 decimals has a total of 100,000,000 divisible units. The actual fee calculation is a logarithmic scale based on this number, using the formula:</p><p>Fee = (log10(divisible units) – 2) * 100</p><p>A minimum fee of 1 NXS always applies. This yields the following fees based on number of divisible units</p><p>100 = 1 NXS<br>1,000 = 100 NXS<br>100,000 = 300 NXS<br>1,000,000 = 400 NXS<br>1,000,000,000 = 700 NXS<br>1,000,000,000,000 = 1000 NXS</p> |
| Transaction Fee                                 |  0-1 | <p>A transaction fee is applied whenever a transaction is created within 10 seconds of the last transaction within a signature chain. The fee is calculated based on the number of contracts within the transaction at a rate of 0.01 NXS per contract, of which there can be a maximum of 100 (at the time of writing). Therefore the transaction fee will be between 0 and 1 NXS.</p><p><br>The transaction fee is applied in addition to any of the other fees described in this table</p>           |

&nbsp;

## Advanced Contract Execution Fee:

When Advanced Contracts are launched (with core V7.0), except the basic contracts (which are already free)  contract execution will be charged as they require computation cycles and the fee will be calculated before execution and the user will pay the exact fee shown, unlike GAS on Ethereum.



