# Blockchain-Homework-18: Proof of Authority Blockchain

###
A Proof of Authority (PoA) algorithm was used to set up a private blockchain for this assignment.  In comparison to a proof of work algorithm (PoW), the PoA requires pre-approval of the account addresses that can approve transactions, rather than showing the amount of work that was done to mine the transaction.

## Node Account Creation

The first step is to create two accounts for two nodes for the network using geth
  * ./geth --datadir node1 account new
  * ./geth --datadir node2 account new

The above commands will generate two node accounts that will be used
  * node1 address: 0xe1568a26aba294A071Db1a93ff0Bbdcd485d1b90
  * node2 address: 0x98f11f89D5bC1e9f5aF6b4fB2bf76A057797033b

## Blockchain Genesis

A new genesis block called "blockchain" was generated using puppeth and Clique (PoA) concensus algothrithm was used.

![Blockchain Genesis](https://github.com/Davisg1179/Blockchain-Homework-18/blob/main/images/Blockchain%20Genesis.png)

As seen in the image above, we were asked how many seconds should each block take.  The default value is 15 seconds, however I elected for 5 seconds for a shorter time.  In the next two steps, we are asked which accounts are allowed to seal and which accounts should be pre-funded.  The two accounts that were generated in the node account created step above were used for both steps, being sure to keep the order.

The precompile-addresses were pre-funded with 1 wei, and a chain/network ID was specified, in this case it's 787.

The genesis specs for "blockchain" were then exported and saved to a file folder so that we can use the blockchain.json file later.

## Node Initialization

Each node was initialized using the generated blockchain.json file using geth
  * ./geth --datadir node1 init blockchain.json
  * ./geth --datadir node2 init blockchain.json

## Begin Mining Blocks

In the terminal the following command to unlock the node1 address was executed 
  * ./geth --datadir node1 --unlock "0xe1568a26aba294A071Db1a93ff0Bbdcd485d1b90" --mine --rpc --allow-insecure-unlock --syncmode full

The command was successful as seen in the screenshot below:
![Unlock node1](https://github.com/Davisg1179/Blockchain-Homework-18/blob/main/images/unlock%20first%20account.png)

Similarly, node2 was unlocked using the command:
  * ./geth --datadir node2 --unlock "0x98f11f89D5bC1e9f5aF6b4fB2bf76A057797033b" --mine --port 30304 --bootnodes "enode://993d998112cadac8ecc9fec1f7e0fc6ba4b3966d36393a5b3c6d0f3d7e587850454088b6e46900ff5d0c6c197010ff52b596b702c8c4943cd958213c5b749d44@127.0.0.1:30303" --allow-insecure-unlock --syncmode full

The port needed to be changed to 30304 because node1 is using 30303 and we used the enode address that was generated when node1 was unlocked.  The command was successful as seen in the screenshot below:
![Unlock node2](https://github.com/Davisg1179/Blockchain-Homework-18/blob/main/images/unlock%20second%20account.png)

The PoA blockchain is now successfully mining blocks and is ready for transactions.

## Making a Transaction

With both nodes successfully running and being mined, we can now make transactions.  Using the MyCrypto app we set up a custom node and named it "blockchain."  The Chain ID was set to 787, which is what we had defined when the blockchain was set up.  We could then unlock the wallet using the Keystore File that is contained in the node1 file that we generated above.  A transaction could then be made to the node2 account from above.  In this instance, 2000 ETH was transferred, and as seen below, the transaction was successful.

![Successful Transaction](https://github.com/Davisg1179/Blockchain-Homework-18/blob/main/images/Successful%20Transaction.png)

## Conclusion

In this assignment we learned how to set up a blockchain using the PoA algorithm.  We successfully generated two node accounts, initialized them, and unlocked them for mining.  We were then able to make transactions using the MyCrypto App by setting up a custom network and then verifying that the transaction went through.