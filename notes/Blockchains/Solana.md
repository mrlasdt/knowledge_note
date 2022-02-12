# Accounts
+ **Definition** : Accounts within Solana are used to store state. There are an essential building block for developing on Solana
  + Accounts are used to store data
  + Each account has unique address
  + Accounts have a max size of 10mb
  + Program Derived Address(PDA) accounts have a max size of 10kb
  + PDA accounts can be used to sign on behalf of a program
  + Account size is static
  + Account data storage is paid with rent
  + Default account owner is the System Program
+ There are 3 kinds of accounts:
  + Data accounts: store data: 2 types
    + System owned accounts
    + PDA accounts
  + Program accounts: store executable programs
  + Native accounts: indicate native programs on Solana such as System Stake, and Vote $\to$ Don't understand what is it
+ Each account has an address(usually a public key) and an owner(address of a program account). The full field list an account stores is: 
  <div style = "text-align:center">
  <img src="/Media/solana_accounts_contains.png">
  <figcaption> Information is stored by account</figcaption> 
  </div>
+ **Rent** : Validators on the Solana network need to maintain a working copy of this state in memory, the network charges a time-and-space based fee for this resource consumption, also known as rent. 
  > **Note**
  + Only a data account's owner can modify data and debit lamports.
  + Anyone is allowed to creadit lamports to a data account
  + The owner of an account may assign a new owner if the account's data is zeroed out
  + Program accounts do not store state $\to$ use have to use another data account to store state.
    + Example: if you have a counter program that lets you increment a counter , you must create two accounts. one account to store the program's code, and one to store the counter.
  > **Terminology**
    + Program Derived Address(PDA): an account whose owner is a program and thus is not controlled by a private key like other accounts.
# Programs
+ **Definition**: known as smart contracts on other protocols.
+ Facts
  + Programs process instructions from both end users and other programs
  + All programs are stateless: any data they interact with is stored in separate accounts that are passed via instruction
  + Programs themselves are stored in accounts marked as executable
  + All programs are owned by BPF loader and executed by Solana Runtime
  + Developers most commonly write programs in rust or C++, bu can choose any language that targets the LLVM's BPF backend
  + All programs have a single entry point where instruction processing take place; parameters always include:
    + program_id: pubkey
    + accounts: array,
    + instruction_data: byte array
+ Writing programs:
  <div style = text-align:center>
  <img src ="/Media/solana_program_struct.png">
  <figcaption> Program architecture in Solana</figcaption>
  </div>
> **Note**:
   + Solana completely separates code from data $\to$ all data that programs interact with are stored in sperate accounts and passed in as references via instructions.

# Transactions

+ **Definition**: clients invoke programs by submitting a transaction to a cluster. When a transaction is submitted, the Solana Runtime will process its instruction in order. If any part of an instruction fails, the entire transaction will fail
+ Facts
  + Instructions are the most basic operational unit on Solana.
  + Each instruction contains:
    + The programid of the intended program.
    + An array of all accounts it intends to read from or write to.
    + An instruction_data byte array that is specific to the intended program.
  + Multiple instructions can be bundled into a single transaction. 
  + Each transaction contains:
    + An array of all accounts it intend to read from or write to
    + One or more instructions
    + A recent blockhash
    + One or more signatures
  + Instructions are processed in order and atomically.
  + If any part of an instruction fails, the entire transaction fails.
  + Transactions are limited to 1232 bytes.
+ **Fees**:
  + 2 types of fees:
    + Transaction fees for propagating transactions(aka "gas fees")
    + Rent fees for storing data on-chain
> **Note**
> + all transactions require at least one writable account to sign the transaction $\to$ pay for transaction fees.
# References: 
  + https://docs.solana.com/developing/programming-model/overview
  + https://spl.solana.com/
  + [Solana Cookbook](https://solanacookbook.com/references/programs.html#how-to-do-cross-program-invocation)



# New words
+ executable(adj): có thể thực hiện. 
+ grant(v): cấp, chấp nhận.
+ bundle(v) into : nhét vào.