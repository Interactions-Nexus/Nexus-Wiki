---
title: Create Asset
description: Create Asset using the Interface
published: true
date: 2022-12-07T22:45:41.956Z
tags: guides
editor: markdown
dateCreated: 2022-10-05T08:26:14.466Z
---

# Create an Asset

This guide will help users to create an **Asset,** also popularly known as  **NFT's**, check the asset details and transfer ownership using the Nexus Interface.

Before we start to create an asset, users need to be familiar with some of the concepts and parameters used with assets.

>Creating an asset has a fee of 1 NXS and "Asset Name" has a fee of 1 NXS. Total cost of an Asset with name will be 2 NXS.
{.is-info}

## Asset Parameters

### Asset Name

This is a globally unique name for the asset. Duplicate names will not be allowed. If creating a bunch of  assets with a similar name then use a serial no with the name.

>Asset Name has a separate fee of 1NXS. Users can opt not to create an Asset Name and can use the register address to access or search the Asset.
{.is-info}


Naming Convention:
* Use a unique name if creating an asset. Short names are preferred, but if needed use long names.
* Names can contain upper lower case letters, numbers and special characters.
* If creating an asset of a real world assets like real estate, provide clear and precise information for the Asset Name.&#x20;
* If creating a bunch of Assets / NFT's, say from a single art collection, then suffix the collection name with a unique serial Number series Ex: "_Iron Maiden #0001."_

### Asset Data

This section is for the asset data or metadata. The information provided here helps to give validity to the asset and its value. The asset data has to be precise, complete and should enable anyone to check authenticity of the asset its backing. The data provided will depend on the digital or physical asset which is being backed as a blockchain Asset. &#x20;

>Asset Data has a limit of 1KB and this is binding. An asset can hold approximately 990 - 995 characters including spaces. This excludes the Asset Name.
{.is-info}

To easily count the characters for the Asset data use the link below:

<a href="https://wordcount.com" target="_blank">https://wordcount.com</a>

> **Note:** If creating an Asset of a digital art, which basically is an image file, provide a md5 hash of the original image for anyone to check the authenticity of that particular file. If all the details are provided without the file hash, the asset will not be of any use, due to the fact that no one will be able to confirm the authenticity of the file which represents the asset.
>{.is-info}


Asset Data is entered in fields which represent a single line in the image above.

#### Name:

The first column is the field name, which is the name for the data you are going to add like Description, Owner, Artist, Hash etc.

#### Value:

The second column is the value of the field, like the owner's name.

#### Mutable:

Third is the radio button to enable mutable field (default is disabled). Mutable fields can be changed anytime by the sigchain owner of the asset. This is very helpful in case you have a house minted as an Asset and once you sell the house, transfer the asset to the new owner and he can change the "Owner" field to his name.

>Only make the fields mutable which really need. Ex When creating a asset which refers to a house, The "Owner" field needs to be mutable, this is due to the  where as Location, Name, Registration No.&#x20;
{.is-info}

#### Type:

String: It is a data type used to represent text. It is comprised of a set of characters that can also contain spaces and numbers. For example, the word "hamburger" and the phrase "I ate 3 hamburgers" are both strings. Even "12345" could be considered a string.&#x20;

Date types uint8, uint16, uint32, uint64, uint128, uint256, uint512 and uint1024 represents an unsigned integer number stored with 8, 16, 32 or 64 bit.&#x20;

|       Type | No of Bits | Min - Max Value                |
| ---------- | :--------: | ------------------------------ |
| uint8      |      1     | 0 - 255                        |
| unit16     |      2     | 0 - 65535                      |
| uint32     |      4     | 0 - 4,294,967,295              |
| unit64     |      8     | 0 - 18,446,744,073,709,551,615 |
| unit256    |     16     | 0 - 2^256-1                    |
| uint512    |     32     | 0 - 2^512-1                    |
| uint1024   |     64     | 0 - 2^1024-1                   |

**Max Length:**

This field is enabled only if the field is selected as mutable and the type is selected as "string". This is important as this will allow to limit the length of the field when it's changed later and to contain the Asset Data within the 1 KB limit.

## Create an Asset

To create an asset using the Interface follow the steps below:

* Open the Nexus Interface, make sure the wallet is fully synched. Log into the user account (Sigchain).
* In the Overview page, at the bottom click on the "_User"_ module. This opens the User page.
* In the User page, on the left side click on the "_Assets_" tab. The Assets page will list the assets owned by the Sigchain.
* In the Assets page click on "Create a new asset". This opens the _Create a new asset_ page.
* In this page the user has to provide the name and data which define the asset.&#x20;
  * **Add Another Field:** To add another field click on the "+ADD FIELD" button below the first field.
  * **Remove Field:** To remove a field hover the mouse pointer on that field, a "x" icon will appear on the left side of the field, click on it to remove the field.
* Once the data is provided, double check to make sure everything is in order. At the bottom you can see the estimated cost to mint this asset. Click on the "CREATE ASSET" button on the bottom of the page.

>The fees will be deducted automatically from the "default" account, make sure that you have NXS to cover the fees or it will fail to mint the asset.&#x20;
{.is-info}

* Once the asset is minted you will see a new entry in the "Assets" page.

## Asset Details

A user can check the details of an asset, it includes all the asset data saved with that asset.  To check the asset details, on the Assets page, click on the asset which will open the Asset Details page&#x20;

![asset_details_.png](/asset_details_.png)

### Asset History

A user can check the history of an asset, history includes creation, update, transfer, claim and tokenize. To check the asset history, on the Assets page, click on the "Asset" which will open the Asset Details. At the bottom left of this page click on "View history", this will open the history page which will list all the changes that happened with that asset.   &#x20;

![asset_history.png](/asset_history.png)

### Transfer the Asset

The asset owner might sell the Asset and for that he needs to transfer ownership of the asset to the buyer.&#x20;

* To transfer ownership of the asset click on that asset, which opens the "Asset Details" page.
* At the bottom right of the page click on "Transfer Ownership". This will open the "Transfer asset" page.

![transfer_asset.png](/transfer_asset.png)

* In this page confirm the asset Name, asset address and in the "Transfer To" field enter the username or the userID of the buyer.
* To confirm, on the bottom of the page click on "Transfer Asset" which will transfer the asset to the buyer.

>The buyer will claim the Asset automatically via the Interface, There will be a fee of 1 NXS to claim, this creates a local name of that asset on the receivers Sigchain.
{.is-info}
