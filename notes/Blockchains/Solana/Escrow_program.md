
# Interactive with Program
+ In Solana network, only account that owned by program can call program function. 
+ Normal account (wallet) that owned by system program $\to$ so that it only call system program $\to$ If we want to call another program(Smart contract) we should create an account that owned by this program. 
  <div style = "text-align:center">
  <img src="/Media/solana_program.drawio.png">
  <figcaption> Account interact with program</figcaption> 
  </div>

  ```ts 
    const GREETING_SEED = 'hello';// any string
    let programId: PublicKey;
    /**
    * The state of a greeting account managed by the hello world program
    */
    // state 
    class GreetingAccount {
        counter = 0;
        constructor(fields: {counter: number} | undefined = undefined) {
            if (fields) {
            this.counter = fields.counter;
            }
        }
    }

    const GreetingSchema = new Map([
    [GreetingAccount, {kind: 'struct', fields: [['counter', 'u32']]} ]]);
    //The expected size of each greeting account.
    const GREETING_SIZE = borsh.serialize(
            GreetingSchema,
            new GreetingAccount(),
    ).length;

   const greetedPubkey = await PublicKey.createWithSeed(
        payer.publicKey,// PublicKey
        GREETING_SEED,// String
        programId,// Publickey
    ); // -> return publickey


    // we use greetedPubkey stand for payer public key. Cause payer account is owned by system program -> its can't call this program. 
    // check whether account exist on solana network
    const greetedAccount = await connection.getAccountInfo(greetedPubkey);
    // if it not exist
    if (greetedAccount === null) {
        // estimate lamports to rent the location on Solana network for account
        const lamports = await connection.getMinimumBalanceForRentExemption(
        GREETING_SIZE,
        );
        // create account -> this will owned by programId. (greetedpubkey.owner = programId)
        // space: we need to calculate extract space account gonna take.

        const transaction = new Transaction().add(
        SystemProgram.createAccountWithSeed({
            fromPubkey: payer.publicKey,
            basePubkey: payer.publicKey,
            seed: GREETING_SEED,
            newAccountPubkey: greetedPubkey,
            lamports,
            space: GREETING_SIZE,
            programId,
        }),
        );
        // add to transaction and call 
        await sendAndConfirmTransaction(connection, transaction, [payer]);
    }

  ```
