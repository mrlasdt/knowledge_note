# **ETHEREUM**

## **Driving Factors**.
+ **Goals of this project**: 
  + *key goal* is to facilitate transactions between consenting individuals who would otherwise have no means to trust one another.
## Definition 
+ *Mining* is the process of dedicating effort (working) to bolster one series of transactions (a block) over any other potential competitor block. 
### Basic concepts: Blocks,State, Transactions
1. *The world state (state)* is a mapping between addresses (160-bit identifiers) and account states (a data structure serialized as RLP, see Appendix).





$$\begin{aligned}
\sigma_(t+1) &\equiv \Pi(\sigma_t, B)\\
B &\equiv (\dots , (T_0,T_1,\dots), \dots)\\
\Pi(\sigma, B) &\equiv \Omega(B, \Upsilon (\Upsilon(\sigma, T_0), T_1))\dots)
\end{aligned}$$
Where: 
  + $\Omega$ is the block-finalization state transition function (a function that rewards a nominated party);
  + B is this block, which includes a series of transactions amongst some other components; 
  + $\Pi$ is the block-level state-transition function.

## Fork
Since the system is decentralized and all parties have an opportunity to create a new block on some older pre-existing block
$\to$ the resultant structure is necessarily a tree of blocks. In order to form a consensus as to which path, from root (the genesis block) to leaf (the block containing the most recent transactions) through this tree structure, known as the blockchain, there must be an agreed-upon scheme. 
$\to$If there is ever a disagreement between nodes as to which root-to-leaf path down the block tree is the ‘best’ blockchain, then a fork occurs.

This would mean that past a given point in time (block), multiple states of the system may coexist: some nodes believing one block to contain the canonical transactions, other nodes believing some other block to be canonical, potentially containing radically different or incompatible transactions. This is to be avoided at all costs as the uncertainty that would ensue would likely kill all confidence in the entire system. 
## APPENDIX

### RECURSIVE LENGTH PREFIX (RLP)
+ This is a serialization method for encoding arbitrarily structured binary data (byte arrays).
+ We define the set of possible structures $\mathbb{T}$:

$$\begin{aligned}
\mathbb{T} &= \mathbb{L} 
\end{aligned}$$

## New words

