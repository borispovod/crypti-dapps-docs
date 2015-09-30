[![Slack Status](http://slack.crypti.me/badge.svg)](http://slack.crypti.me)

# Crypti Dapps Documentation

Welcome to the Crypti Dapps documentation. Where you will find all the information needed to start developing decentralized applications on the Crypti blockchain.

## About Crypti

Crypti is a decentralized applications platform, which offers an all round solution for Node.js and JavaScript developers to deploy their own decentralized applications.

## Tutorials

* [Setting up an Environment](EnvironmentSetup.md)
* [Creating a Basic Dapp](BasicDapp.md)
* [Creating a Messaging Dapp](MessagingDapp.md)
* [Adding a User Interface](UserInterface.md)
* [Introducing the DApp Toolkit](DappToolkit.md)
* [Creating a Custom Sidechain](Sidechain.md)

## Crypti Dapps

Crypti Dapps are blockchain based applications which operate on their own custom sidechain. Allowing developers to create decentralized applications which use XCR or BTC as a dapp's internal token.

Each Dapp has its own unique private side chain which operates in synchronization with the Crypti block time and current block height.

Dapp side chains are managed by a group of up to 101 master nodes, each of which have block generation enabled specifically for an individual dapp.

The primary role of each master node is to process transactions and signify the validity of each block generated on the side chain.

The signing of blocks by a master node against a given Dapp is restricted by the Dapp owners. Whom approve individual Crypti accounts as master nodes, which then are allowed to forge on the Dapp’s side chain.

Side chain consensus is maintained among the 101 master nodes using the same Delegated Proof-of-Stake (DPOS) method used to secure the Crypti blockchain. This allows individual master nodes to collect fees from each transaction as reward for securing the Dapp's side chain.

Users can move tokens (XCR) in and out of a dapp by depositing it into the dapp and or withdrawing XCR from the dapp.

Deposits and withdrawals are special Crypti based transactions that move your XCR funds from the main Crypti blockchain to the sidechain, thus allowing its use within the dapp.

Some example use cases:

  * **Messaging Dapp** - Users send messages and pay fees for each message to dapp owner.
  * **Decentralized Exchange** - Users deposit funds into a decentralized exchange dapp and pays order fees to dapp owner.
  * **Decentralized Torrent Tracker** - Users posts new torrents files to dapp and gets XCR as "thanks" for sharing.

### Development

Crypti Dapps are written using existing web technologies:

  * Backend: **NodeJS/JavasScript**
  * Frontend: **CSS3/HTML5/JavasScript**

Therfore, developers already familiar with these technologies, will quickly find their comfort zone, and and start building decentralized applications in no time at all.

Using our Command Line Interface *crypti-cli*. Developers can easily generate a new genesis block for their dapp's sidechain, clone the **Crypti DApp Toolkit** as a base project structure and create new contracts.

For more information on how to proceed with developing your first Crypti based dapp. Please read the tutorials which are part of this documentation.

### Sandboxing

Crypti Dapps execute within an sandboxed NodeJS environment. Where 90% of all system calls are handled by [Seccomp](https://en.wikipedia.org/wiki/Seccomp).

As a result of this, you can only run master nodes in production on Linux machines. Max OS X and Windows machines are restricted to the development of dapps only.

When Crypti launches a new Dapp, it launches a new NodeJS process, secured by Seccomp which communicates with Crypti via pipes.

**NOTE:** Taking into consideration pipes often have their limitations. There is no limit on the message size.

### Forging

It is the responsibiliy of forgers to generate blocks for each sidechain. They are approved by the owner of a dapp to sign new blocks, and as a reward they receive a portion of the transaction fees.

Each genesis block contains a basic list of forgers, but this can be altered at any given point.

All operations affecting the genesis block are done using the provided command line tool: **crypti-cli**.

### Deposits/Withdrawals

When you make deposit or withdrawal to/from a dapp, a special type of transaction is used.

In the case of a deposit. This special transaction is sent from the mainchain which is then received by the dapp.

Creating another new transaction that is saved along with a new transaction id in the Dapp's sidechain. Where the funds are then allocated to the dapp user's account.

All funds deposited are stored within the Dapp owner's account. So, funds don't move from the mainchain, but instead stored wihtin the dapp owner's account.

To prevent theft of funds, there is the option of using a multi-signature account. This is highly recommended for open sourced dapps, where one or more participants are required to a sign any withdrawal requests.

When making a withdrawal from a dapp. Another special type of transaction is sent to the dapp. Once this transaction has been applied to a block, the dapp master nodes will initiate the withdrawal, which is sent to the mainchain. Where a copy of the transaction id from the sidechain is saved into the mainchain to prevent double spending attacks.

## API

The API used to communicate between a Dapp and the Crypti blockchain can be found [here](http://docs.crypti.me).

## Further Help

The Crypti Foundation is ready and waiting to answer your questions.

So feel free to join our slack group at: [slack.crypti.me](slack.crypti.me).

Thank you for making Crypti your decentralized applications platform of choice.

**The Crypti Foundation**
