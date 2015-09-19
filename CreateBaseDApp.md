# Create Base DApp

Yeah, we at step, when we will little change decetralized world and make it better! Let's create first DApp using crypti-cli.

First of all we need next things:

  * GitHub repository.
  * Unique genesis block.
  
Let me example why you need it:

**GitHub Repository** - for store your dapp code for sure. Easy update your DApp and etc. So, go to Github.com and create some new public empty repository.

**Unique genesis block** - unique genesis block special for you, you will have testnet coins and use it for test/play your dapp.

So, you have github repository, let's make new genesis block and add dapp there with crypti-cli:

```sh
crypti-cli dapps -a
```

This command will ask you few questions and output will looks like:
```sh
? This operation need to remove old blockchain.db file and create new one, are you sure? Yes
? Put secret of your testnet account ******
? Update current genesis block? (or make new one) No
? Your DApp name test
? Description test
? Github repository git@github.com:crypti/testdapp.git
Generating unique genesis block special for you...
? Additional public keys of dapp forgers - hex array, use ',' for seperator 808c2a6e3bf0a8a6edd64356e98c8aab4daeacb4dc177a8a20a6442b40d1f0e0
Creating DApp genesis block
Fetch Crypti DApp Toolkit
Connect local repository with your remote repository
<installation logs>
Save genesis blocks
Update config
? Add dapp to autolaunch Yes
Done
```
