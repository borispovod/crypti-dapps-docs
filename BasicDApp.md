# Creating a Basic DApp

Moving onto our next tutorial. Let's create our first DApp using **crypti-cli**: an automated tool for bootstrapping Crypti based decentralized applications.

#### GitHub Repository

Before we start, we first need a publicly accessible repository to store our DApp source code.

Sign up or log into your [GitHub](https://github.com/) account, and [create a new public repository](https://help.github.com/articles/create-a-repo/) using a name of your choosing.

#### Unique Genesis Block

Once we have created our GitHub repository, we can proceed to make a new unique genesis block, which we will use to test our DApp. To do so, open a command prompt and enter the following command:

```sh
crypti-cli dapps -a
```

This command will ask you a few important questions:

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

Each question is further described below:

* **This operation need to remove old blockchain.db file and create new one, are you sure?**

Answering **yes** will replace the existing blockchain.db, the file in which your DApp's blockchain resides.

* **Put secret of your testnet account**

Enter a password of your choosing. **Important**: Keep a record of your password, otherwise you will need to regenerate the genesis block.

* **Update current genesis block?**

Answering yes will retain the existing genesis block; keeping delegates and previous dapps. **Important**: Answer **no** if this is the first time you have launched **crypti-cli** for a given DApp.

* **Your DApp name**

The name of your DApp, e.g. `myFirstDApp`.

* **Description**

A brief description of your DApp's intent and purpose.

* **Github repository**

A link to the github repository of our DApp we created earlier. **Important**: Enter the SSH based link to your repository like so: `git@github.com:crypti/testdapp.git`

* **Additional public keys of dapp forgers - hex array, use ',' for seperator**

Here we list the public keys of the accounts which will forge the side chain of our DApp.  **Note**: The public key of the testnet account is added by default.

Separate each public key with a comma like so:

```
0f788d6e3a60e8dcbb237a9c479bff7f424efcabe3c8dc780c6ace7edb8547d7,67cc18ac44c28e1e0a57851901933bc001474d2daebd0d1ad9400d03ca8553ce,1114b78189a6a49bdd4c78640426e172be2f3e1e8f8d9a3cefecd683d5a9ceb2
```

* **Add DApp to autolaunch**

Answering **yes** will set your DApp to automatically launch upon starting Crypti.

#### Example

Below is an example of how to create a test DApp using **crypti-cli** with the corresponding output:

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
Done (Dapp id is 16595324874141671114)
```

Upon successful completion, the **crypti-cli** will return the DApp's unique id, in this case: **16595324874141671114**.

If you answered **Yes** to autolaunch the DApp, then you can launch it by starting Crypti, using the following command:

```sh
node app.js
```

Once Crypti has loaded, your DApp should have launched. To verify this, simply open your browser with the following link: [http://localhost:7040/api/dapps/[dappid]/hello](http://localhost:7040/api/dapps/[dappid]/hello), replacing **[dappid]** with your DApp's own unique identifier.

All done! In the next tutorial, we describe how to make a new Messaging DApp using Crypti's DApp Toolkit.
