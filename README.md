# Proof of Authority Blockchain

The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions (seal blocks).


1. Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as our pre-approved sealer addresses.

- Create accounts for two nodes for the network with a separate datadir for each using geth.

    - ./geth --datadir node1 account new
    - ./geth --datadir node2 account new


2. Next, generate your genesis block.


- Run puppeth, name your network, and select the option to configure a new genesis block.


- Choose the Clique (Proof of Authority) consensus algorithm.


- Paste both account addresses from the first step one at a time into the list of accounts to seal.


- Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.


- You can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.


- Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.


- Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.




3. With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

- Using geth, initialize each node with the new networkname.json.

    - ./geth --datadir node1 init networkname.json
    - ./geth --datadir node2 init networkname.json


4. Now the nodes can be used to begin mining blocks.

- Run the nodes in separate terminal windows with the commands:

    - ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
    - ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock


5. Your private PoA blockchain should now be running!


6. With both nodes up and running, the blockchain can be added to MyCrypto for testing.

    - Open the MyCrypto app, then click Change Network at the bottom left:

# MyCrypto Desktop App Instructions

First, you will need to get the private key of your pre-funded address and keep it handy for later.

- Open up MyCrypto to get the private key of the ETH address you use to pre-fund your chain. Be sure the Kovan network is selected.

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/verify-kovan.gif?raw=true)

- Unlock your wallet using your mnemonic phrase and choose the address you want to inspect.


- Select the ETH address you use to pre-fund your chain, and in the "Select" dropdown list, choose Wallet Info.


- Click on the eye icon next to the Private Key field, and copy and paste the private key of the wallet. Keep this handy, as you will use it in a bit.


![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/get-private-key.gif?raw=true)

Now you are going to connect MyCrypto with the blockchain you created. Follow the next steps.

- Open up MyCrypto, then click Change Network at the bottom left:

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/change-network.png?raw=true)

- Click "Add Custom Node", then add the custom network information that you set in the genesis.


- Make sure that you scroll down to choose Custom in the "Network" column to reveal more options like Chain ID:

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/custom-network.png?raw=true)

- The chain ID must match what you came up with earlier.


- he URL is pointing to the default RPC port on your local machine. Use http://127.0.0.1:8545.


- Once you save and use the network, double-check that it is selected and is connected.


Now that you are connected to your blockchain, you will need to load a private key that you created and funded on the network.

- If you are logged in to another wallet, you'll need to click Change Wallet on the top right, but make sure you are connected to your custom network:

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/mycrypto-switch-wallet.png?raw=true)

- On the left pane menu, click on "View & Send".


- Next, click on the "Private Key" option to continue.

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/open-wallet-1.png?raw=true)

- A new window will pop-up, paste the private key of the pre-fund wallet and click on the "Unlock" button to continue.

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/open-wallet-2.png?raw=true)

- Looks like we're filthy rich! This is the balance that was pre-funded for this account in the genesis configuration; however, these millions of ETH tokens are just for testing purposes.

![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/prefunded-account.png?raw=true)

Now we're going to send a transaction to ourselves to test it out. Follow the next steps.

- Copy the pre-fund address into the "To Address" field, then fill in an arbitrary amount of ETH:


![picture](https://github.com/amanafzali/bootcamp_blockchain/blob/main/Images/send-transaction.gif?raw=true)

- Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.


# Blockchain Terminology Guide

*What is a blockchain?*

Answer: A blockchain is a network of nodes or machines linked in a peer-to-peer fashion that facilitates transactions in a verifiable and permanent way. A blockchain network is also often called an open distributed ledger.

*What is a blockchain node?*

Answer: A node is a single machine that contributes to the infrastructure of a blockchain network. Blockchains networks as a whole are composed of multiple nodes that are interconnected with each other and therefore exchange the latest blockchain data with each other so that each node is up-to-date with the latest verified transactions on the blockchain network.

*What is blockchain mining?*

Answer: Blockchain mining is the process of adding verified transaction records to the current blockchain data; miners act as separate nodes that are paid a fee to verify blockchain transactions and do so by solving intense computations to finalize transactions.

*What is a blockchain wallet?*

Answer: A blockchain wallet is a digital wallet containing a public and private key that is used to not only store cryptocurrencies, but also conduct secure transactions amongst other users via wallet addresses (hashed version of a public key). It is imperative that the private key for a digital wallet be kept safe, as losing it will be prevent a user from accessing their funds (no other way for decryption).

*What is Ethereum?*

Answer: Ethereum is an open software platform based on blockchain technology that enables developers to build and deploy decentralized applications.

*What is a hash?*

Answer: A hash value is a product of a function that converts an input of letters and numbers into an encrypted output of a fixed length. Hashing is one way to enable security during message transmission when the message is intended for a particular recipient only, ensuring that the message has not been tampered with, as doing so would generate a new hash value different from the originating hash value.

*What is a digital signature?*

Answer: A digital signature is a numerical value that is represented as a sequence of characters and is the product of ensuring the contents of a message have not been altered in transit (integrity), that the message was indeed sent by the sender (authentication), and that the sender cannot deny having sent the message (non-repudiation).

*What is encryption?*

Answer: Encryption is the process in which a message is encoded in a format that cannot be read or understood by an external party lacking the necessary credentials.

*What is symmetric encryption?*

Answer: Symmetric encryption is the simplest type of encryption that uses only a single key (a private/secret key) to both encrypt and decrypt information. As a result, the parties communicating via symmetric encryption must exchange the secret key so that it can be used in the decryption process, which is a security disadvantage compared to asymmetric encryption.

*What is an asymmetric key?*

Answer: Asymmetric encryption uses a key pair: a public and private key. As the name suggests, the public key is made freely available to anyone on the Internet while the private key is kept a secret by the end-user. Therefore, messages that are encrypted using the public key can only be decrypted using the associated private key, and messages that are encrypted using the private key can only be decrypted using the associated public key.

*What are the advantages vs. disadvantages of both types of encryption techniques?*

Answer: Symmetric encryption is the oldest and best-known technique for encryption; however, because of its use of only a single key (the private/secret key), there is the potential for a breach in security when exchanging the private key between two parties, especially over a vast network such as the Internet with possible eavesdroppers. In contrast, due to the use of a key pair in asymmetric encryption (public and private key), the private key is never exchanged and therefore is kept a secret at all times. Though as a result of the use of a key pair, asymmetric encryption is slower than symmetric encryption due to the increased processing power used to encrypt and decrypt messages.

*What is a consensus algorithm?*

Answer: A consensus algorithm is a protocol used to verify the validity of transactions on a blockchain network. Due to the decentralized nature of the blockchain network, there is no central authority and therefore nodes within the blockchain network must be able to verify such transactions with certainty.

*What is proof of authority?*

Answer: Proof of Authority (PoA) is a reputation-based consensus algorithm in which the model relies on a limited number of block validators that act as moderators to verify the newest blocks and transactions.

*What is proof of work?*

Answer: Proof of Work (PoW) is an asset-based consensus algorithm in which the model relies on producing a piece of data which is both resource (computation) and time intensive, but allows for others to verify the validity of the transaction. This consensus algorithm directly relates to the blockchain mining concept in which miners solve intense computations to finalize transactions.

*What is proof of stake?*

Answer: Proof of Stake (PoS) is an collateral-based consensus algorithm in which the model relies on transactional validators whom are selected based on the amount of Bitcoin or Ether they hold. When they validate transactions, they put up a stake of their own Bitcoin or Ether and are rewarded (proportional to their stake) when a new block or transaction is added to the blockchain.