# Layer2

## What are Layers 1 and 2?

### Layer 1
A Layer-1 blockchain (also known as the parent chain or root chain) is typically a name used to describe a main blockchain network protocol such as Ethereum or Bitcoin. Layer-1 blockchains are simply the main network that a Layer-2 scaling solution attaches to in order to improve the scalability and transaction throughput of the main chain, or Layer 1. 
The name Layer 1 comes from its relationship with Layer-2 scaling solutions such as state channels, rollups, nested blockchains, and plasma side chains, all of which we will get into in more detail.

Think of Layer 1 as the standard blockchain technology we've been studying so far, and Layer 2 as extensions built on top of that blockchain to add functionality.

### Layer 2

Layer 2 refers to a secondary framework or protocol that is built on top of an existing blockchain system. Major cryptocurrency networks such as Ethereum face transaction speed and scaling difficulties. Bitcoin and Ethereum are still not able to process thousands of transactions per second. Additionally, these layer 2 solutions usually offer much better transaction fees.

Layer 2 protocols are specifically designed to integrate with the underlying blockchain to improve the transaction throughput. They rely on the consensus mechanism and security of the main chain. Operations on layer 2 can often be performed independently of layer 1. This is why these are sometimes referred to as "off-chain" solutions. While the main chain / layer 1 can provide the security inherrent to a blockchain, layer 2 can provide the speed.

Since transactions on layer 2 are happening on a different chain, a connection is periodically opened to move these transactions onto the main blockchain. This connection is sometimes called a bridge, or a channel. Therefore, a major consideration for a layer 2 solution is how transactions are validated and confirmed before being moved to the main chain.

### Layer 2 Scaling Solutions

#### Sidechains

Sidechains are independent networks with a channel to Layer 1. A sidechain has its own validators and consensus method of adding blocks. Sidechains accumulate transactions quickly and cheaply and summarize them to the main chain via a bridge or channel.

#### State Channels

A state channel is a temporary sidechain for managing transactions between two or more users, or between users and nodes, or between users and services.

A simple example of this is a tic tac toe game on the blockchain, with betting.

Let's say Alice and Bob want to put 10 ETH down to play a game of tic tac toe. We might design a smart contract such that each move is recorded on the blockchain, and, at the end of the game, either Alice or Bob receive their winnings. But this would be an expensive game, since each move would cost either Alice or Bob gas fees. This can be solved with state channels.

Instead of designing a smart contract to support tic tac toe move by move, we design a smart contract that allows opening and closing a state channel. Once opened, the state channel will have the default start state of the game, and Alice and Bob can makes moves on it without paying gas fees, because the opened state channel will be off-chain. Every move will not be written to the main chain. When the channel is closed, the end state of the game is written to the main chain, along with processing the winnings from the game. So, instead of writing every move to the blockchain, only the start and end of the game is written to the blockchain, thereby saving massive amounts of transaction fees. The number of moves in tac tac toe might be low, but imagine a game of chess, or go, and you'll see how much money this can save.

In applications that involve money/crypto transfers, sometimes these are called payment channels.

State channels still utilize blockchain methodology such as making each state change cryptographically secure. 

In addition to potential gains to speed and lower fees, there are some other benefits to state channels. Since the beginning and end of the game is written to the main chain, but in between states are not, it's possible to have more privacy. The state channel was just between Alice and Bob, but since each move was not published to the blockchain, each move is not public.

This approach is not without its challenges as well. To open the channel, both Alice and Bob had to put down 10 ETH. That money is locked into the smart contract until the state channel is closed. However, if Alice goes offline on her move, Bob will never get his money back. Either player can lock up the smart contract.

#### Plasma chains

Like sidechains, plasma chains have their own consensus algorithm and create blocks of transactions. At a fixed interval, a compressed representation of each block is committed to a smart contract on Ethereum.

Plasma is a construction scalability method that places layer 2 blocks on top of the Ethereum blockchain in the form of a side chain. Like sidechains, plasma chains have their own consensus algorithm and create blocks of transactions. At a fixed interval, a compressed representation of each block is committed to a smart contract on Ethereum. 

The implementation of Plasma gives the ability of hundreds of side chain transactions to be processed offline with only a single hash of the side chain block being added to the Ethereum blockchain. The problem with Plasma is that for a user to withdraw from the side chain, they must retain a high amount of data so that enough exists for validation; a lengthy challenge period also requires users to stay online or lose reward.

#### Roll-ups
In short, Rollups are solutions that perform transaction execution outside Layer 1 but make transaction data available on Layer 1. By moving computation off chain, they free up more space on-chain. Onchain data availability is crucial, since it allows Ethereum to double check the integrity of rollup transactions.

#### ZK roll-ups
ZK-rollups, or Zero Knowledge rollups, are one of many Layer 2 scalability solutions and work by rolling up mass transfer processing into a single transaction. ZK roll-ups use zero-knowledge succinct non-interactive arguments of knowledge (zk-SNARKs) to validate transactions. Zk-snarks refer to a proof construction where one can provide proof of certain information, e.g. a secret key, without revealing that information itself, and without any interaction between the prover and verifier.

ZK = “Zero Knowledge”... As a "zero knowledge proof" approach is used to present and publicly record the validity of the block on the Ethereum blockchain, ZK reduces computing and storage resources for validating the block by reducing the amount of data held in a transaction; zero knowledge of the entire data is needed. 

#### Optimistic roll-ups
In optimistic rollups, batches of transaction data are posted to the main chain and presumed to be valid (optimistic) but can be challenged. Theoretically, anyone can challenge them by submitting a claim, also known as fraud proof, to prove that a batch committed to the chain contained invalid state transitions. If the fraud proof is valid, these invalid state transitions would be rolled back
The challenge with optimistic roll-ups, from a usability perspective, is that batches posted to the main chain can be disputed for several days (typically 1 week) during which funds on these Layer 2s cannot be withdrawn back to the main chain - this means Layer 2 users are not liquid.

#### Validium

Validium works very similar to ZK rollups except data is stored off-chain. Since transaction data is not published on-chain, this introduces new trust assumptions as users must trust an operator to make data available when it is needed. This is typically achieved through a committee of known entities who stake their business reputation on being reliable data providers. If an L2 node operator stops servicing withdrawal requests, this committee will make its copy of the data publicly available. 

### Examples of Layer 2

For example, [Immutable X](https://www.immutable.com) is a Layer 2 scaling solution for NFTs on Ethereum. It allows developers to build marketplaces, games, apps, and more. While Ethereum handles only about 15 transactions per second and suffers from high-gas fees, an Layer 2 solution like `Immutable X` handles 9,000 transactions per second with zero gas fees. It leverages Ethereum’s well-developed security, connections, and ecosystem to help developers.