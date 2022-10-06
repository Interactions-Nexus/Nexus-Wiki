---
title: tokens
description: TOKENS API
published: true
date: 2022-10-05T08:34:49.674Z
tags: 
editor: markdown
dateCreated: 2022-10-05T08:30:11.019Z
---

# TOKENS

The Tokens API provides methods for creating fungible tokens, creating accounts to store them in, and sending and receiving tokens between users.

### `Named Shortcuts`

For each API method we support an alternative endpoint that includes the token/account name or register address at the end of the URI. This shortcut removes the need to include the name name or address as an additional parameter.

For example `tokens/create/account/savings` is a shortcut to `tokens/create/account?name=savings`.

Similarly `tokens/get/token/5efc8a9437d93e894defd50f8ba73a0b2b5529cc593d5e4a7ea413022a9c35e9` is a shortcut to `tokens/get/token?address=5efc8a9437d93e894defd50f8ba73a0b2b5529cc593d5e4a7ea413022a9c35e9`

The logic for resolving the shortcut to either a name or address is that if the data is 64 characters of hexadecimal then it will be assumed to be a register address. Otherwise it will be considered a name.

### `Methods`

The following methods are currently supported by this API

[`create/token`](tokens.md#create-token)\
[`debit/token`](tokens.md#debit-token)\
[`credit/token`](tokens.md#credit-token)\
[`get/token`](tokens.md#get-token)\
[`burn/token`](tokens.md#burn-token)\
[`list/token/transactions`](tokens.md#list-token-transactions)\
[`list/token/accounts`](tokens.md#list-token-accounts)\
[`create/account`](tokens.md#create-account)\
[`debit/account`](tokens.md#debit-account)\
[`credit/account`](tokens.md#credit-account)\
[`get/account`](tokens.md#get-account)\
[`list/account/transactions`](tokens.md#list-account-transactions)

### `create/token`

Create a new token object register. The API supports an alternative endpoint that can include the new token name in the URI. For example `/tokens/create/token/mytoken` will resolve to `tokens/create/token?name=mytoken`.

#### Endpoint:

`/tokens/create/token`

{% swagger method="post" path="/tokens/create/token" baseUrl="http://api.nexus-interactions.io:8080" summary="create/token" %}
{% swagger-description %}
Create a new token object register
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" required="false" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token should be created with. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" required="true" %}
An optional name to identify the token. If provided a Name object will also be created in the users local namespace, allowing the token to be accessed/retrieved by name. If no name is provided the token will need to be accessed/retrieved by its 256-bit register address
{% endswagger-parameter %}

{% swagger-parameter in="body" name="supply" required="true" %}
The initial token supply amount. Must be a whole number amount
{% endswagger-parameter %}

{% swagger-parameter in="body" name="decimals" required="true" %}
The maximum number of decimal places that can be applied to token amounts. For example decimals=2 will allow a token amount to be given to 2 decimal places
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="created token" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// create/token
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  pin: "YOUR_PIN",
  //  session: "YOUR_SESSION_ID", //optional
  // name: "TOKEN_NAME", //optional
  supply: 1000000,
  decimals: 2,
}
fetch(`${SERVER_URL}/tokens/create/token`, {
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
    #  "session": "YOUR_SESSION_ID", #optional
    # "name": "TOKEN_NAME", #optional
    "supply": 1000000,
    "decimals": 2,
}
response = requests.post(f"{SERVER_URL}/tokens/create/token", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token should be created with. For single-user API mode the session should not be supplied.

`name` : An optional name to identify the token. If provided a Name object will also be created in the users local namespace, allowing the token to be accessed/retrieved by name. If no name is provided the token will need to be accessed/retrieved by its 256-bit register address.

`supply` : The initial token supply amount. Must be a whole number amount.

`decimals` : The maximum number of decimal places that can be applied to token amounts. For example decimals=2 will allow a token amount to be given to 2 decimal places.

#### Example:

```
{
    "pin": "1234",
    "name": "ABC",
    "supply": 1000000,
    "decimals": 4
}
```

#### Return value JSON object:

```
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d",
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the token creation.

`address` : The register address for this token. The address (or name that hashes to this address) is needed when creating token accounts, so that we know which token the account can be used with.

***

### `debit/token`

Deduct a token amount from a token's initial supply and send it to a token account. The API supports an alternative endpoint that can include the token name in the URI. For example `/tokens/debit/token/mytoken` will resolve to `tokens/debit/token?name=mytoken`.\
Any fee that is applicable fo this transaction is deducted from the `default` account.

The method supports the ability to send to multiple recipients in one transaction by supplying a `recipients` array instead of the single `name_to`/`address_to`/`amount`. The method allows up to 99 recipients to be supplied.

#### Endpoint:

`/tokens/debit/token`

{% swagger method="post" path="/tokens/debit/token" baseUrl="http://api.nexus-interactions.io:8080" summary="debit/token" %}
{% swagger-description %}
Deduct a token amount from a token's initial supply and send it to a token account
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token owner. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token to debit. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" %}
The amount of tokens to debit
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name_to" %}
The name identifying the token account to send to. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address_to" %}
The register address of the token account to send to. This is optional if the name is provided.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference" %}
This optional field allows callers to provide a reference, which the recipient can then use to relate the transaction to an order number, invoice number etc. The reference is be a 64-bit unsigned integer in the range of 0 to 18446744073709551615
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expires" %}
This optional field allows callers to specify an expiration for the debit transaction. The expires value is the 

`number of seconds`

 from the transaction creation time after which the transaction can no longer be credited by the recipient. Conversely, when you apply an expiration to a transaction, you are unable to void the transaction until after the expiration time. If expires is set to 0, the transaction will never expire, making the sender unable to ever void the transaction. If omitted, a default expiration of 7 days (604800 seconds) is applied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recipients" %}
This optional array can be provided as an alternative to the single 

`name_to`

/

`address_to`

, 

`amount`

, 

`reference`

, and 

`expires`

 fields. Each object in the array can have 

`name_to`

/

`address_to`

, 

`amount`

, 

`refer`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="token debited" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// debit/token
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  pin: "YOUR_PIN",
  //  session: "YOUR_SESSION_ID" //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  amount: 10,
  name_to: "TO_TOKEN_NAME", //optional if address_to is passed
  // address_to: "TO_TOKEN_ADDRESS", //optional if name_to is passed
  // reference: "64-bit unsigned integer", optional
  // expires: 604800, //optional (in seconds)
  // recipients: [
  //   { name: "NAME", amount: 10, name_to: "NAME_TO" },
  //   { name: "NAME", amount: 10, name_to: "NAME_TO" }
  // ] //optional
}
fetch(`${SERVER_URL}/tokens/debit/token`, {
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
    #  "session": "YOUR_SESSION_ID" #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    "amount": 10,
    "name_to": "TO_TOKEN_NAME",  # optional if address_to is passed
    # "address_to": "TO_TOKEN_ADDRESS", #optional if name_to is passed
    # "reference": "64-bit unsigned integer", optional
    # "expires": 604800, #optional (in seconds)
    # "recipients": [
    #   { "name": "NAME", amount: 10, name_to: "NAME_TO"
}
response = requests.post(f"{SERVER_URL}/tokens/debit/token", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token owner. For single-user API mode the session should not be supplied.

`name` : The name identifying the token to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the token to debit. This is optional if the name is provided.

`amount` : The amount of tokens to debit.

`name_to` : The name identifying the token account to send to. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address_to` : The register address of the token account to send to. This is optional if the name is provided.

`reference` : This optional field allows callers to provide a reference, which the recipient can then use to relate the transaction to an order number, invoice number etc. The reference is be a 64-bit unsigned integer in the range of 0 to 18446744073709551615

`expires` : This optional field allows callers to specify an expiration for the debit transaction. The expires value is the `number of seconds` from the transaction creation time after which the transaction can no longer be credited by the recipient. Conversely, when you apply an expiration to a transaction, you are unable to void the transaction until after the expiration time. If expires is set to 0, the transaction will never expire, making the sender unable to ever void the transaction. If omitted, a default expiration of 7 days (604800 seconds) is applied.

`recipients` : This optional array can be provided as an alternative to the single `name_to`/`address_to`, `amount`, `reference`, and `expires` fields. Each object in the array can have `name_to`/`address_to`, `amount`, `reference`, and `expires` fields, as described above. Up to 99 recipients can be included in the array.

#### Example:

The following example shows the json payload for a debit of 10.5 ABC tokens (that itself was created by the sig chain logged into session "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8") being sent to a token account identified by the name "jack:savings". In the name\_to field, "jack" refers to the username of the account holder and "savings" is their token account. If jack is concerned about privacy he could have provided the register address of his token account instead

```
{
    "pin": "1234",
    "session": "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8",
    "name": "bob:ABC",
    "amount": 10.5,
    "name_to": "jack:savings"
}
```

#### Example Multiple Recipients:

The following example shows the json payload for a debit from a token called "ABC" made to 3 separate recipients, each receiving 5 ABC tokens, and each with a different reference

```
{
    "pin": "1234",
    "name": "ABC"
    "recipients" :
    [
        {
            "name_to": "bob:abc",
            "amount": 5,
            "reference": 1234
        },
        {
            "address_to": "8CHjS5Qe7Mghgrqb6NeEaVxjexbdp9p2QVdRTt8W4rzbWhu3fL8",
            "amount": 5,
            "reference": 5678
        },
        {
            "address_to": "8CM4SYrd6ohcBB8tfqyZG3MCtDStMUXN37gwC2RtkNSUayM2FSN",
            "amount": 5
        }
    ]
}
```

#### Return value JSON object:

```
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the token debit.

***

### `credit/token`

Increment the token balance by an amount received from a token account. This method allows fungible tokens to be recycled back to the token creator in circumstances where they have reached the end of their life-cycle, for example a loyalty token that has been used by the customer to pay for a product can be debited from the customer's account and back to the token for reuse. The API supports an alternative endpoint that can include the token name to credit in the URL. For example `/tokens/credit/token/mytoken` will resolve to `tokens/credit/token?name=mytoken`.

#### Endpoint:

`/tokens/credit/token`

{% swagger method="post" path="/tokens/credit/token" baseUrl="http://api.nexus-interactions.io:8080" summary="credit/token" %}
{% swagger-description %}
Increment the token balance by an amount received from a token account
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the token account. For single-user API mode the session should not be supplie
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token to credit. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="txid" required="true" %}
The transaction ID (hash) of the corresponding debit transaction for which you are creating this credit for
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="credited tokens" %}
```json
{
    "txid": "318b86d2c208618aaa13946a3b75f14472ebc0cce9e659f2830b17e854984b55606738f689d886800f21ffee68a3e5fd5a29818e88f8c5b13b9f8ae67739903d"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// credit/token
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  pin: "YOUR_PIN",
  //  session: "YOUR_SESSION_ID", //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  txid: "of the debit transaction",
}
fetch(`${SERVER_URL}/tokens/credit/token`, {
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
    #  "session": "YOUR_SESSION_ID", #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    "txid": "of the debit transaction",
}
response = requests.post(f"{SERVER_URL}/tokens/credit/token", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the token account. For single-user API mode the session should not be supplied.

`name` : The name identifying the token to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the token to credit. This is optional if the name is provided.

`txid` : The transaction ID (hash) of the corresponding debit transaction for which you are creating this credit for.

#### Example:

The following example shows the json payload for a credit to a token called "mytoken" (that itself was created by the sig chain logged into session "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8").

```
{
    "pin": "1234",
    "session": "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8",
    "name": "mytoken",
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```

#### Return value JSON object:

```
{
    "txid": "318b86d2c208618aaa13946a3b75f14472ebc0cce9e659f2830b17e854984b55606738f689d886800f21ffee68a3e5fd5a29818e88f8c5b13b9f8ae67739903d"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the token credit.

***

### `get/token`

Retrieves information about a token and its supply. The API supports an alternative endpoint that can include the token name in the URI. For example `/tokens/get/token/mytoken` will resolve to `tokens/get/token?name=mytoken`.

Additionally the API supports passing a field name in the URL after the token name, which will populate the `fieldname` parameter in the request. For example `/tokens/get/token/mytoken/supply` will resolve to `tokens/get/token?name=mytoken&fieldname=supply`

#### Endpoint:

`/tokens/get/token`

{% swagger method="post" path="/tokens/get/token" baseUrl="http://api.nexus-interactions.io:8080" summary="get/token" %}
{% swagger-description %}
Retrieves information about a token and its supply
{% endswagger-description %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the token. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token to retrieve. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="count" %}
Optional boolean field that determines whether the response includes the transaction 

`count`

 field. This defaults to false, as including the transaction count can slow the response time of the method considerably
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fieldname" %}
This optional field can be used to filter the response to return only a single field from the toke
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="token details" %}
```json
{
    "owner": "a2e51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
    "created": 1566534164,
    "modified": 1566616211,
    "name": "mytoken",
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
    "balance": 990,
    "pending": 0,
    "unconfirmed": 0,
    "maxsupply": 1000,
    "currentsupply": 10,
    "decimals": 0
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// get/token
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  name: "TOKEN_NAME", //optional if address is passed
  //  session: "YOUR_SESSION_ID", //optional
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  // count: false, //optional
  // fieldname: "FILTER_NAME", //optional
}
fetch(`${SERVER_URL}/tokens/get/token`, {
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
    "name": "TOKEN_NAME",  # optional if address is passed
    #  "session": "YOUR_SESSION_ID", #optional
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    # "count": False, #optional
    # "fieldname": "FILTER_NAME", #optional
}
response = requests.post(f"{SERVER_URL}/tokens/get/token", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`name` : The name identifying the token to retrieve information. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the token. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`address` : The register address of the token to retrieve. This is optional if the name is provided.

`count` : Optional boolean field that determines whether the response includes the transaction `count` field. This defaults to false, as including the transaction count can slow the response time of the method considerably.

`fieldname`: This optional field can be used to filter the response to return only a single field from the token.

#### Return value JSON object:

```
{
    "owner": "a2e51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
    "created": 1566534164,
    "modified": 1566616211,
    "name": "mytoken",
    "address": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
    "balance": 990,
    "pending": 0,
    "unconfirmed": 0,
    "maxsupply": 1000,
    "currentsupply": 10,
    "decimals": 0
}
```

#### Return values:

`owner` : The genesis hash of the signature chain that owns this token.

`created` : The UNIX timestamp when the token was created.

`modified` : The UNIX timestamp when the token was last modified.

`name` : The name identifying the token. For privacy purposes, this is only included in the response if the caller is the owner of the token

`address` : The register address of the token.

`balance` : The available balance of this token. Initially the balance of the token is equal to the max supply, until the tokens have been distributed to accounts. This is the last confirmed balance less any new debits that you have made since the last block.

`pending` : This is the sum of all confirmed debit transactions that have been made to this token, that have not yet been credited. To move tokens from pending into the available balance you must create a corresponding credit transaction. NOTE: if configured to run, the events processor does this for you.

`unconfirmed` : This is the sum of all unconfirmed debit transactions that have been made to this token PLUS the sum of all unconfirmed credits that you have for confirmed debit transactions. When someone makes a debit to the token it will immediately appear in the unconfirmed balance until that transaction is included in a block, at which point it moves into `pending`. When you (or the events processor) creates the corresponding credit transaction for that debit, the amount will move from `pending` back into `unconfirmed` until the credit transaction is included in a block, at which point the amount moves to `balance`.

`maxsupply` : The maximum token supply amount.

`currentsupply` : The current amount of tokens that have been distributed to token accounts.

`decimals` : The maximum number of decimal places that can be applied to token amounts. For example decimals=2 will allow a token amount to be given to 2 decimal places.

`count` : Only returned if the caller requested `count` : true. This is the number of transactions made to/from the token.

***

### `burn/token`

This method can be used to take tokens permanently out of the current supply, a process commonly known as burning. The method will debit a token account and send the tokens back to the token address. However the transaction contains a condition that will always evaluate to false, guaranteeing that the debit can not be credited by the token issuer nor the sender. The result is that the amount burned will always appear in the "pending" balance of the token.

#### Endpoint:

`/tokens/burn/token`

{% swagger method="post" path="/tokens/burn/tokens" baseUrl="http://api.nexus-interactions.io:8080" summary="burn/token" %}
{% swagger-description %}
This method can be used to take tokens permanently out of the current supply, a process commonly known as burning
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token owner. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the account to debit the tokens from to be burnt. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the account to debit the tokens from the be burnt. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" %}
The amount of tokens to burn
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference" %}
This optional field allows callers to provide a reference, which the recipient can then use to relate the transaction to an order number, invoice number etc. The reference is be a 64-bit unsigned integer in the range of 0 to 18446744073709551615
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="tokens burnt" %}
```json
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// burn/token
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  name: "TOKEN_NAME", //optional if address is passed
  // session: "YOUR_SESSION_ID", //optional
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  amount: 10,
  // reference: "64-bit unsigned integer", optional
}
fetch(`${SERVER_URL}/tokens/burn/token`, {
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
    "name": "TOKEN_NAME",  # optional if address is passed
    # "session": "YOUR_SESSION_ID", #optional
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    "amount": 10,
    # "reference": "64-bit unsigned integer", optional
}
response = requests.post(f"{SERVER_URL}/tokens/burn/token", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token owner. For single-user API mode the session should not be supplied.

`name` : The name identifying the account to debit the tokens from to be burnt. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the token was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the account to debit the tokens from the be burnt. This is optional if the name is provided.

`amount` : The amount of tokens to burn.

`reference` : This optional field allows callers to provide a reference, which the recipient can then use to relate the transaction to an order number, invoice number etc. The reference is be a 64-bit unsigned integer in the range of 0 to 18446744073709551615

#### Example:

The following example shows the json payload for a burn of 100 tokens from an account called "main" (that itself was created by the sig chain logged into session "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8")

```
{
    "pin": "1234",
    "session": "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8",
    "name": "main",
    "amount": 100
}
```

#### Return value JSON object:

```
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the token burn.

***

### `list/token/transactions`

This will list off all of the transactions related to a given token. You DO NOT need to be logged in to use this command. If you are logged in, then neither username or genesis are required as it will default to the logged in user.

{% hint style="info" %}
**NOTE** : The returned transaction data will only include contracts that related to the requested token. Any other contracts are omitted from the transaction result.

**NOTE** : If you use the username parameter it will take slightly longer to calculate the username genesis with our brute-force protected hashing algorithm. For higher performance, use the genesis parameter.
{% endhint %}

#### Endpoint:

`/tokens/list/token/transactions`

{% swagger method="post" path="/tokens/list/token/transactions" baseUrl="http://api.nexus-interactions.io:8080" summary="list/token/transactions" %}
{% swagger-description %}
This will list off all of the transactions related to a given token. You DO NOT need to be logged in to use this command. If you are logged in, then neither username or genesis are required as it will default to the logged in user.
{% endswagger-description %}

{% swagger-parameter in="body" name="genesis" %}
The genesis hash identifying the signature chain to scan for transactions (optional if username is supplied or already logged in)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="username" %}
The username identifying the signature chain to scan for transactions(optional if genesis is supplied or already logged in)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the token name in order to deduce the register address of the token. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token to list transactions for. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the object was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token to list transactions for. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verbose" %}


Optional, determines how much transaction data to include in the response. Supported values are : \


`default` : hash, contracts

``

`summary` : type, version, sequence, timestamp, operation, and confirmations.

``

`detail` : genesis, nexthash, prevhash, pubkey and signature.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" %}
The number of records to return for the current page. The default is 100
{% endswagger-parameter %}

{% swagger-parameter in="body" name="page" %}
Allows the results to be returned by page (zero based). E.g. passing in page=1 will return the second set of (limit) records. The default value is 0 if not supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offset" %}
An alternative to 

`page`

, offset can be used to return a set of (limit) results from a particular index
{% endswagger-parameter %}

{% swagger-parameter in="body" name="where" %}
An array of clauses to filter the JSON results. More information on filtering the results from /list/xxx API methods can be found here Filtering Results
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="token transactions list" %}
```json
[
    {
        "txid": "01034b39cb3635d370f97339e6f87b8751d4c0d62676da7d6ec20416966f298f47dea99603d03a74e638b0d50b31b1e721790e5b103abfe3353a709ccf5d1e7c",
        "contracts": [
            {
                "OP": "CREDIT",
                "txid": "01e73b498dbabbf4629ad674b9ae3824b96cca83199c25a67901db53b271d19acf1411b0c4f9a3d8ded80860ffe2dcf683d2d227a675d453303b31f86f868f9e",
                "contract": 0,
                "proof": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse",
                "to": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
                "to_name": "main",
                "amount": 76.450762,
                "token": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse",
                "token_name": "XXX"
            },
            {
                "OP": "FEE",
                "from": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
                "from_name": "default",
                "amount": 0.1
            }
        ]
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// list/token/transactions
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  // genesis: "GENESIS_HASH", //optional 
  username: "YOUR_USERNAME",//optional
  // session: "YOUR_SESSION_ID", //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  // verbose: "detail", //optional or "summary","none"
  // limit: 50, //optional
  // page: 1, //optional
  // offset: 10, //optional
  // where: "FILTERING SQL QUERY" //optional
}
fetch(`${SERVER_URL}/tokens/list/token/transactions`, {
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
    # "genesis": "GENESIS_HASH", #optional
    "username": "YOUR_USERNAME",  # optional
    # "session": "YOUR_SESSION_ID", #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    # "verbose": "detail", #optional or "summary","none"
    # "limit": 50, #optional
    # "page": 1, #optional
    # "offset": 10, #optional
    # "where": "FILTERING SQL QUERY" #optional
}
response = requests.post(
    f"{SERVER_URL}/tokens/list/token/transactions", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`genesis` : The genesis hash identifying the signature chain to scan for transactions (optional if username is supplied or already logged in).

`username` : The username identifying the signature chain to scan for transactions(optional if genesis is supplied or already logged in).

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the token name in order to deduce the register address of the token. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`name` : The name identifying the token to list transactions for. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the object was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the token to list transactions for. This is optional if the name is provided.

`verbose` : Optional, determines how much transaction data to include in the response. Supported values are :

* `default` : hash, contracts
* `summary` : type, version, sequence, timestamp, operation, and confirmations.
* `detail` : genesis, nexthash, prevhash, pubkey and signature.

`limit` : The number of records to return for the current page. The default is 100.

`page` : Allows the results to be returned by page (zero based). E.g. passing in page=1 will return the second set of (limit) records. The default value is 0 if not supplied.

`offset` : An alternative to `page`, offset can be used to return a set of (limit) results from a particular index.

`where` : An array of clauses to filter the JSON results. More information on filtering the results from /list/xxx API methods can be found here Filtering Results

#### Return value JSON object:

```
[
    {
        "txid": "01034b39cb3635d370f97339e6f87b8751d4c0d62676da7d6ec20416966f298f47dea99603d03a74e638b0d50b31b1e721790e5b103abfe3353a709ccf5d1e7c",
        "contracts": [
            {
                "OP": "CREDIT",
                "txid": "01e73b498dbabbf4629ad674b9ae3824b96cca83199c25a67901db53b271d19acf1411b0c4f9a3d8ded80860ffe2dcf683d2d227a675d453303b31f86f868f9e",
                "contract": 0,
                "proof": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse",
                "to": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
                "to_name": "main",
                "amount": 76.450762,
                "token": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse",
                "token_name": "XXX"
            },
            {
                "OP": "FEE",
                "from": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P",
                "from_name": "default",
                "amount": 0.1
            }
        ]
    }
]
```

#### Return values:

`txid` : The transaction hash.

`type` : The description of the transaction (`legacy` | `tritium base` | `trust` | `genesis` | `user`).

`version` : The serialization version of the transaction.

`sequence` : The sequence number of this transaction within the signature chain.

`timestamp` : The Unix timestamp of when the transaction was created.

`blockhash` : The hash of the block that this transaction is included in. Blank if not yet included in a block.

`confirmations` : The number of confirmations that this transaction obtained by the network.

`genesis` : The signature chain genesis hash.

`nexthash` : The hash of the next transaction in the sequence.

`prevhash` : the hash of the previous transaction in the sequence.

`pubkey` : The public key.

`signature` : The signature hash.

`contracts` : The array of contracts bound to this transaction and their details with opcodes.\
{\
`id` : The sequential ID of this contract within the transaction.

`OP` : The contract operation. Can be `APPEND`, `CLAIM`, `COINBASE`, `CREATE`, `CREDIT`, `DEBIT`, `FEE`, `GENESIS`, `LEGACY`, `TRANSFER`, `TRUST`, `STAKE`, `UNSTAKE`, `WRITE`.

`for` : For `CREDIT` transactions, the contract that this credit was created for . Always `DEBIT` for token transactions.

`txid` : The transaction that was credited / claimed.

`contract` : The ID of the contract within the transaction that was credited / claimed.

`proof` : The register address proving the credit.

`from` : For `DEBIT`, `CREDIT`, `FEE` transactions, the register address of the account that the debit is being made from.

`from_name` : For `DEBIT`, `CREDIT`, `FEE` transactions, the name of the account that the debit is being made from. Only included if the name can be resolved.

`to` : For `DEBIT` and `CREDIT` transactions, the register address of the recipient account.

`to_name` : For `DEBIT` and `CREDIT` transactions, the name of the recipient account. Only included if the name can be resolved.

`amount` : the token amount of the transaction.

`token` : the register address of the token that the transaction relates to. Set to 0 for NXS transactions

`token_name` : The name of the token that the transaction relates to.

`reference` : For `DEBIT` and `CREDIT` transactions this is the user supplied reference used by the recipient to relate the transaction to an order or invoice number.

}

### `list/token/accounts`

This will list all accounts (globally) that have been created for a particular token.

#### Endpoint:

`/tokens/list/token/accounts`

{% swagger method="post" path="/tokens/list/token/accounts" baseUrl="http://api.nexus-interactions.io:8080" summary="list/token/accounts" %}
{% swagger-description %}
This will list all accounts (globally) that have been created for a particular token.
{% endswagger-description %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the token name in order to deduce the register address of the token. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token to list accounts for. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the object was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token to list transactions for. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" %}
The number of records to return for the current page. The default is 100
{% endswagger-parameter %}

{% swagger-parameter in="body" name="page" %}
Allows the results to be returned by page (zero based). E.g. passing in page=1 will return the second set of (limit) records. The default value is 0 if not supplied.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offset" %}
An alternative to 

`page`

, offset can be used to return a set of (limit) results from a particular index
{% endswagger-parameter %}

{% swagger-parameter in="body" name="where" %}
An array of clauses to filter the JSON results. More information on filtering the results from /list/xxx API methods can be found here Filtering Results
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="token account list" %}
```json
[
    {
        "owner": "a1f94d55f41aba2f75b020d0582c8b607b72f4f2742e4cde6135558adc44583d",
        "created": 1576709402,
        "modified": 1576718254,
        "address": "8CsmdG4rP5J2RRY5M9ibTxKEpnZiJoGu5RzmGyxxy726sv6Nc76",
        "balance": 32930.0
    },
    {
        "owner": "a1fc3f7264e53dba1e1043e29e4087f57f5a30a2008fdc8483be7e6cd3d7ff97",
        "created": 1576655433,
        "modified": 1576673358,
        "address": "8BjpdTPJthrBDQan2mABjbYhs2FPKAih6Vq5oxELiXqXGVq1Mqt",
        "balance": 6586.0
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// list/token/accounts
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
  // session: "YOUR_SESSION_ID", //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  // verbose: "detail", //optional or "summary","none"
  // limit: 50, //optional
  // page: 1, //optional
  // offset: 10, //optional
  // where: "FILTERING SQL QUERY" //optional
}
fetch(`${SERVER_URL}/tokens/list/token/accounts`, {
  method: 'POST',
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify(data)
})
  .then(resp => resp.json())
  .then(json => console.log(json))
  .catch(error => console.log(error))
```
{% endtab %}

{% tab title="Pyhton" %}
```python
import requests
SERVER_URL = "http://api.nexus-interactions.io:8080"
data = {
    # "session": "YOUR_SESSION_ID", #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    # "verbose": "detail", #optional or "summary","none"
    # "limit": 50, #optional
    # "page": 1, #optional
    # "offset": 10, #optional
    # "where": "FILTERING SQL QUERY" #optional
}
response = requests.post(f"{SERVER_URL}/tokens/list/token/accounts", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the token name in order to deduce the register address of the token. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`name` : The name identifying the token to list accounts for. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the object was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the token to list transactions for. This is optional if the name is provided.

`limit` : The number of records to return for the current page. The default is 100.

`page` : Allows the results to be returned by page (zero based). E.g. passing in page=1 will return the second set of (limit) records. The default value is 0 if not supplied.

`offset` : An alternative to `page`, offset can be used to return a set of (limit) results from a particular index.

`where` : An array of clauses to filter the JSON results. More information on filtering the results from /list/xxx API methods can be found here Filtering Results

#### Return value JSON object:

```
[
    {
        "owner": "a1f94d55f41aba2f75b020d0582c8b607b72f4f2742e4cde6135558adc44583d",
        "created": 1576709402,
        "modified": 1576718254,
        "address": "8CsmdG4rP5J2RRY5M9ibTxKEpnZiJoGu5RzmGyxxy726sv6Nc76",
        "balance": 32930.0
    },
    {
        "owner": "a1fc3f7264e53dba1e1043e29e4087f57f5a30a2008fdc8483be7e6cd3d7ff97",
        "created": 1576655433,
        "modified": 1576673358,
        "address": "8BjpdTPJthrBDQan2mABjbYhs2FPKAih6Vq5oxELiXqXGVq1Mqt",
        "balance": 6586.0
    }
]
```

#### Return values:

`owner` : The genesis hash of the signature chain that owns this account.

`created` : The UNIX timestamp when the account was created.

`modified` : The UNIX timestamp when the account was last modified.

`address` : The register address of the account.

`balance` : The available balance of this account. This is the last confirmed balance for the account, and does not reflect and any new debits that have been made since the last block.

***

### `create/account`

Create a new token account for receiving tokens. The API supports an alternative endpoint that can include the account name in the URI. For example `/tokens/create/account/savings` will resolve to `tokens/create/account?name=savings`.

#### Endpoint:

`/tokens/create/account`

{% swagger method="post" path="" baseUrl="" summary="create/account" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// create/account
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
  pin: "YOUR_PIN",
  // session: "YOUR_SESSION_ID", //optional
  // name: "TOKEN_NAME", //optional name to identify the account
  token_name: "username:tokenname", //optional if the token address is supplied.
  // token: "ADDRESS OF THE TOKEN", //optional if token_name is supplied
}
fetch(`${SERVER_URL}/tokens/create/account`, {
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
    # "session": "YOUR_SESSION_ID", #optional
    # "name": "TOKEN_NAME", #optional name to identify the account
    # optional if the token address is supplied.
    "token_name": "username:tokenname",
    # "token": "ADDRESS OF THE TOKEN", #optional if token_name is supplied
}
response = requests.post(f"{SERVER_URL}/tokens/create/account", json=data)
print(response.json())

```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) the token account should be created with. For single-user API mode the session should not be supplied.

`name` : An optional name to identify the account. If provided a Name object will also be created in the users local namespace, allowing the account to be accessed/retrieved by name. If no name is provided the account will need to be accessed/retrieved by its 256-bit register address.

`token_name` : This is the name of the token that the account can be used for. The token name should be supplied in the format `username:tokenname`. This is optional if the token address is supplied.

`token` : This is the address of the token that the account can be used for. This is optional if token\_name is supplied.

#### Example:

This example creates a token account called "main" for a token identified by the token name. NOTE the name has been qualified with a namespace which is the username of the signature chain that created the token

```
{
    "pin": "1234",
    "name": "main",
    "token_name": "bob:ABC"
}
```

#### Example:

This example creates a token account called "savings" for a token identified by its register address.

```
{
    "pin": "1234",
    "name": "savings",
    "token": "8CvLySLAWEKDB9SJSUDdRgzAG6ALVcXLzPQREN9Nbf7AzuJkg5P"
}
```

#### Return value JSON object:

```
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d",
    "address": "8FJxzexVDUN5YiQYK4QjvfRNrAUym8FNu4B8yvYGXgKFJL8nBse"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the account creation.

`address` : The register address for this token account. The address (or name that hashes to this address) is needed when creating crediting or debiting the account.

***

### `debit/account`

Deduct a token amount from a token account and send it to another token account. The API supports an alternative endpoint that can include the account name in the URI. For example `/tokens/debit/account/savings` will resolve to `tokens/debit/account?name=savings`.

Any fee that is applicable fo this transaction is deducted from the `default` account.

The method supports the ability to send to multiple recipients in one transaction by supplying a `recipients` array instead of the single `name_to`/`address_to`/`amount`. The method allows up to 99 recipients to be supplied.

#### Endpoint:

`/tokens/debit/account`

{% swagger method="post" path="/tokens/debit/account" baseUrl="http://api.nexus-interactions.io:8080" summary="debit/account" %}
{% swagger-description %}
Deduct a token amount from a token account and send it to another token account.
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) that owns the token account. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token account to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token account to debit. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" %}
The amount of tokens to debit
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name_to" %}
The name identifying the token account to send to. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address_to" %}
The register address of the token account to send to. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference" %}
This optional field allows callers to provide a reference, which the recipient can then use to relate the transaction to an order number, invoice number etc. The reference is be a 64-bit unsigned integer in the range of 0 to 18446744073709551615
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expires" %}
This optional field allows callers to specify an expiration for the debit transaction. The expires value is the 

`number of seconds`

 from the transaction creation time after which the transaction can no longer be credited by the recipient. Conversely, when you apply an expiration to a transaction, you are unable to void the transaction until after the expiration time. If expires is set to 0, the transaction will never expire, making the sender unable to ever void the transaction. If omitted, a default expiration of 7 days (604800 seconds) is applied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receipient" %}
This optional array can be provided as an alternative to the single 

`name_to`

/

`address_to`

, 

`amount`

, 

`reference`

, and 

`expires`

 fields. Each object in the array can have 

`name_to`

/

`address_to`

, 

`amount`

, 

`reference`

, and 

`expires`

 fields, as described above. Up to 99 recipients can be included in the array.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Debit token account" %}
```json
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// debit/account
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
  pin: "YOUR_PIN",
  //  session: "YOUR_SESSION_ID" //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  amount: 10,
  name_to: "TO_TOKEN_NAME", //optional if address_to is passed
  // address_to: "TO_TOKEN_ADDRESS", //optional if name_to is passed
  // reference: "64-bit unsigned integer", optional
  // expires: 604800, //optional (in seconds)
  // recipients: [
  //   { name: "NAME", amount: 10, name_to: "NAME_TO" },
  //   { name: "NAME", amount: 10, name_to: "NAME_TO" }
  // ] //optional
}
fetch(`${SERVER_URL}/tokens/debit/account`, {
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
    #  "session": "YOUR_SESSION_ID" #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    "amount": 10,
    "name_to": "TO_TOKEN_NAME",  # optional if address_to is passed
    # "address_to": "TO_TOKEN_ADDRESS", #optional if name_to is passed
    # "reference": "64-bit unsigned integer", optional
    # "expires": 604800, #optional (in seconds)
    # "recipients": [
    #   { "name": "NAME", amount: 10, name_to: "NAME_TO"
}
response = requests.post(f"{SERVER_URL}/tokens/debit/account", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) that owns the token account. For single-user API mode the session should not be supplied.

`name` : The name identifying the token account to debit. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the token account to debit. This is optional if the name is provided.

`amount` : The amount of tokens to debit.

`name_to` : The name identifying the token account to send to. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address_to` : The register address of the token account to send to. This is optional if the name is provided.

`reference` : This optional field allows callers to provide a reference, which the recipient can then use to relate the transaction to an order number, invoice number etc. The reference is be a 64-bit unsigned integer in the range of 0 to 18446744073709551615

`expires` : This optional field allows callers to specify an expiration for the debit transaction. The expires value is the `number of seconds` from the transaction creation time after which the transaction can no longer be credited by the recipient. Conversely, when you apply an expiration to a transaction, you are unable to void the transaction until after the expiration time. If expires is set to 0, the transaction will never expire, making the sender unable to ever void the transaction. If omitted, a default expiration of 7 days (604800 seconds) is applied.

`recipients` : This optional array can be provided as an alternative to the single `name_to`/`address_to`, `amount`, `reference`, and `expires` fields. Each object in the array can have `name_to`/`address_to`, `amount`, `reference`, and `expires` fields, as described above. Up to 99 recipients can be included in the array.

#### Example:

The following example shows the json payload for a debit of 10.5 tokens from an account called "main" (that itself was created by the sig chain logged into session "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8") being sent to a token account identified by the name "bob:savings". In the name\_to field, "bob" refers to the username of the account holder and "savings" is their token account. If Bob is concerned about privacy he could have provided the register address of his token account instead

```
{
    "pin": "1234",
    "session": "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8",
    "name": "main",
    "amount": 10.5,
    "name_to": "bob:savings"
}
```

#### Example Multiple Recipients:

The following example shows the json payload for a debit from an account called "main" made to 3 separate recipients, each receiving 5 tokens, and each with a different reference

```
{
    "pin": "1234",
    "name": "main"
    "recipients" :
    [
        {
            "name_to": "bob:abc",
            "amount": 5,
            "reference": 1234
        },
        {
            "address_to": "8CHjS5Qe7Mghgrqb6NeEaVxjexbdp9p2QVdRTt8W4rzbWhu3fL8",
            "amount": 5,
            "reference": 5678
        },
        {
            "address_to": "8CM4SYrd6ohcBB8tfqyZG3MCtDStMUXN37gwC2RtkNSUayM2FSN",
            "amount": 5
        }
    ]
}
```

#### Return value JSON object:

```
{
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the token debit.

***

### `credit/account`

Increment an amount received from another token account to an account owned by your signature chain. The API supports an alternative endpoint that can include the account name to credit in the URI. For example `/tokens/credit/account/savings` will resolve to `tokens/credit/account?name=savings`.

#### Endpoint:

`/tokens/credit/account`

{% swagger method="post" path="/tokens/credit/account" baseUrl="http://api.nexus-interactions.io:8080" summary="credit/account" %}
{% swagger-description %}
Increment an amount received from another token account to an account owned by your signature chain.
{% endswagger-description %}

{% swagger-parameter in="body" name="pin" required="true" %}
PIN for the user account
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the token account. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token account to credit. This is only required for split payments (where the receiving account is not included in the credit transaction) and is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the account to credit. This is only required for split payments (where the receiving account is not included in the credit transaction) and is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="txid" %}
The transaction ID (hash) of the corresponding debit transaction for which you are creating this credit for.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name_proof" %}
he name identifying the account that proves your ability to credit the debit transaction. This is only required for split payments, where your right to receive a payment is determined by the number of tokens you hold in the account proof account. The 

`name_proof`

 parameter can be used as alternative to 

`proof`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address_proof" %}
The register address the account that proves your ability to credit the debit transaction. This is only required for split payments, where your right to receive a payment is determined by the number of tokens you hold in the account proof account. The 

`address_proof`

 parameter can be used as alternative to 

`name_proof`
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="credited token" %}
```json
{
    "txid": "318b86d2c208618aaa13946a3b75f14472ebc0cce9e659f2830b17e854984b55606738f689d886800f21ffee68a3e5fd5a29818e88f8c5b13b9f8ae67739903d"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// // credit/account
const SERVER_URL = "http://api.nexus-interactions.io:8080"
let data = {
  pin: "YOUR_PIN",
  // session: "YOUR_SESSION_ID" //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  txid: "256 char hash", // (hash) of the corresponding debit transaction for which you are creating this credit for.
  amount: 10,
  name_to: "TO_TOKEN_NAME", //optional if address_to is passed
  // name_proof: "NAME_PROOF", //used only for split payments (optional if address_proof is passed)
  // address_proof: "REGISTER_ADDRESS" //optional if name_proof is passed 
}
fetch(`${SERVER_URL}/tokens/credit/account`, {
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
    # "session": "YOUR_SESSION_ID" #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    # (hash) of the corresponding debit transaction for which you are creating this credit for.
    "txid": "256 char hash",
    "amount": 10,
    "name_to": "TO_TOKEN_NAME",  # optional if address_to is passed
    # "name_proof": "NAME_PROOF", #used only for split payments (optional if address_proof is passed)
    # "address_proof": "REGISTER_ADDRESS" #optional if name_proof is passed
}
response = requests.post(f"{SERVER_URL}/tokens/credit/account", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`pin` : The PIN for this signature chain.

`session` : For multi-user API mode, (configured with multiuser=1) the session is required to identify which session (sig-chain) owns the token account. For single-user API mode the session should not be supplied.

`name` : The name identifying the token account to credit. This is only required for split payments (where the receiving account is not included in the credit transaction) and is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the account to credit. This is only required for split payments (where the receiving account is not included in the credit transaction) and is optional if the name is provided.

`txid` : The transaction ID (hash) of the corresponding debit transaction for which you are creating this credit for.

`name_proof` : The name identifying the account that proves your ability to credit the debit transaction. This is only required for split payments, where your right to receive a payment is determined by the number of tokens you hold in the account proof account. The `name_proof` parameter can be used as alternative to `proof`

`address_proof` : The register address the account that proves your ability to credit the debit transaction. This is only required for split payments, where your right to receive a payment is determined by the number of tokens you hold in the account proof account. The `address_proof` parameter can be used as alternative to `name_proof`

#### Example:

The following example shows the json payload for a credit to an account called "savings" (that itself was created by the sig chain logged into session "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8") identified by the name "bob:savings". In the name field, "bob" refers to the username of the account holder and "savings" is their token account.

```
{
    "pin": "1234",
    "session": "5e9d8aa625a1838f60f30e12058089169e32c968389f365428f7b0c878bb47f8",
    "name": "bob:savings",
    "txid": "f9dcd28bce2563ab288fab76cf3ee5149ea938c735894ce4833b55e474e08e8a519e8005e09e2fc19623577a8839a280ca72b6430ee0bdf13b3d9f785bc7397d"
}
```

#### Return value JSON object:

```
{
    "txid": "318b86d2c208618aaa13946a3b75f14472ebc0cce9e659f2830b17e854984b55606738f689d886800f21ffee68a3e5fd5a29818e88f8c5b13b9f8ae67739903d"
}
```

#### Return values:

`txid` : The ID (hash) of the transaction that includes the token credit.

***

### `get/account`

Retrieves information about a token account . The API supports an alternative endpoint that can include the account name in the URI. For example `/tokens/get/account/savings` will resolve to `tokens/get/account?name=savings`.

Additionally the API supports passing a field name in the URL after the account name, which will populate the `fieldname` parameter in the request and filter the response on that field. For example `/tokens/get/account/savings/balance` will resolve to `tokens/get/account?name=savings&fieldname=balance`

#### Endpoint:

`/tokens/get/account`

{% swagger method="post" path="/tokens/get/account" baseUrl="http://api.nexus-interactions.io:8080" summary="get/account" %}
{% swagger-description %}
Retrieves information about a token account .
{% endswagger-description %}

{% swagger-parameter in="body" name="name" %}
The name identifying the token account to retrieve. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the 

`session`

 parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the account. The 

`session`

 parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token account to retrieve. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="count" %}
Optional boolean field that determines whether the response includes the transaction 

`count`

 field. This defaults to false, as including the transaction count can slow the response time of the method considerably
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fieldname" %}
This optional field can be used to filter the response to return only a single field from the token account
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="token account details" %}
```json
{
    "owner": "a2e51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
    "created": 1566534164,
    "modified": 1566616211,
    "name": "myaccount",
    "address": "8CbkwEQ9S8owmX74joU6XmiwxJq1aoiqUoXc9fLCKzw15HscM99",
    "token_name": "mytoken",
    "token": "8EHRNnxn5qX9gMF1Jbqvo1jkAeP7XY1PETnMtegv9rdr6QG3ZJy",
    "balance": 990,
    "pending": 0.0,
    "unconfirmed": 10
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
// get/account
const SERVER_URL = "http://api.nexus-interactions.io:8080"

let data = {
  name: "TOKEN_NAME", //optional if address is passed
  // session: "YOUR_SESSION_ID", //optional
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  // count: false, //optional
  // fieldname: "FILTER_NAME", //optional
}
fetch(`${SERVER_URL}/tokens/get/account`, {
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
    "name": "TOKEN_NAME",  # optional if address is passed
    # "session": "YOUR_SESSION_ID", #optional
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    # "count": False, #optional
    # "fieldname": "FILTER_NAME", #optional
}
response = requests.post(f"{SERVER_URL}/tokens/get/account", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`name` : The name identifying the token account to retrieve. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the account was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the name in order to deduce the register address of the account. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`address` : The register address of the token account to retrieve. This is optional if the name is provided.

`count` : Optional boolean field that determines whether the response includes the transaction `count` field. This defaults to false, as including the transaction count can slow the response time of the method considerably.

`fieldname`: This optional field can be used to filter the response to return only a single field from the token account.

#### Return value JSON object:

```
{
    "owner": "a2e51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
    "created": 1566534164,
    "modified": 1566616211,
    "name": "myaccount",
    "address": "8CbkwEQ9S8owmX74joU6XmiwxJq1aoiqUoXc9fLCKzw15HscM99",
    "token_name": "mytoken",
    "token": "8EHRNnxn5qX9gMF1Jbqvo1jkAeP7XY1PETnMtegv9rdr6QG3ZJy",
    "balance": 990,
    "pending": 0.0,
    "unconfirmed": 10
}
```

#### Return values:

`owner` : The genesis hash of the signature chain that owns this account.

`created` : The UNIX timestamp when the account was created.

`modified` : The UNIX timestamp when the account was last modified.

`name` : The name identifying the token account. For privacy purposes, this is only included in the response if the caller is the owner of the token account

`address` : The register address of the account.

`token_name` : The name of the token that this account can be used with.

`token` : This is register address of the token that this account can be used with.

`balance` : The available balance of this account. This is the last confirmed balance less any new debits that you have made since the last block

`pending` : This is the sum of all confirmed debit transactions that have been made to this account, that have not yet been credited. To move coins from pending into the available balance you must create a corresponding credit transaction. NOTE: if configured to run, the events processor does this for you.

`unconfirmed` : This is the sum of all unconfirmed debit transactions that have been made to this account PLUS the sum of all unconfirmed credits that you have for confirmed debit transactions. When someone makes a debit to your account it will immediately appear in the unconfirmed balance until that transaction is included in a block, at which point it moves into `pending`. When you (or the events processor) creates the corresponding credit transaction for that debit, the amount will move from `pending` back into `unconfirmed` until the credit transaction is included in a block, at which point the amount moves to `balance`.

`count` : Only returned if the caller requested `count` : true. This is the number of transactions made to/from the account.

***

### `list/account/transactions`

This will list off all of the transactions related to a given account. You DO NOT need to be logged in to use this command. If you are logged in, then neither username or genesis are required as it will default to the logged in user.

{% hint style="info" %}
**NOTE** : The returned transaction data will only include contracts that related to the requested account. Any other contracts are omitted from the transaction result.

**NOTE** : If you use the username parameter it will take slightly longer to calculate the username genesis with our brute-force protected hashing algorithm. For higher performance, use the genesis parameter.
{% endhint %}

#### Endpoint:

`/tokens/list/account/transactions`

{% swagger method="post" path="/list/account/transactions" baseUrl="http://api.nexus-interactions.io:8080" summary="list/account/transactions" %}
{% swagger-description %}
This will list off all of the transactions related to a given account. You DO NOT need to be logged in to use this command. If you are logged in, then neither username or genesis are required as it will default to the logged in user.
{% endswagger-description %}

{% swagger-parameter in="body" name="genesis" required="false" %}
The genesis hash identifying the signature chain to scan for transactions (optional if username is supplied or already logged in)
{% endswagger-parameter %}

{% swagger-parameter in="body" required="false" name="username" %}
The username identifying the signature chain to scan for transactions(optional if genesis is supplied or already logged in
{% endswagger-parameter %}

{% swagger-parameter in="body" required="false" name="session" %}
For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the account name in order to deduce the register address of the account. The

`session`

parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.
{% endswagger-parameter %}

{% swagger-parameter in="body" required="false" name="name" %}
The name identifying the token account to list transactions for. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the object was created in the callers namespace (their username), then the username can be omitted from the name if the

`session`

parameter is provided (as we can deduce the username from the session)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" %}
The register address of the token account to list transactions for. This is optional if the name is provided
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verbose" %}


Optional, determines how much transaction data to include in the response. Supported values are :\


`default` : hash, contracts

`summary` : type, version, sequence, timestamp, operation, and confirmations.

`detail` : genesis, nexthash, prevhash, pubkey and signature
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" %}
The number of records to return for the current page. The default is 100
{% endswagger-parameter %}

{% swagger-parameter in="body" name="page" %}
Allows the results to be returned by page (zero based). E.g. passing in page=1 will return the second set of (limit) records. The default value is 0 if not supplied
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offset" %}
An alternative to 

`page`

, offset can be used to return a set of (limit) results from a particular index
{% endswagger-parameter %}

{% swagger-parameter in="body" name="where" %}
An array of clauses to filter the JSON results. More information on filtering the results from /list/xxx API methods can be found here Filtering Results
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="account transaction list" %}
```json
[
    {
        "txid": "01034b39cb3635d370f97339e6f87b8751d4c0d62676da7d6ec20416966f298f47dea99603d03a74e638b0d50b31b1e721790e5b103abfe3353a709ccf5d1e7c",
        "contracts": [
            {
                "OP": "CREDIT",
                "txid": "01e73b498dbabbf4629ad674b9ae3824b96cca83199c25a67901db53b271d19acf1411b0c4f9a3d8ded80860ffe2dcf683d2d227a675d453303b31f86f868f9e",
                "contract": 0,
                "proof": "a2e51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
                "to": "8CbkwEQ9S8owmX74joU6XmiwxJq1aoiqUoXc9fLCKzw15HscM99",
                "to_name": "test",
                "amount": 10,
                "token": "8EHRNnxn5qX9gMF1Jbqvo1jkAeP7XY1PETnMtegv9rdr6QG3ZJy",
                "token_name": "TST"
            }
        ]
    }
]
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Javascript" %}
```javascript
let data = {
  // genesis: "GENESIS_HASH", //optional 
  username: "YOUR_USERNAME",//optional
  // session: "YOUR_SESSION_ID", //optional
  name: "TOKEN_NAME", //optional if address is passed
  // address: "TOKEN_ADDRESS", // optional if name is passed 
  // verbose: "detail", //optional or "summary","none"
  // limit: 50, //optional
  // page: 1, //optional
  // offset: 10, //optional
  // where: "FILTERING SQL QUERY" //optional
}
fetch(`${SERVER_URL}/tokens/list/account/transactions`, {
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
    # "genesis": "GENESIS_HASH", #optional
    "username": "YOUR_USERNAME",  # optional
    # "session": "YOUR_SESSION_ID", #optional
    "name": "TOKEN_NAME",  # optional if address is passed
    # "address": "TOKEN_ADDRESS", # optional if name is passed
    # "verbose": "detail", #optional or "summary","none"
    # "limit": 50, #optional
    # "page": 1, #optional
    # "offset": 10, #optional
    # "where": "FILTERING SQL QUERY" #optional
}
response = requests.post(
    f"{SERVER_URL}/tokens/list/account/transactions", json=data)
print(response.json())
```
{% endtab %}
{% endtabs %}

#### Parameters:

`genesis` : The genesis hash identifying the signature chain to scan for transactions (optional if username is supplied or already logged in).

`username` : The username identifying the signature chain to scan for transactions(optional if genesis is supplied or already logged in).

`session` : For multi-user API mode, (configured with multiuser=1) the session can be provided in conjunction with the account name in order to deduce the register address of the account. The `session` parameter is only required when a name parameter is also provided without a namespace in the name string. For single-user API mode the session should not be supplied.

`name` : The name identifying the token account to list transactions for. This is optional if the address is provided. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). However, if the object was created in the callers namespace (their username), then the username can be omitted from the name if the `session` parameter is provided (as we can deduce the username from the session)

`address` : The register address of the token account to list transactions for. This is optional if the name is provided.

`verbose` : Optional, determines how much transaction data to include in the response. Supported values are :

* `default` : hash, contracts
* `summary` : type, version, sequence, timestamp, operation, and confirmations.
* `detail` : genesis, nexthash, prevhash, pubkey and signature.

`limit` : The number of records to return for the current page. The default is 100.

`page` : Allows the results to be returned by page (zero based). E.g. passing in page=1 will return the second set of (limit) records. The default value is 0 if not supplied.

`offset` : An alternative to `page`, offset can be used to return a set of (limit) results from a particular index.

`where` : An array of clauses to filter the JSON results. More information on filtering the results from /list/xxx API methods can be found here Filtering Results

#### Return value JSON object:

```
[
    {
        "txid": "01034b39cb3635d370f97339e6f87b8751d4c0d62676da7d6ec20416966f298f47dea99603d03a74e638b0d50b31b1e721790e5b103abfe3353a709ccf5d1e7c",
        "contracts": [
            {
                "OP": "CREDIT",
                "txid": "01e73b498dbabbf4629ad674b9ae3824b96cca83199c25a67901db53b271d19acf1411b0c4f9a3d8ded80860ffe2dcf683d2d227a675d453303b31f86f868f9e",
                "contract": 0,
                "proof": "a2e51edcd41a8152bfedb24e3c22ee5a65d6d7d524146b399145bced269aeff0",
                "to": "8CbkwEQ9S8owmX74joU6XmiwxJq1aoiqUoXc9fLCKzw15HscM99",
                "to_name": "test",
                "amount": 10,
                "token": "8EHRNnxn5qX9gMF1Jbqvo1jkAeP7XY1PETnMtegv9rdr6QG3ZJy",
                "token_name": "TST"
            }
        ]
    }
]
```

#### Return values:

`txid` : The transaction hash.

`type` : The description of the transaction (`legacy` | `tritium base` | `trust` | `genesis` | `user`).

`version` : The serialization version of the transaction.

`sequence` : The sequence number of this transaction within the signature chain.

`timestamp` : The Unix timestamp of when the transaction was created.

`blockhash` : The hash of the block that this transaction is included in. Blank if not yet included in a block.

`confirmations` : The number of confirmations that this transaction obtained by the network.

`genesis` : The signature chain genesis hash.

`nexthash` : The hash of the next transaction in the sequence.

`prevhash` : the hash of the previous transaction in the sequence.

`pubkey` : The public key.

`signature` : The signature hash.

`contracts` : The array of contracts bound to this transaction and their details with opcodes.\
{\
`id` : The sequential ID of this contract within the transaction.

`OP` : The contract operation. Can be `APPEND`, `CLAIM`, `COINBASE`, `CREATE`, `CREDIT`, `DEBIT`, `FEE`, `GENESIS`, `LEGACY`, `TRANSFER`, `TRUST`, `STAKE`, `UNSTAKE`, `WRITE`.

`for` : For `CREDIT` transactions, the contract that this credit was created for . Always `DEBIT` for token transactions.

`txid` : The transaction that was credited / claimed.

`contract` : The ID of the contract within the transaction that was credited / claimed.

`proof` : The register address proving the credit.

`from` : For `DEBIT`, `CREDIT`, `FEE` transactions, the register address of the account that the debit is being made from.

`from_name` : For `DEBIT`, `CREDIT`, `FEE` transactions, the name of the account that the debit is being made from. Only included if the name can be resolved.

`to` : For `DEBIT` and `CREDIT` transactions, the register address of the recipient account.

`to_name` : For `DEBIT` and `CREDIT` transactions, the name of the recipient account. Only included if the name can be resolved.

`amount` : the token amount of the transaction.

`token` : the register address of the token that the transaction relates to. Set to 0 for NXS transactions

`token_name` : The name of the token that the transaction relates to.

`reference` : For `DEBIT` and `CREDIT` transactions this is the user supplied reference used by the recipient to relate the transaction to an order or invoice number.

***
