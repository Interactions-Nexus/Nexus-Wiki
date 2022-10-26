---
title: Commandline Arguments
description: 
published: true
date: 2022-10-26T21:09:34.384Z
tags: 
editor: markdown
dateCreated: 2022-10-19T16:22:49.820Z
---

# Commandline Arguments
This will list out all the command line parameters or core configuration parameters.


 | Parameter | Description | Values |
 | --- | --- | --- |
 | -addnode | Add to address manager and let it make connections | 
 | -api |  Handle for API if '/' symbol detected | |
 | -apiuser | The API authentication username | username |
 | -apipassword | The API authentication password | password |     
 | -apiauth | Enable/disable API authentication | 0/1 |
 | -apiconnect | Make the connection to the API server | |
 | -apiport | Manually assign the API port | port number |  
 | -apisssl | Enable SSL for API | 0/1 |
 | -apisslport | Assign a port for API SSL | port number|
 | -apisslrequired | Boolean for if API is using SSL | true/false |
 | -apithreads | | default = 8 |
 | -apicscore | | default = 5 |
 | -apirscore | | default = 5 |
 | -apitimespan | | default = 60 |
 | -apitimeout |
 | -argon2 | Hash generation algorithm | |
 | -argon2_memory | Memory allocation for argon2 | |
 | -autotx | Builds tx based on a list of contracts, to be deployed as a single tx or batched | default = false |
 | -avatar |
 | -authattempts | Session authentication failure counter | default = 3 |
 | -beta | Flag to disable checkpoint checks for non legacy mode | |
 | -blocknotify | Notification for new block created | |
 | -blockrefresh | Grab block expiration timestamp | default = 60 |
 | -client | Flag to enable lite mode | default = false |
 | -checkpoints | To go back the specified checkpoints on startup | default = 100 |
 | -connect |
 | -conf |
 | -contractcache| Create the contract database instance |
 | -cscore |
 | -datadir | Core data directory location |
 | -dbcache | Legacy database cache size | default = 25 |
 | -ddos |
 | -dnsupdate | Check if DNS needs update | default = 86400 |
 | -dns | Flag to enable DNS nodes provided | default = true |
 | -flushwallet | Legacy - Flag to flush wallet database  | |
 | -forcereindex | Flag to force reindex if needed | 
 | -forkblocks | Rewind the chain to the specified number of blocks | default = 0 |
 | -gdb | GDB mode waits for keyboard input to initiate clean shutdown | |
 | -generate | Block generation password for private networks | 
 | -httpheader | Dump the header on every read |
 | -httpresponse | Flag to log http response | default = false |
 | -hybrid | Hybrid network Identity | password |
 | -inactivetimeout | Session inactivity timout | default = 3600 |
 | -indexheight | Enable block height indexing| 0/1 |
 | -indexaddress | Enable address indexing | 0/1 | 
 | -latency | Latency to create blocks in private or hybrid mode | |
 | -ledgercache | Create the ledger database instance |
 | -legacycache | Create the legacy database instance |
 | -latency | The duration to create blocks in private networks |
 | -llpsleep | cache sleep timer | default = 0 |
 | -lldmeters | Flag to track LLD meter thread | |
 | -legacy | To check if address is legacy |
 | -limitfreerelay | Rate limit free transactions to limit flooding | |
 | -listen |
 | -logfiles | Debug logging configuration parameter | default = 20 |
 | -logsizeMB | Debug logging configuration parameter | default = 5 |
 | -keypool |  Desired legacy keypool size |
 | -manager | |
 | -mining | Enable mining on the node|
 | -miningthreads |
 | -miningcscore |
 | -miningrscore |
 | -miningtimespan |
 | -miningtimeout |
 | -miningddos |
 | -miningport | Change mining port |
 | -meters |
 | -maturityrequired | Signature chain maturity check to create new transaction | |
 | -maxconnections | Set maximum peer connections to the node | default = 100 |
 | -maxincoming | Set maximum incoming peer connections  | default = 84 |
 | -maxoutgoing | Set maximum outgoing peer connections  | default = 16 |
 | -maxcontracts | Set maximum number of contracts per transaction | default = 99 |
 | -maxsendbuffer | Write buffer overflow check |
 | -maxsendsize | Set the maximum bytes to flush to 2^16 or max socket buffer |
 | -marketfee | To enable and set fee for the P2P marketplace | |
 | -nodns | Flag to disable DNS provided | |
 | -notificationsthread | Total no of manager threads | default = 1 |
 | -pid | (Nexus.pid) PID file full pathname | |
 | -printstate | Flag to output the block state | |
 | -prunefailed | Kill address if no valid address is found | default = 0|
 | -printselectcoin | Legacy - 
 | -p2pport | Change p2p port |
 | -p2psslport | Change p2p SSL port |
 | -port |
 | -private | Enable the node to run as a private chain | |
 | -primemod | Flag to reduce the lash proof down to 1017-bit to maximize prime ratio  | default = false | 
 | -registercache | Create the register database instance |
 | -rpcuser | The RPC authentication - username |
 | -rpcpassword | The RPC authentication - password |
 | -rpcremote | Enable RPC remote access | 0/1 |
 | -rpcthreads | | default = 4 |
 | -rpccscore | | default = 5 |
 | -rpcrscore | | default = 5 |
 | -rpctimespan | | default = 60 |
 | -rpcport |
 | -rpcconnect | Make the connection to the RPC server | |
 | -rpcssl | | true/false |
 | -rpcsslport | | |
 | -rpcsslrequired | | true/false |
 | -rpcmeters |  | true/false |
 | -rscore |
 | -regtest | Flag to handle regression testing blocks | |
 | -runtime | Flag to check if the database is running | default = false |
 | -rescan | Legacy - Flag to handle rescanning database | |
 | -reindexheight | Flag to force reindexing height | |
 | -requirepassword | Flag to force password authntication for unlocking session |
 | -safemode | Recalculate nexthash to protect against nexthash corruption |
 | -sessionlocks | Create session locks | default = 1024 |
 | -serverport |
 | -serversslport |
 | -ssl |
 | -sslport | Change SSL port |
 | -sslrequired |
 | -sslcertificate | ssl - certificate location | location |
 | -sslcertificatekey | ssl - keyfile location | location |
 | -sslcabundle | ssl - cabundle location | location|
 | -stake | Enable staking on node |
 | -sync | Flag denoting the synchronization status | |
 | -syncbatchsize | Do a sequential read to obtain the list | default = 3000 |
 | -system/stop | Core shutdown authentication password | password |
 | -terminateauth | Check for authenticated sigchain | |
 | -testnet | Enable the node to be a testnet | Number (0 - 92349234) |
 | -threads | |
 | -timeout | |
 | -timespan | |
 | -trustboost | Preset trust for testing on testnet | |
 | -upnp | upnp flag which will enable required port forwarding | default = true |
 | verbose | Enable verbose logging  | 0, 1, 2, 3 default = 0|
 | -wallet | Load the legacy wallet | |
 | -walletcheck |
 | -walletclean |