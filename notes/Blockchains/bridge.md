# BRIDGE
**Accounts**: We will need 3 types of accounts in both blockchain network(source and destination chain).
| type | Description |
| ---- | ----------- |
| Admin | The account pays the gas fees when deploying contracts, registering resources IDs, updating setting in the contracts, or minting tokens.| 
| Relayer | The account used in the relayer to create transactions to vote or execute a proposal. The relayer accounts pay gas fees when sending transaction for voting and execution in the destination chain.| 
| User | The sender/recipient account that sends/receives assets. The sender account pays the gas fee when approving tokens transfers and calling ```deposit``` in the Bridge contract to begin a transfer. |

## Setup
### Contract setup
```
Setup for cb-sol-cli
git clone https://github.com/ChainSafe/chainbridge-deploy
cd chainbridge-deploy/cb-sol-cli
make install
```
> Notes:
>  + Update version of etherjs up tp v5.
>  + Remove gas price and gas limit when deploying. 


**Step 1**: Deploy necessary contract on source rinkeby
```
cb-sol-cli deploy --all --chainId 4 \
  --url https://rinkeby-light.eth.linkpool.io/ \
  --privateKey 0xe9753797850779570c4dac1cce32023838483c01e768b5c3ea50f777a230dae5\
  --relayers 0xC533fb3571eBDde01ee37eaF01a3b8727066791B \
  --relayerThreshold 1
```
Sample output
```
Deploying contracts...
deploying...
✓ Bridge contract deployed
✓ ERC20Handler contract deployed
✓ ERC721Handler contract deployed
✓ GenericHandler contract deployed
✓ ERC20 contract deployed
WARNING: Multiple definitions for safeTransferFrom
✓ ERC721 contract deployed

================================================================
Url:        https://rinkeby-light.eth.linkpool.io/
Deployer:   0xC533fb3571eBDde01ee37eaF01a3b8727066791B
Gas Limit:   8000000
Gas Price:   20000000
Deploy Cost: 0.021880131116694032

Options
=======
Chain Id:    4
Threshold:   1
Relayers:    0xC533fb3571eBDde01ee37eaF01a3b8727066791B
Bridge Fee:  0
Expiry:      100

Contract Addresses
================================================================
Bridge:             0x631F42620999113aA5f31f13422C6087795266e3
----------------------------------------------------------------
Erc20 Handler:      0x03E86f791e459864d6666b5FB8bE1888581Ceb49
----------------------------------------------------------------
Erc721 Handler:     0x6c0A9fd7a7dE35BD7c14C502eCcEc079ae706e71
----------------------------------------------------------------
Generic Handler:    0x4f940986718A98d925d7d240aeF2ce94291bc90b
----------------------------------------------------------------
Erc20:              0x7BC63DE735ba8bE2B14a6fe0d9082DaB0B0E03BC
----------------------------------------------------------------
Erc721:             0x7334975bdEaE94525cD447Cd96edaA7A41b8614B
----------------------------------------------------------------
Centrifuge Asset:   Not Deployed
----------------------------------------------------------------
WETC:               Not Deployed
================================================================
```


**step 2**: deploy contracts on destination chain (BNB testnet)
```
cb-sol-cli deploy --all --chainId 97\
  --url https://data-seed-prebsc-1-s2.binance.org:8545/ \
  --privateKey 0x974789ec2d8b85789d9275e5c65cf9c8be8a1944fd3cb0a5ffa52341b1b2b019 \
  --relayers 0xd19D90A68F6Ed4FfA2ae603Fb764ca1064463000 \
  --relayerThreshold 1
```
Output:
```
Deploying contracts...
deploying...
✓ Bridge contract deployed
✓ ERC20Handler contract deployed
✓ ERC721Handler contract deployed
✓ GenericHandler contract deployed
✓ ERC20 contract deployed
WARNING: Multiple definitions for safeTransferFrom
✓ ERC721 contract deployed

================================================================
Url:        https://data-seed-prebsc-1-s2.binance.org:8545/
Deployer:   0xd19D90A68F6Ed4FfA2ae603Fb764ca1064463000
Gas Limit:   8000000
Gas Price:   20000000
Deploy Cost: 0.14532606

Options
=======
Chain Id:    97
Threshold:   1
Relayers:    0xd19D90A68F6Ed4FfA2ae603Fb764ca1064463000
Bridge Fee:  0
Expiry:      100

Contract Addresses
================================================================
Bridge:             0x177DEDdE1B4FAcF2e67179E9CD054aeB51087800
----------------------------------------------------------------
Erc20 Handler:      0xe4f07401b58C493dbf5dA742c8BD38A9b8bf38a4
----------------------------------------------------------------
Erc721 Handler:     0x51F8Cbdcde973F0C1CDbF818BbceF24900277Bf4
----------------------------------------------------------------
Generic Handler:    0xE8D618C943531A268256Daed5c1c66A6345cc4d0
----------------------------------------------------------------
Erc20:              0xf06f53EEf6E78eAD6eDf5342901cF182A04Ee823
----------------------------------------------------------------
Erc721:             0xab75b527799E6b522e786B53cc9A875f46856d4E
----------------------------------------------------------------
Centrifuge Asset:   Not Deployed
----------------------------------------------------------------
WETC:               Not Deployed
================================================================
```

+ you can check [ChainID](https://chainlist.org/) here. 

### Replayer Setup 


Clone and build ChainBridge repository.
```
git clone https://github.com/ChainSafe/ChainBridge.git
cd chainBridge && make build
```
Follow [docs](https://chainbridge.chainsafe.io/live-evm-bridge/)

## Bridging flow
<div style = "text-align:center">
<img src= "Media/Bridging_flow.png">
<figcaption> Bridging flow </figcaption>
</div>

> Notes: 
> + private key: start with 0x
> + update ether v4 -> v5
> + remove gas price + gas limit
> + convert truffle to hardhat
>  ... 
## REFERENCE
+ https://chainbridge.chainsafe.io/live-evm-bridge/