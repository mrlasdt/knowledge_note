# Zero-knowledge proof
## Zero-knowledge proof
**Zero-knowledge proof** (or **Zero-knowledge protocol**) is a method by which one party (the prover) can prove to another party (the verifier) that they know a value x, without conveying any information apart from the fact that they know the value x. 

*Consequences*: 
+ no passwords are exchanged, which means they cannot be stolen.



+ A zero-knowledge proof must satisfy the following three parameters:

  + **Completeness**. If the statement is true, the honest verifier—the one that is following the protocol properly—will be convinced of this fact by an honest prover.
  + **Soundness**. If the statement is false, no cheating prover can convince the honest verifier that it is true, ***except for some small probability***.
  + **Zero knowledge**. If the statement is true, no verifier learns anything, except the fact that the statement is true. 
  $\to$ In other words, just knowing the statement (not the secret) is sufficient to imagine a scenario, showing that the prover knows the secret. This is achieved through each verifier having a simulator, which can produce a transcript that “looks like” an interaction between the honest prover and the verifier. The simulator should be able to produce the transcript, while only having access to the statement to be proved and not the prover itself.
  

> **Completeness and soundness are properties of more general interactive proof systems. The addition of zero knowledge is what turns the verification process into a zero-knowledge proof.**

Zero-knowledge proofs are not proofs in the mathematical sense of the term, because ***there is some small probability, the soundness error, that a cheating prover will be able to convince the verifier of a false statement***. In other words, ***zero-knowledge proofs are probabilistic proofs rather than deterministic ones***. However, there are some techniques to decrease the soundness error to negligibly small values.

## The general structure of a ZKP
The general structure of a zero-knowledge proof consists of three sequential actions between participants A and B. These actions are called a *witness*, a *challenge*, and a *response*.
+ ***Witness***. The fact that A knows the secret determines some set of the questions, which always can be answered by A correctly. At first, A chooses randomly any question from the set and calculates a proof. Then, A sends the proof to B.
<div style = "text-align:center">
<img src="/Media/blockchain-Zero-Knowledge-Proof-Witness.png">
<figcaption> A picks a random question and sends the proof to B</figcaption> 
</div>
