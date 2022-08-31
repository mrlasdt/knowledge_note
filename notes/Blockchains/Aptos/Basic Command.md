# Aptos basic

+ Fund account: 
`aptos account fund-with-facet --account ACCOUNT_ADDRESS`
+ Compile
`aptos move compile --named-addresses hello_blockchain=0xa345dbfb0c94416589721360f207dcc92ecfe4f06d8ddc1c286f569d59721e5a`
+ test 
`aptos move test --named-addresses hello_blockchain=0xa345dbfb0c94416589721360f207dcc92ecfe4f06d8ddc1c286f569d59721e5a`
+ publish 
`aptos move publish --named-addresses hello_blockchain=0xa345dbfb0c94416589721360f207dcc92ecfe4f06d8ddc1c286f569d59721e5a
`

> Move modules expose access points or `entry functions`. These can be called via transactions. 


## Move-Aptos example step by step
+ https://github.com/move-language/move/tree/main/language/documentation/tutorial
+ Move abilities: 
+ Swap coin example: https://github.com/move-language/move/blob/main/language/documentation/examples/experimental/coin-swap/sources/PoolToken.move
+ https://docs.pontem.network/03.-tutorials/move-code-playground-tutorial-01