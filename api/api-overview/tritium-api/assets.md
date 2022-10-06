---
title: assets
description: ASSETS API
published: true
date: 2022-10-05T08:33:55.357Z
tags: 
editor: markdown
dateCreated: 2022-10-05T08:28:58.174Z
---

# ASSETS

An asset is a user-defined data structure that is stored in an object register, owned by a particular signature chain. Assets can hold one or more pieces of data and users can define the fields (name, data type, mutability) that data is stored in. The assets API supports several formats for defining the object data structures giving users and developers varying levels of functionality, including per-field type definition and mutability.

The `basic` format allows callers to define an asset in terms of simple key-value pairs. It assumes that all fields are read-only and all values are stored using the string data type. `basic` assets are always immutable and cannot be updated once created.

The `JSON`, `ANSI`, and `XML` \~formats allow callers to provide a detailed definition of the asset data structure, with each field defined with a specific data type and mutability. Assets defined with one of the complex formats can be updated after their initial creation.

The `raw` format differs from the other formats in that the asset data is not stored in object register, but instead is stored in a read-only state register. The raw format is useful when developers wish to store arbitrary binary data on the Nexus blockchain, without incurring the overhead of defining an object.

### `Named Shortcuts`

For each API method we support an alternative endpoint that includes the asset name or register address at the end of the the URI. This shortcut removes the need to include the asset name or address as an additional parameter.

For example `assets/create/asset/myasset` is a shortcut to `assets/create/asset?name=myasset`.

Similarly `assets/get/asset/8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P` is a shortcut to `assets/get/asset?address=8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P`

The logic for resolving the shortcut to either a name or address is that if the data is 64 characters of hexadecimal then it will be assumed to be a register address. Otherwise it will be considered a name.

## `Methods`

The following methods are currently supported by this API

[`create/asset`](assets.md#create-asset)\
[`get/asset`](assets.md#get-asset)\
[`update/asset`](assets.md#update-asset)\
[`transfer/asset`](assets.md#transfer-asset)\
[`claim/asset`](assets.md#claim-asset)\
[`list/asset/history`](assets.md#list-asset-history)\
[`tokenize/asset`](assets.md#tokenize-asset)\
[`get/schema`](assets.md#get-schema)

### `create/asset`

This will create a new asset or object register. The API supports an alternative endpoint that can include the new asset name in the URI. For example `/assets/create/asset/myasset` will resolve to `assets/create/asset?name=myasset`.

#### Endpoint:

`/assets/create/asset`

{% swagger method="post" path="/assets/create/asset" baseUrl="http://api.nexus-interactions.io:8080" summary="create/asset" %}
{% swagger-description %}
This will create a new asset or object register
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the asset should be created with. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
An optional name to identify the asset. If provided a Name object will also be created in the users local namespace, allowing the asset to be accessed/retrieved by name. If no name is provided the asset will need to be accessed/retrieved by its 256-bit register address
{% endswagger-parameter %}

{% swagger-parameter in="body" name="format" required="false" %}
The format the caller is using to define the asset. Values can be 

`basic`

 (the default), 

`raw`

, 

`JSON`

, 

`ANSI`

 (not currently supported), or 

`XML`

 (not currently supported). This is an optional field and the value 

`basic`

 is assumed if omitted
{% endswagger-parameter %}

{% swagger-parameter in="body" name="data" %}
If format is 

`raw`

, then this field contains the hex-encoded data to be stored in this asset. Raw assets are always read-only. All other preceding fields are ignored
{% endswagger-parameter %}

{% swagger-parameter in="body" name="<fieldname>:<value>" %}
If format is 

`basic`

, then the caller can provide additional = pairs for each piece of data to store in the asset
{% endswagger-parameter %}

{% swagger-parameter in="body" name="json" %}


`json` : If format is `JSON`, then this field will hold the json definition of the asset as a JSON array of objects representing each field in the object. It uses the following format:&#x20;

`name` : The name of the data field.

``

`type` : The data type to use for this field. Values can be `uint8`, `uint16`, `uint32`, `uint64`, `uint256`, `uint512`, `uint1024`, `string`, or `bytes`.

``

`value` : The default value of the field.

``

`mutable` : The boolean field to indicate whether the field is writable (true) or read-only (false).

``

`maxlength`: Only applicable to `string` or `bytes` fields where `mutable`=true, this is the maximum number of characters (bytes) that can be stored in the field. If no maxlength parameter is provided then we will default the field size to the length of the default value rounded up to the nearest 64 bytes
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="asset created" %}
```json
{
    "pin": "1234",
    "name": "watch",
    "format": "JSON",
    "json" :
        [
            {
                "name": "serial_number",
                "type": "uint64",
                "value": "123456789123456789",
                "mutable" : "false"
            },
            {
                "name": "description",
                "type": "string",
                "value": "This is the description of my asset",
                "mutable" : "false"
            },
            {
                "name": "shelf_location",
                "type": "string",
                "value": "Aisle 9 Shelf 2",
                "mutable" : "true"
            }
        ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// create / asset
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
    pin: "YOUR_PIN",
    name: "ASSET_NAME", //optional
    // session: "YOUR_SESSION_ID", //optional
    format: "JSON", //optional or "basic" ,"raw","JSON","ANSI","XML"
    // data: "HEX_ENCODED_DATA_TOBE_STORED_IN_THE_ASSET",//optional
    // <fieldname>=<value>//optional,
    json: [{
        name: "NAME_OF_DATA_FIELD",
        type: "string", //uint8, uint16, uint32, uint64, uint256, uint512, uint1024 ,string,bytes
        value: "default value of the field",
        mutable: true, //false for read-only
        // maxlength: 64, //in bytes 
    }]
}
fetch(`${SERVER_URL}/assets/create/asset`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```json
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "pin": "YOUR_PIN",
    "name": "ASSET_NAME",  # optional
    # "session": "YOUR_SESSION_ID", #optional
    "format": "JSON",  # optional or "basic" ,"raw","JSON","ANSI","XML"
    # "data": "HEX_ENCODED_DATA_TOBE_STORED_IN_THE_ASSET",#optional
    # <fieldname>=<value>#optional,
    "json": [{
        "name": "NAME_OF_DATA_FIELD",
        "type": "string",  # uint8, uint16, uint32, uint64, uint256, uint512, uint1024 ,string,bytes
        "value": "default value of the field",
        "mutable": True,  # False for read-only
        # "maxlength": 64, #in bytes
    }]
}
response = requests.post(f"{SERVER_URL}/assets/create/asset", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the asset should be created with. For single-user API mode the session should not be supplied.

`name` : An optional name to identify the asset. If provided a Name object will also be created in the users local namespace, allowing the asset to be accessed/retrieved by name. If no name is provided the asset will need to be accessed/retrieved by its 256-bit register address.

`format` : The format the caller is using to define the asset. Values can be `basic` (the default), `raw`, `JSON`, `ANSI` (not currently supported), or `XML` (not currently supported). This is an optional field and the value `basic` is assumed if omitted.

`data` : If format is `raw`, then this field contains the hex-encoded data to be stored in this asset. Raw assets are always read-only. All other preceding fields are ignored.

`<fieldname>=<value>` : If format is `basic`, then the caller can provide additional = pairs for each piece of data to store in the asset.

`json` : If format is `JSON`, then this field will hold the json definition of the asset as a JSON array of objects representing each field in the object. It uses the following format:

* `name` : The name of the data field.
* `type` : The data type to use for this field. Values can be `uint8`, `uint16`, `uint32`, `uint64`, `uint256`, `uint512`, `uint1024`, `string`, or `bytes`.
* `value` : The default value of the field.
* `mutable` : The boolean field to indicate whether the field is writable (true) or read-only (false).
* `maxlength`: Only applicable to `string` or `bytes` fields where `mutable`=true, this is the maximum number of characters (bytes) that can be stored in the field. If no maxlength parameter is provided then we will default the field size to the length of the default value rounded up to the nearest 64 bytes.

{% hint style="warning" %}
There is a limit of 1KB for asset data to be saved in the register, excluding the Asset Name
{% endhint %}

#### Example:

The following is an example of an asset defined using the `basic` format:

{% hint style="info" %}
**NOTE**: In this example the asset is entirely read-only and no fields can be updated.
{% endhint %}

```
{
    "pin": "1234",
    "name": "watch",
    "format": "basic",
    "serial_number": "123456789123456789",
    "description": "This is the description of my asset",
    "shelf_location": "Aisle 9 Shelf 2"
}
```

The following is an example of an asset defined using the `JSON` format:

{% hint style="info" %}
**NOTE**: In this example the shelf\_location field is defined as mutable and can therefore be updated.
{% endhint %}

```
{
    "pin": "1234",
    "name": "watch",
    "format": "JSON",
    "json" :
        [
            {
                "name": "serial_number",
                "type": "uint64",
                "value": "123456789123456789",
                "mutable" : "false"
            },
            {
                "name": "description",
                "type": "string",
                "value": "This is the description of my asset",
                "mutable" : "false"
            },
            {
                "name": "shelf_location",
                "type": "string",
                "value": "Aisle 9 Shelf 2",
                "mutable" : "true"
            }
        ]
}
```

#### Return value JSON object:

```
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the asset creation.

`address` : The register address for this asset. The address (or name that hashes to this address) is needed for downstream transactions / api methods for this asset.

***

### `get/asset`

This is the generic endpoint for retrieving an asset from the object register. The Assets API supports an alternative endpoint that can include the asset name (if known) in the URI. For example `/assets/get/asset/myasset` will resolve to `assets/get/asset?name=myasset`.

Additionally the API supports passing a field name in the URL after the asset name, which will populate the `fieldname` parameter in the request. For example `/assets/get/asset/myasset/description` will resolve to `assets/get/asset?name=myasset&fieldname=description`

#### Endpoint:

`/assets/get/asset`

{% swagger method="post" path="/assets/get/asset" baseUrl="http://api.nexus-interactions.io:8080" summary="get/asset" %}
{% swagger-description %}
This retrieves an asset information from the object register
{% endswagger-description %}

{% swagger-parameter in="body" name="name" required="false" type="String" %}
The name identifying the asset. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" required="false" type="String" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the asset. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" required="false" type="String" %}
The register address of the asset. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="field" required="false" type="String" %}
This optional field can be used to filter the response to return only a single field from the asset
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="asset information" %}
```json
{
    "name": "watch",
    "address": "8B7SMKmECgYU1ydBQbzp5FCSe4AnkU2EwLE59D7eQDBpixmLZ2c",
    "timestamp": "1553227128",
    "owner": "bf501d4f3d81c31f62038984e923ad01546ff678e305a7cc11b1931742524ce1",
    "serial_number": "123456789123456789",
    "description": "This is the description of my asset",
    "shelf_location": "Aisle 9 Shelf 2"
} 
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// get / asset
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
    pin: "YOUR_PIN",
    // session: "YOUR_SESSION_ID",//optional
    name: "ASSET_NAME", //optional if address is passed
    // address: "ASSET_ADDRESS", //optional if name is passed
    // fieldname: "FILTER_FIELD" //optional
}
fetch(`${SERVER_URL}/assets/get/asset`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "pin": "YOUR_PIN",
    # "session": "YOUR_SESSION_ID",#optional
    "name": "ASSET_NAME",  # optional if address is passed
    # "address": "ASSET_ADDRESS", #optional if name is passed
    # "fieldname": "FILTER_FIELD" #optional
}
response = requests.post(f"{SERVER_URL}/assets/get/asset", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`name` : The name identifying the asset. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the asset. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`address` : The register address of the asset. This is optional if the name is provided.

`fieldname`: This optional field can be used to filter the response to return only a single field from the asset.

#### Return value JSON object:

```
{
    "name": "watch",
    "address": "8B7SMKmECgYU1ydBQbzp5FCSe4AnkU2EwLE59D7eQDBpixmLZ2c",
    "timestamp": "1553227128",
    "owner": "bf501d4f3d81c31f62038984e923ad01546ff678e305a7cc11b1931742524ce1",
    "serial_number": "123456789123456789",
    "description": "This is the description of my asset",
    "shelf_location": "Aisle 9 Shelf 2"
}
```

#### Return values:

`owner` : The genesis hash of the signature chain that owns this asset.

`created` : The UNIX timestamp when the asset was created.

`modified` : The UNIX timestamp when the asset was last modified.

`name` : The name identifying the asset. For privacy purposes, this is only included in the response if the caller is the owner of the asset

`address` : The register address of the asset.

`ownership` : Only included for tokenized assets, this is the percentage of the asset owned by the caller, based on the number of tokens owned

`<fieldname>=<value>` : The key-value pair for each piece of data stored in the asset.

***

### `update/asset`

This is the generic endpoint for updating one or more values in an asset. The API supports an alternative endpoint that can include the asset name (if known) or register address in the URI. For example `/assets/update/asset/myasset` will resolve to `assets/update/asset?name=myasset`.

**NOTE** Only assets created using `JSON`, `ANSI`, or `XML` an be updated, and only those data fields that were defined as mutable. `raw` and `basic` format assets are always created as read-only (immutable).

#### Endpoint:

`/assets/update/asset`

{% swagger method="post" path="/assets/update/asset" baseUrl="http://api.nexus-interactions.io:8080" summary="update/asset" %}
{% swagger-description %}
This will update one or more values in an asset.
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" required="false" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the asset should be created with. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" required="false" %}
The name identifying the asset to update. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" required="false" %}
The register address of the asset to update. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="<fieldname>=<value>" required="true" %}
The caller can provide = pairs for each piece of data to update in the asset.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="asset information updated" %}
```json
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// update / asset
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
    name: "ASSET_NAME", //optional if address is passed
    // session: "YOUR_SESSION_ID",//optional
    // address: "ASSET_ADDRESS", //optional if name is passed
    fieldname = value //<fieldname>=<values> to be updated
}
fetch(`${SERVER_URL}/assets/update/asset`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "name": "ASSET_NAME",  # optional if address is passed
    # "session": "YOUR_SESSION_ID",#optional
    # "address": "ASSET_ADDRESS", #optional if name is passed
    # fieldname: value #<fieldname>=<values> to be updated
}
response = requests.post(f"{SERVER_URL}/assets/update/asset", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the asset should be created with. For single-user API mode the session should not be supplied.

`name` : The name identifying the asset to update. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the asset to update. This is optional if the name is provided.

`<fieldname>=<value>` : The caller can provide = pairs for each piece of data to update in the asset.

#### Example:

The following is an example JSON payload to update two fields in an asset called "mysong"

```
{
    "pin": "1234",
    "name": "mysong",
    "last_downloaded": "2019/02/03 14:22:08",
    "download_count": "428"
}
```

#### Return value JSON object:

```
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the asset update.

`address` : The register address for this asset.

***

### `transfer/asset`

This will transfer ownership of an asset or digital item. This is a generic endpoint requiring the asset name or address to be passed as parameters. The API supports an alternative endpoint that can include the asset name (if known) or register address in the URI. For example `/assets/transfer/asset/myasset` will resolve to `assets/transfer/asset?name=myasset`.

#### Endpoint:

`/assets/transfer/asset`

{% swagger method="post" path="/assets/transfer/asset" baseUrl="http://api.nexus-interactions.io:8080" summary="transfer/asset" %}
{% swagger-description %}
This will transfer ownership of an asset or digital item
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the asset. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the asset to be transferred. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the asset to be transferred. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="username" %}
The username identifying the user account (sig-chain) to transfer the asset to. This is optional if the destination is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="destination" %}
The genesis hash of the signature chain to transfer the the asset to. This is optional if the username is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expires" %}
This optional field allows callers to specify an expiration for the transfer transaction. The expires value is the 

`number of seconds`

 from the transaction creation time after which the transaction can no longer be claimed by the recipient. Conversely, when you apply an expiration to a transaction, you are unable to void the transaction until after the expiration time. If expires is set to 0, the transaction will never expire, making the sender unable to ever void the transaction. If omitted, a default expiration of 7 days (604800 seconds) is applied
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="transferred asset" %}
```json
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// transfer / asset
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
    pin: "YOUR_PIN",
    // session: "YOUR_SESSION_ID",//optional
    name: "ASSET_NAME", //optional if address is passed
    // address: "ASSET_ADDRESS", //optional if name is passed
    username: "TO_USERNAME", //optional if destination is passed
    // destination: "TO_GENESIS_HASH_OF_SIGCHAIN",//optional if username is passed
}
fetch(`${SERVER_URL}/assets/transfer/asset`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "pin": "YOUR_PIN",
    # "session": "YOUR_SESSION_ID",#optional
    "name": "ASSET_NAME",  # optional if address is passed
    # "address": "ASSET_ADDRESS", #optional if name is passed
    "username": "TO_USERNAME",  # optional if destination is passed
    # "destination": "TO_GENESIS_HASH_OF_SIGCHAIN",#optional if username is passed
}
response = requests.post(f"{SERVER_URL}/assets/transfer/asset", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the asset. For single-user API mode the session should not be supplied.

`name` : The name identifying the asset to be transferred. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the asset to be transferred. This is optional if the name is provided.

`username` : The username identifying the user account (sig-chain) to transfer the asset to. This is optional if the destination is provided.

`destination` : The genesis hash of the signature chain to transfer the the asset to. This is optional if the username is provided.

`expires` : This optional field allows callers to specify an expiration for the transfer transaction. The expires value is the `number of seconds` from the transaction creation time after which the transaction can no longer be claimed by the recipient. Conversely, when you apply an expiration to a transaction, you are unable to void the transaction until after the expiration time. If expires is set to 0, the transaction will never expire, making the sender unable to ever void the transaction. If omitted, a default expiration of 7 days (604800 seconds) is applied.

#### Return value JSON object:

```
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the asset transfer.

`address` : The new register address for this asset.

***

## `claim/asset`

Assets that have been transferred need to be claimed by the recipient before the transfer is complete. This method creates the claim transaction . This is a generic endpoint requiring the transaction ID (hash) of the corresponding transfer transaction to be passed as a parameter. The API supports an alternative endpoint that can include the transaction ID in the URI. For example `/assets/claim/asset/27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1` will resolve to `assets/claim/asset?txid=27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1`.

#### Endpoint:

`/assets/claim/asset`

{% swagger method="post" path="/assets/claim/asset" baseUrl="http://api.nexus-interactions.io:8080" summary="claim/asset" %}
{% swagger-description %}
Assets that have been transferred need to be claimed by the recipient before the transfer is complete
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user accounts
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the asset. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="txid" %}
The transaction ID (hash) of the corresponding asset transfer transaction for which you are claiming
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
This optional field allows the user to rename an asset when it is claimed. By default the name is copied from the previous owner and a Name record is created for the asset in your user namespace. If you already have an object for this name then you will need to provide a new name in order for the claim to succeed
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="asset claimed" %}
```javascript
{
    "claimed" : 
    [
        "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
    ],
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// claim / asset
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
    pin: "YOUR_PIN",
    // session: "YOUR_SESSION_ID",//optional
    txid: "TX_HASH",
    name: "ASSET_NAME", //optional if address is passed
}
fetch(`${SERVER_URL}/assets/claim/asset`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "pin": "YOUR_PIN",
    # "session": "YOUR_SESSION_ID",#optional
    "txid": "TX_HASH",
    "name": "ASSET_NAME",  # optional if address is passed
}
response = requests.post(f"{SERVER_URL}/assets/claim/asset", json=data)
print(response.json())

```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the asset. For single-user API mode the session should not be supplied.

`txid` : The transaction ID (hash) of the corresponding asset transfer transaction for which you are claiming.

`name` : This optional field allows the user to rename an asset when it is claimed. By default the name is copied from the previous owner and a Name record is created for the asset in your user namespace. If you already have an object for this name then you will need to provide a new name in order for the claim to succeed.

#### Return value JSON object:

```
{
    "claimed" : 
    [
        "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
    ],
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
}
```

#### Return values:

`claimed` : Array of addresses for each asset that was claimed by this transaction

`txid` : The ID (hash) of the transaction that includes the asset transfer.

***

### `list/asset/history`

This will get the history of an asset or digital item as well as it's ownership.The API supports an alternative endpoint that can include the asset name (if known) or register address in the URI. For example `/assets/list/asset/history/myasset` will resolve to `assets/list/asset/history?name=myasset`.

#### Endpoint:

`/assets/list/asset/history`

{% swagger method="post" path="/assets/list/asset/history" baseUrl="http://api.nexus-interactions.io:8080" summary="list/asset/history" %}
{% swagger-description %}
This will get the history of an asset or digital item as well as it's ownership
{% endswagger-description %}

{% swagger-parameter in="body" name="name" %}
The name identifying the asset. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the asset. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the asset. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="asset history" %}
```json
[
    {
        "type": "TRANSFER",
        "owner": "2be51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
        "modified": 1560492117,
        "checksum": 13703027408063695802,
        "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
        "name": "test",
        "data": "1234"
    },
    {
        "type": "CREATE",
        "owner": "1ff463e036cbde3595fbe2de9dff15721a89e99ef3e2e9bfa7ce48ed825e9ec2",
        "modified": 1560492117,
        "checksum": 13703027408063695802,
        "address": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse",
        "name": "test",
        "data: "1234"
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// list / asset / history
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
    name: "ASSET_NAME", //optional if address is passed
    // session: "YOUR_SESSION_ID",//optional
    // address: "ASSET_ADDRESS", //optional if name is passed
}
fetch(`${SERVER_URL}/assets/list/asset/history`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "name": "ASSET_NAME",  # optional if address is passed
    # "session": "YOUR_SESSION_ID",#optional
    # "address": "ASSET_ADDRESS", #optional if name is passed
}
response = requests.post(f"{SERVER_URL}/assets/list/asset/history", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`name` : The name identifying the asset. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the asset. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`address` : The register address of the asset. This is optional if the name is provided.

#### Return value JSON object:

```
[
    {
        "type": "TRANSFER",
        "owner": "2be51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
        "modified": 1560492117,
        "checksum": 13703027408063695802,
        "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
        "name": "test",
        "data": "1234"
    },
    {
        "type": "CREATE",
        "owner": "1ff463e036cbde3595fbe2de9dff15721a89e99ef3e2e9bfa7ce48ed825e9ec2",
        "modified": 1560492117,
        "checksum": 13703027408063695802,
        "address": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse",
        "name": "test",
        "data: "1234"
    }
]
```

#### Return values:

The return value is a JSON array of objects for each entry in the assets history:

`type` : The action that occurred - CREATE | MODIFY | TRANSFER | CLAIM

`owner` : The genesis hash of the signature chain that owned the asset.

`modified` : The Unix timestamp of when the asset was updated.

`checksum` : A checksum of the state register used for pruning.

`address` : The register address of the asset

`name` : The name of the asset

`<fieldname>=<value>` : The key-value pair for each piece of data stored in the asset at that time.

***

### `tokenize/asset`

This will tokenize an asset into fungible tokens that represent ownership. This is a generic endpoint requiring the asset name or address to be passed as parameters. The API supports an alternative endpoint that can include the asset name (if known) or register address in the URI. For example `/assets/tokenize/asset/myasset` will resolve to `assets/tokenize/asset?name=myasset`.

#### Endpoint:

`/assets/tokenize/asset`

{% swagger method="post" path="/assets/tokenize/asset" baseUrl="http://api.nexus-interactions.io:8080" summary="tokenize/asset" %}
{% swagger-description %}
This will tokenize an asset into fungible tokens that represent ownership
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode (configured with multiuser=1) the session is required to identify which session (sig chain) owns the asset. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the asset to be tokenized. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the asset to be tokenized. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token_name" %}
The name of a token to use to tokenize the asset. The name should be in username:token name format. 

`token`

 can be supplied as an alternative to 

`token_name`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" %}
The register address of a token to use to tokenize the asset. 

`token_name`

 can be supplied as an alternative to 

`token`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="asset tokenised" %}
```json
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// tokenize / asset
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
    pin: "YOUR_PIN",
    // session: "YOUR_SESSION_ID",//optional
    name: "ASSET_NAME", //optional if address is passed
    // address: "ASSET_ADDRESS", //optional if name is passed
    token_name: "username:token",
    // token: "address of the token",//optional
}
fetch(`${SERVER_URL}/assets/tokenize/asset/`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "pin": "YOUR_PIN",
    # "session": "YOUR_SESSION_ID",#optional
    "name": "ASSET_NAME",  # optional if address is passed
    # "address": "ASSET_ADDRESS", #optional if name is passed
    "token_name": "username:token",
    # "token": "address of the token",#optional
}
response = requests.post(f"{SERVER_URL}/assets/tokenize/asset/", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode (configured with multiuser=1) the session is required to identify which session (sig chain) owns the asset. For single-user API mode the session should not be supplied.

`name` : The name identifying the asset to be tokenized. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the asset to be tokenized. This is optional if the name is provided.

`token_name` : The name of a token to use to tokenize the asset. The name should be in username:token name format. `token` can be supplied as an alternative to `token_name`.

{% hint style="info" %}
Create the token beforehand and use the token\_name or token address to tokenize the asset
{% endhint %}

`token` : The register address of a token to use to tokenize the asset. `token_name` can be supplied as an alternative to `token`.

#### Return value JSON object:

```
{
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
    "address": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the asset tokenization.

`address` : The register address for this asset.

***

### `get/schema`

This method returns the information about the user-defined fields that make up the asset. The Assets API supports an alternative endpoint that can include the asset name (if known) or address in the URI. For example `/assets/get/schema/myasset` will resolve to `assets/get/schema?name=myasset`.

#### Endpoint:

`/assets/get/schema`

{% swagger method="post" path="/assets/get/schema" baseUrl="http://api.nexus-interactions.io:8080" summary="get/schema" %}
{% swagger-description %}
This method returns the information about the user-defined fields that make up the asset
{% endswagger-description %}

{% swagger-parameter in="body" name="name" %}
The name identifying the asset. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the asset. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the asset. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fieldname" %}
This optional field can be used to filter the response to return only a single field from the asset
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="schema details" %}
```json
[
    {
        "name": "description",
        "type": "string",
        "value": "this is the description",
        "mutable": true,
        "maxlength": 200
    },

    {
        "name": "count",
        "type": "uint64",
        "value": 1000,
        "mutable": true
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// get / schema
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
    name: "ASSET_NAME", //optional if address is passed
    // session: "YOUR_SESSION_ID",//optional
    // address: "ASSET_ADDRESS", //optional if name is passed
    fieldname: "FILTER_FIELD",
}
fetch(`${SERVER_URL}/assets/get/schema`, {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    })
    .then(resp => resp.json())
    .then(json => console.log(json))
    .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    "name": "ASSET_NAME",  # optional if address is passed
    # "session": "YOUR_SESSION_ID",#optional
    # "address": "ASSET_ADDRESS", #optional if name is passed
    "fieldname": "FILTER_FIELD",
}
response = requests.post(f"{SERVER_URL}/assets/get/schema", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`name` : The name identifying the asset. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the asset was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the asset. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`address` : The register address of the asset. This is optional if the name is provided.

`fieldname`: This optional field can be used to filter the response to return only a single field from the asset.

#### Return value JSON object:

```
[
    {
        "name": "description",
        "type": "string",
        "value": "this is the description",
        "mutable": true,
        "maxlength": 200
    },

    {
        "name": "count",
        "type": "uint64",
        "value": 1000,
        "mutable": true
    }
]
```

#### Return values:

`name` : The name of the data field.

`type` : The data type to use for this field. Values can be `uint8`, `uint16`, `uint32`, `uint64`, `uint256`, `uint512`, `uint1024`, `string`, or `bytes`.

`value` : The default value of the field.

`mutable` : The boolean field to indicate whether the field is writable (true) or read-only (false).

`maxlength`: Only applicable to `string` or `bytes` fields where `mutable`=true, this is the maximum number of characters (bytes) that can be stored in the field.

***
