---
title: REGISTER
description: Register API
published: true
date: 2022-11-02T20:24:09.092Z
tags: api
editor: markdown
dateCreated: 2022-10-05T08:35:09.936Z
---

# REGISTER

The Register API gives access to the register data and this allows network wide information to be presented. The full supported endpoint of the profiles URI is as follows:

```
register/verb/noun/filter/operator
```

The minimum required components of the URI are:

```
register/verb/noun
```

## `Supported Verbs`

The following verbs are currently supported by this API command-set:

`get` - Get object of supported type.\
`list` - List all objects owned by given user.\
`history` - Generate the history of all last states.\
`transactions` - List all transactions that modified specified object.

## `Supported Nouns`

The following nouns are supported for this API command-set:

\[`crypto`] - An object register which holds public key hashes.\
\[`object`] - An object register containing user-defined data structure.\
\[`raw`] - An object register of type raw.\
\[`readonly`] - An object register of type readonly.\
\[`any`] - An object selection noun allowing mixed accounts of different tokens.

## `Supported API/noun`

#### `Finance API:`

\[`finance:account`] - An object register containing a token-id and balance.\
\[`finance:trust`] - An object register containing a token-id, balance, and trust.\
\[`finance:token`] - An object register containing a token-id, balance, supply, and decimals.

#### `Names API:`

\[`names:local`] - An object register containing local names.\
\[`names:global`] - An object register containing global names.\
\[`names:namespaces`] - An object register containing namespaces.

#### `Invoices API:`

\[`invoices:outstanding`] - An object register containing outstanding invoices.\
\[`invoices:paid`] - An object register containing outstanding invoices.\
\[`invoices:cancelled`] - An object register containing cancelled invoices.

#### `Assets API:`

\[`assets:asset`] - An object register containing asset object.\
\[`assets:raw`] - An object register containing raw asset object.\
\[`assets:readonly`] - An object register containing readonly asset object.

#### `Supply API:`

\[`supply:item`] - An object register containing item object.\
\[`supply:raw`] - An object register containing raw item object.\
\[`supply:readonly`] - An object register containing readonly item object.

## `get` <a href="#get" id="get"></a>

Retrieves information for a single object for a type specified by the noun or API:noun

```
register/get/noun
```

This command supports all the nouns.

```
register/get/API:noun
```

This command supports all the API:nouns.

**get/crypto**

Retrieves information for a specified profile crypto object register.

**get/object**

Retrieves information for a specified object register.

**get/readonly**

Retrieves information for a specified readonly register.

**get/raw**

Retrieves information for a specified raw register.

**get/append**

Retrieves information for a specified append register.

### Parameters:

`name` : Required to **identify** the name of the account/trust/token. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). This is optional if the `address` is provided

`address` : Required to **identify** the register address of the account/trust/token. This is optional if the `name` is provided.

[`Sorting`](https://docs/API/SORTING.MD).

[`Filtering`](../filtering.md).

## `list` <a href="#list" id="list"></a>

This method provides the user with the ability to directly access the object register data specified by the noun and does not need the user to be logged in.

```
register/list/noun
```

This command supports all the nouns.

```
register/list/API:noun
```

This command supports all the API:nouns.

**list/crypto**

Returns a list of all the crypto object registers.

**list/object**

Returns a list of all the object registers.

**list/readonly**

Returns a list of all the readonly registers.

**list/raw**

Returns a list of all the raw registers.

**list/append**

Returns a list of all the append registers.

### Parameters:

`where` : An array of clauses to **filter** the JSON results. More information on filtering the results from /list/xxx API methods can be found here: `Queries`

[`Sorting`](https://docs/API/SORTING.MD).

[`Filtering`](../filtering.md).

[`Operators`](https://docs/API/OPERATORS.MD).

## `history` <a href="#history" id="history"></a>

This will get the history of the specified noun.

```
register/history/noun
```

This command supports all the nouns.

```
register/history/API:noun
```

This command supports all the API:nouns.

**history/crypto**

This will get the history of the specified crypto object register.

**history/object**

This will get the history and ownership of the specified object register.

**history/readonly**

This will get the history and ownership of the specified readonly register.

**history/raw**

This will get the history and ownership of the specified raw register.

**history/append**

This will get the history and ownership of the specified append register.

### Parameters:

`name` : Required to **identify** the name of the account/trust/token. The name should be in the format username:name (for local names) or namespace::name (for names in a namespace). This is optional if the `address` is provided

`address` : Required to **identify** the register address of the account/trust/token. This is optional if the `name` is provided.

[`Sorting`](https://docs/API/SORTING.MD).

`Filtering`.

[`Operators`](https://docs/API/OPERATORS.MD).

## `transactions` <a href="#transactions" id="transactions"></a>

This will list off all of the transactions for the specified noun.

```
register/transactions/noun
```

This command supports all the nouns.

```
register/transactions/API:noun
```

This command supports all the API:nouns.

**transactions/crypto**

List out all the transactions for the specified crypto object register.

**transactions/object**

List out all the transactions for the specified object register.

**transactions/readonly**

List out all the transactions for the specified readonly register.

**transactions/raw**

List out all the transactions for the specified raw register.

**transactions/append**

List out all the transactions for the specified append register.

### Parameters:

`verbose` : Optional, determines how much transaction data to include in the response. Supported values are :

* `default` : hash
* `summary` : type, version, sequence, timestamp, operation, and confirmations.
* `detail` : genesis, nexthash, prevhash, pubkey and signature.

[`Sorting`](https://docs/API/SORTING.MD).

`Filtering`.

[`Operators`](https://docs/API/OPERATORS.MD).

## `Register API with Query DSL`

A few register API calls which will showcase the power of registers, LLD, which is the database and Query-DSL. This is going to be a powerful tool for developers.

All these calls will require the latest build of the core and will not work with the current stable version.

To calculate the sum of all NXS on the tritium chain:

```
register/list/finance:accounts,finance:trust/total/sum limit=none where='results.total>0 AND results.ticker=NXS'
```

List all the namespaces sorted by created date in ascending order:

```
register/list/names:namespaces sort=created order=asc
```

List all the global names on the network:

```
register/list/names:global
```

Create a rich list:

```
register/list/finance:accounts,finance:trust sort=total order=desc page=0 where='results.token=0'
```

***
