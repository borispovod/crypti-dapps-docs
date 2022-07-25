# Crypti Dapps Documentation

Welcome to the Crypti Dapps documentation. Where you will find all the information needed to start developing decentralized applications on the Crypti blockchain.

## About Crypti

Crypti is a decentralized application platform and crypto-currency, which offers an all round solution for Node.js and JavaScript developers to deploy their own decentralized applications (dapps).

## Crypti Dapps

Crypti Dapps are blockchain based applications which operate on their own custom sidechain. Allowing developers to create decentralized applications which use XCR or BTC as an internal currency / token.

Each Dapp has its own unique private side chain which operates in synchronization with the Crypti block time and current block height.

Dapp side chains are managed by a group of up to 101 master nodes, each of which have block generation enabled specifically for an individual dapp.

The primary role of each master node is to process transactions and signify the validity of each block generated on the side chain.

The signing of blocks by a master node against a given Dapp is restricted by the Dapp owners. Whom approve individual Crypti accounts as master nodes, which then are allowed to forge on the Dapp’s side chain.

Side chain consensus is maintained among the 101 master nodes using the same Delegated Proof-of-Stake (DPOS) method used to secure the Crypti blockchain. This allows individual master nodes to collect fees from each transaction as reward for securing the Dapp's side chain.

Users can move tokens (XCR or BTC) in and out of a dapp by making deposits or withdrawals to and from each dapp.

Deposits and withdrawals are special Crypti based transactions that move your XCR funds from the main Crypti maincain to the sidechain, thus allowing its use within the dapp.

Some example use cases:

  * **Messaging Dapp** - Users send messages via a messaging dapp and pay transaction fees for each message sent to the dapp owner.
  * **Decentralized Exchange** - Users deposit funds into a decentralized exchange dapp and pay order fees to the dapp owner.
  * **Decentralized Torrent Tracker** - Users post new torrents files to a torrent tracking dapp and receive XCR as "thanks" for sharing the file.

## Development

Crypti Dapps are written using existing web technologies:

  * Backend: **NodeJS/JavasScript**
  * Frontend: **CSS3/HTML5/JavasScript**

Developers already familiar with these technologies, will quickly find their comfort zone, and can start building decentralized applications in very little time at all.

Using the provided command line interface: **crypti-cli**. Developers can easily generate a new genesis block for their dapp's sidechain, clone the **Crypti Dapp Toolkit** as a base project structure and create new contracts.

If you are just starting out, then before progressing any further. We strongly suggest learning the basics of the [JavaScript](http://www.w3schools.com/js/default.asp) , [CSS](https://www.scaler.com/topics/css/) programming language and [NodeJS](https://nodejs.org/) runtime.

## Tutorials

For more information on how to proceed with developing your first Crypti based dapp. Please read the following tutorials:

* [Setting up an Environment](EnvironmentSetup.md)
* [Creating a Basic Dapp](BasicDapp.md)
* [Creating a Messaging Dapp](MessagingDapp.md)
* [Adding a User Interface](UserInterface.md)
* [Introducing the Dapp Toolkit](DappToolkit.md)
* [Creating a Custom Sidechain](Sidechain.md)
* [Creating a Reddit Dapp](RedditDapp.md)
* [Debugging Dapps](DebuggingDapps.md)

## Sandboxing

Crypti Dapps execute within an sandboxed NodeJS environment. Where 90% of all system calls are handled by [Seccomp](https://en.wikipedia.org/wiki/Seccomp). An application sandboxing mechanism located in the Linux kernel.

As a result of this, you can only run master nodes in production on Linux machines. Mac OS X and Windows machines are restricted to the development of dapps only.

When Crypti launches a new Dapp, it launches a NodeJS sandboxed process which communicates with Crypti via a [Named Pipe](https://en.wikipedia.org/wiki/Named_pipe). Which consequently, provides a safe execution environment for dapps to operate within.

**NOTE:** Taking into consideration how named pipes have their known limitations. We have made signifcant efforts to ensure no limit is imposed on the message size.

## Determinism

In order for a Crypti sidechain to function correctly, all contracts pertaining to the dapp must behave deterministically. Meaning if a contract is given some particular input, it should always produce the exact same output.

Therefore, when developing new contracts, please take note of the following rules:

* Contracts must always return the exact same result on all nodes.
* Do not use non-deterministic functions such as: Math.random(), which in this case returns a random number.
* All contract logic must exist inside a contract module and follow the DApp Toolkit guidelines.
* Any new data added to the sidechain must be broadcast to all nodes.

If the above rules are not adhered to, the sidechain will most likely fork, and fail to achieve consensus. By adhering to the above rules, it will reduce the likelihood of any forking of the sidechain, and therefore ensure consensus is reliably agreed upon by all nodes on the network.

## Forgers

It is the responsibility of forgers to sign blocks for each sidechain.

Forgers are approved by the owner of a dapp and each receive a portion of the transaction fees as a reward for securing the sidechain.

Each genesis block contains a basic list of forgers, but this can be altered at any given point.

All operations affecting the genesis block are done using the provided command line tool: **crypti-cli**.

## Deposits/Withdrawals

When making deposits or withdrawals between a dapp and the Crypti mainchain. A special type of transaction is used.

In the case of a deposit, this special transaction is broadcast from the mainchain to the dapp's side chain. Wherein a new transaction, along with a reference to the mainchain's transaction id, is saved to dapp's sidechain, preventing double spending attacks.

**NOTE:** All funds deposited to a dapp reside within the Dapp owner's account.

To prevent any theft of these funds, Crypti provides the option of using a multi-signature dapp account. Which for open sourced dapps is highly recommended, as it requires all signees to a sign any withdrawal requests before they can be authorized.

When making a withdrawal from a dapp. Another special type of transaction is broadcast from the mainchain to the dapp's sidechain. Once this transaction has been applied to a block, the dapp master nodes will initiate the withdrawal. Wherein a copy of the transaction id from the sidechain is saved into the mainchain, preventing double spending attacks.

## API Reference

Crypti Dapps interact with the main Crypti blockchain using an easy to use API.

A detailed reference of this API can be found in our [Crypti Dapps API Documentation](http://docs.crypti.me).

## Further Help

The Crypti Foundation is ready and waiting to answer your questions.

Please feel free to join our chat at: [Crypti.Chat](https://crypti.chat), where you will find us ready and waiting to answer any questions you may need answered as quickly as possible.

Thank you for making Crypti your decentralized application platform of choice.

**The Crypti Foundation**
