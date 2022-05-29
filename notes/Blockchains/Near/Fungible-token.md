# Fungible token

Fungible token include two part: 
+ Storage standard: addresses the needs ( and security) for storage staking
+ Fungible token metadata standard: provides the fields needed for ergonomics across dApps and marketplaces. 


## Motivation
**NEAR Protocol uses an asynchronous, sharded runtime**. This means the following:
+ Storage for different contracts and accounts can be located on the different shards.
+ Two contracts can be executed at the same time in different shards.

**Example**
One contract wants to query some information from the state of another contract (e.g. current balance), by the time the first contract receives the balance the real balance can change.
$\to$ In such an async system, a contract can't rely on the state of another contract and assume it's not going to change.
$\to$ need to send a request and confirm back in 1 transaction. However we should avoid deadlock. 
$\to$ implemented in  [Near contract standard](https://nomicon.io/Standards/Tokens/FungibleToken/Core#reference-level-explanation)


## Reference
+ https://nomicon.io/Standards/Tokens/FungibleToken/Core

