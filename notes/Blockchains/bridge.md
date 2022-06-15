# BRIDGE
**Accounts**: We will need 3 types of accounts in both blockchain network(source and destination chain).
| type | Description |
| ---- | ----------- |
| Admin | The account pays the gas fees when deploying contracts, registering resources IDs, updating setting in the contracts, or minting tokens.| 
| Relayer | The account used in the relayer to create transactions to vote or execute a proposal. The relayer accounts pay gas fees when sending transaction for voting and execution in the destination chain.| 
| User | The sender/recipient account that sends/receives assets. The sender account pays the gas fee when approving tokens transfers and calling ```deposit``` in the Bridge contract to begin a transfer. |
## Bridging flow
<div style = "text-align:center">
<img src= "Media/Bridging_flow.png">
<figcaption> Bridging flow </figcaption>
</div>

## REFERENCE
+ https://chainbridge.chainsafe.io/live-evm-bridge/