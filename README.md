# Layer2

## What are Layers 1 and 2?

### Layer 1
A Layer-1 blockchain (also known as the parent chain or root chain) is typically a name used to describe a main blockchain network protocol such as Ethereum or Bitcoin. Layer-1 blockchains are simply the main network that a Layer-2 scaling solution attaches to in order to improve the scalability and transaction throughput of the main chain, or Layer 1. The name Layer 1 comes from its relationship with Layer-2 scaling solutions such as state channels, rollups, and plasma side chains, all of which we will get into in more detail.

Think of Layer 1 as the standard blockchain technology we've been studying so far, and Layer 2 as extensions built on top of that blockchain to add functionality.

### Layer 2

Layer 2 refers to a secondary framework or protocol that is built on top of an existing blockchain system. Major cryptocurrency networks such as Ethereum face transaction speed and scaling difficulties. Bitcoin and Ethereum are still not able to process thousands of transactions per second. Additionally, these layer 2 solutions usually offer much better transaction fees.

Layer 2 protocols are specifically designed to integrate with the underlying blockchain to improve the transaction throughput. They rely on the consensus mechanism and security of the main chain. Operations on layer 2 can often be performed independently of layer 1. This is why these are sometimes referred to as "off-chain" solutions. While the main chain / layer 1 can provide the security inherrent to a blockchain, layer 2 can provide the speed.

Since transactions on layer 2 are happening on a different chain, a connection is periodically opened to move these transactions onto the main blockchain. This connection is sometimes called a bridge, or a channel. Therefore, a major consideration for a layer 2 solution is how transactions are validated and confirmed before being moved to the main chain.

## Layer 2 Scaling Solutions

### Sidechains

A sidechain is an independent EVM-compatible blockchain which runs in parallel to Mainnet, and has a channel to Layer 1. A sidechain has its own validators and consensus method of adding blocks. Sidechains accumulate transactions quickly and cheaply and summarize them to the main chain via a bridge or channel.

Since side chains are based on the EVM, you can think of them as mini ethereum blockchains. Sidechains come with all the benefits of an EVM, just as writing smart contracts in solidity, and interact with the chain using web3 APIs.

The drawbacks of sidechains are that they can be less centralized. For example, if their consensus protocol uses proof or authority and those nodes collude to commit fraud.

Important to note that, unlike other solutions below, sidechains are technically not layer 2 because they do not use the security of the main chain.

#### Further Reading
[Sidechains on ethereum.org](https://ethereum.org/en/developers/docs/scaling/sidechains)

### State Channels

A state channel is a temporary sidechain for managing transactions between two or more users, or between users and nodes, or between users and services.

A simple example of this is a tic tac toe game on the blockchain, with betting.

Let's say Alice and Bob want to put 10 ETH down to play a game of tic tac toe. We might design a smart contract such that each move is recorded on the blockchain, and, at the end of the game, either Alice or Bob receive their winnings. But this would be an expensive game, since each move would cost either Alice or Bob gas fees. This can be solved with state channels.

Instead of designing a smart contract to support tic tac toe move by move, we design a smart contract that allows opening and closing a state channel. Once opened, the state channel will have the default start state of the game, and Alice and Bob can makes moves on it without paying gas fees, because the opened state channel will be off-chain. Every move will not be written to the main chain. When the channel is closed, the end state of the game is written to the main chain, along with processing the winnings from the game. So, instead of writing every move to the blockchain, only the start and end of the game is written to the blockchain, thereby saving massive amounts of transaction fees. The number of moves in tac tac toe might be low, but imagine a game of chess, or go, and you'll see how much money this can save.

In applications that involve money/crypto transfers, sometimes these are called payment channels.

State channels still utilize blockchain methodology such as making each state change cryptographically secure. 

In addition to potential gains to speed and lower fees, there are some other benefits to state channels. Since the beginning and end of the game is written to the main chain, but in between states are not, it's possible to have more privacy. The state channel was just between Alice and Bob, but since each move was not published to the blockchain, each move is not public.

This approach is not without its challenges as well. To open the channel, both Alice and Bob had to put down 10 ETH. That money is locked into the smart contract until the state channel is closed. However, if Alice goes offline on her move, Bob will never get his money back. Either player can lock up the smart contract.

[State Channels on ethereum.org](https://ethereum.org/en/developers/docs/scaling/state-channels)

### Plasma Chains

A plasma chain is a separate, child blockchain that is anchored to the main Ethereum chain. Plasma chains use various fraud proofs to arbitrate disputes. Like sidechains, plasma chains have their own consensus algorithm and create blocks of transactions. At a fixed interval, a compressed representation of each block is committed to a smart contract on Ethereum. [Merkle trees](https://en.wikipedia.org/wiki/Merkle_tree) enable creation of a limitless stack of these chains that can work to offload bandwidth from the parent chains (including Mainnet).

The implementation of Plasma gives the ability of hundreds of side chain transactions to be processed offline with only a single hash of the side chain block being added to the Ethereum blockchain.

One of the big downsides with plasma networks is that it's more difficult to withdraw assets from it to the main chain. Withdrawals are delayed by several days to allow for challenges. For fungible assets this can be mitigated by liquidity providers, but there is an associated capital cost. This is because assets on plasma networks are not exactly the same as the assets on the main chain. For example, you do not hold ETH on plasma, you usually hold wETH (wrapped ETH), which has a 1:1 value to ETH.

Need to periodically watch the network (liveness requirement) or delegate this responsibility to someone else to ensure the security of your funds.
Relies on one or more operators to store data and serve it upon request.


The problem with Plasma is that for a user to withdraw from the side chain, they must retain a high amount of data so that enough exists for validation; a lengthy challenge period also requires users to stay online or lose reward.

As with sidechain, the benefts of plasma are higher throughput and lower cost per transaction. It's excellent for transactions between two users. However, the downsides of plasma are that it does not support computation as complex as the main chain allows.

To use Plasma, you can integrate one of several projects that have implemented Plasma, for example [Polygon](https://polygon.technology), which was formally called Matic.

### Rollups

Rollups are solutions that perform transaction execution on Layer 2 but post transaction data onto Layer 1. By moving computation off chain, they free up more space on-chain. Onchain data availability is crucial, since it allows Ethereum to double check the integrity of rollup transactions.

Rollups work by deploying a set of smart contracts on Layer 1 that are responsible for deposits, withdraws, and verifying proofs. Proofs are the main distinction between different types of rollsup. In general, there are two kinds of rollups: ZK Rollups and Optimistic Rollups.

#### Optimistic Rollups

In optimistic rollups, batches of transaction data are posted to the main chain and presumed to be valid (hence the name optimistic) but can be challenged by other users. Theoretically, anyone can challenge them by submitting a claim, also known as fraud proof, to prove that a batch committed to the chain contained invalid state transitions. If the fraud proof is valid, these invalid state transitions would be rolled back. If nobody challenges the transaction, it will be committed to the main chain. To give users enough time to challenge transactions, there is a long wait time between a transaction being posted to it being committed on the main chain, typicall a few days but as long as a week. During this time, you cannot withdraw your funds to the main chain.

It's important to note that when a challenge happens, the main chain can always verify the authenticity of transactions in the potential block. But these verifications take work and therefore fees.

What's to stop bad actors from spamming a rollup network with bad transactions, or from spamming the network with fraud proof verifications? And where does the money come from for Layer 1 to verify transactions if challenged? To answer this question, we introduce 3 players in this space:

Asserter: proposes to add a block of transactions to the main chain.
Challenger: asserts that a particular block of transcations from a certain `Asserter` is fraudulent.
Verifier: a smart contract on the main chain that verifies that a given block of transactions is valid.

An `asserter` has to provide a bond to propose a block of transactions, usually in the form of some ETH.
A `challenger` also has to provide a bond (usually ETH) to make a challenge.
The `verifier` will verify the transaction(s) on the main chain.

If the `asserter` is found to be fraudulent, they lose their entire bond. The `verifier` gets half of their bond for processing the verification, and the `challenger` gets the other half as a reward for finding the fraud.

If the `asserter` is found to **NOT** be fraudulent, the `challenger` loses their entire bond. The `verifier` gets half of their bond for processing the verification as before, and this time the `asserter` gets the other half as a reward for their trouble.

#### ZK Rollups

ZK stands for "Zero Knowledge" and it's a method by which one party (the prover) can prove to another party (the verifier) that a given statement is true while the prover avoids conveying any additional information apart from the fact that the statement is indeed true. More on [Zero Knowledge Proofs](https://en.wikipedia.org/wiki/Zero-knowledge_proof).

In this rollup, there are no individuals doing the verification. Instead, everyone who proposes a new set of rolled up transactions to be added to the main chain constructs a zero knowledge proof for it. This can be automatically verified by the smart contract that controls adding transactions to the main chain. In particular, the proposer constructs a certain kind of zero knowledge proof, called a [zk-SNARK](https://en.wikipedia.org/wiki/Non-interactive_zero-knowledge_proof), which is a `non-interactive zero knowledge proof`, meaning that this proof requires no interaction between the prover and the verifier.

#### ZK vs Optimistic

At first glance, ZK rollups seem better in every way than optimistic rollups. After all, transactions can be verified automatically, without the need for challengers, and the asserters prove their own transactions before submitting them. Furthermore they pay gas to process the proof in the smart contract so only they lose if they submit an improver proof.

So, why have optimistic rollups at all?

The problem with ZK rollups is that it is difficult to construct these proofs, mathematically speaking. Every use case requires research time to find a matching cryptographic proof, which can take a long time to find.

Furthermore, ZK proofs are often complex and therefore expensive to verify. The more operations the smart contract contains, the more expensive it is to run. In addition, smart contracts are also limited in space, so the proof must run in less than a certain number of operations.

Finally, some existing smart contracts on the main chain are impossible to find ZK proofs for. Optimistic rollsups, on the other hand, can support 99% of all smart contracts on the main chain.

#### Validium

Validium works very similar to ZK rollups except data is stored off-chain. Since transaction data is not published on-chain, this introduces new trust assumptions as users must trust an operator to make data available when it is needed. This is typically achieved through a committee of known entities who stake their business reputation on being reliable data providers. If an L2 node operator stops servicing withdrawal requests, this committee will make its copy of the data publicly available.

[Validium on ethereum.org](https://ethereum.org/en/developers/docs/scaling/validium)

### Examples of Layer 2

#### Immutabe X
[Immutable X](https://www.immutable.com) is a Layer 2 scaling solution for NFTs on Ethereum. It allows developers to build marketplaces, games, apps, and more. While Ethereum handles only about 15 transactions per second and suffers from high-gas fees, an Layer 2 solution like `Immutable X` handles 9,000 transactions per second with zero gas fees. It leverages Ethereum’s well-developed security, connections, and ecosystem to help developers.

#### Polygon (formerly Matic)
(Polygon)[https://polygon.technology] is a protocol and a framework for building and connecting Ethereum-compatible blockchain networks. Aggregating scalable solutions on Ethereum supporting a multi-chain Ethereum ecosystem.

### Required Readings

[Plasma Docs](https://ethereum.org/en/developers/docs/scaling/plasma)
[Merkle Trees](https://en.wikipedia.org/wiki/Merkle_tree)
[Learn Plasma](https://www.learnplasma.org/en/)

### Must Watch

[Ethereum Layer 2 Scaling Explained](https://youtu.be/BgCgauWVTs0)
[Rollsup Explained](https://youtu.be/7pWxCklcNsU)

### Recommended Readings
