# Create Base DApp

Yeah, we at step, when we will little change decetralized world and make it better! Let's create first DApp using crypti-cli.

First of all we need next things:

  * GitHub repository.
  * Unique genesis block.
  
Let me example why you need it:

 * **GitHub Repository** - for store your dapp code for sure. Easy update your DApp and etc. So, go to Github.com and create some new public empty repository.
 * **Unique genesis block** - unique genesis block special for you, you will have testnet coins and use it for test/play your dapp.

So, you have github repository, let's make new genesis block and add dapp there with crypti-cli:

```sh
crypti-cli dapps -a
```

This command will ask you few questions:
```sh
? This operation need to remove old blockchain.db file and create new one, are you sure?
? Put secret of your testnet account
? Update current genesis block? (or make new one)
? Your DApp name
? Description
? Github repository
? Additional public keys of dapp forgers - hex array, use ',' for seperator
? Add dapp to autolaunch Yes
```

I will detail describe questions step by step:

 * **This operation need to remove old blockchain.db file and create new one, are you sure?** - It's means each time when you add new genesis block to your testnet, it will remove previous blockchain.db file (file, where blockchain stored).
 * **Put secret of your testnet account** - Here you need to put your secret passpharse. **Important**: don't lose your secret, or you will need to regenerate genesis block.
 * **Update current genesis block?** - It's means you can update current genesis block, and don't remove delegates, previous dapps from genesis block. **Important** for first launch say **no**.
 * **Your DApp name** - name of your dapp.
 * **Description** - description of your dapp.
 * **Github repository** - github repository of dapp, that you created in previous step. **Important** use ssh link to your repo like: git@github.com:crypti/crypti-dapps-docs.git.
 * **Additional public keys of dapp forgers - hex array, use ',' for seperator** - If you want to more forgers in your dapp (you can update forgers of dapp later), put forgers public keys like: publickey,publickey,publickey. By default there is already you public key of testnet account.
 * **Add dapp to autolaunch** - if you want to add dapp to autolaunch. I recommend to answer **yes** now.

So, i created my first dapp and get output:
```sh
? This operation need to remove old blockchain.db file and create new one, are you sure? Yes
? Put secret of your testnet account ******
? Update current genesis block? (or make new one) No
? Your DApp name test
? Description test
? Github repository <link>
Generating unique genesis block special for you...
? Additional public keys of dapp forgers - hex array, use ',' for seperator 808c2a6e3bf0a8a6edd64356e98c8aab4daeacb4dc177a8a20a6442b40d1f0e0
Creating DApp genesis block
Fetch Crypti DApp Toolkit
Connect local repository with your remote repository
Save genesis blocks
Update config
? Add dapp to autolaunch Yes
Done
```
