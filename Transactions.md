**Transactions**

*Most common: Pay-To-Public-Key-Hash (P2PKH)*

**Alice sending Bob some bitcoin**

First, Bob will provide Alice with an address to receive the bitcoin. An address is basically the hash of a public key which includes a version number, the hash itself and an error checksum. The public key itself was derived from a generated private key using ECDSA with a sep251k curve.

When Alice has the address, she creates a transaction with instructions using a script, such that whoever can prove ownership of the private key corresponding to the public key provided by Bob can spend that output. This script is called the *pubkey script* or *scriptPubKey*.
Alice then broadcasts the transaction to the network and the transaction is added to the block chain (through mining) as an *UTXO* (Unspent Transaction Output). 

Bob sees this transaction as spendable bitcoin in his wallet. If Bob wants to spend it, he similarly creates a transaction where one of his inputs will reference the UTXO (created by Alice's transaction). Specifically, the transaction hash(txid) and the output that Alice used (output index). 
Bob then creates a set of instructions using a script that will attempt to satisfy the conditions Alice placed on the output. This script is called a *signature script* or *scriptSig*

### How is the transaction validated

So each transaction in the blockchain has two scripts, *scriptPubKey* locks a transaction output while *scriptSig* unlocks that transaction output.  When Bob wants to spend the received bitcoin, it is the miners who will concatenate the two scripts and validate that the UTXO was locked to Bob's private key and that he has provided a signature to prove he own that private key. The evaluation/validation is done using the Script language which is a minimal programming language.
Stack evaluates statements left to right and puts each into a stack for evaluation. The final result evaluates either to a true or false.

