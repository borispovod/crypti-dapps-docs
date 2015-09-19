## Messaging DApp

In this tutorial i will show how easy create messaging dapp based on Crypti.

In previous tutorial we made first dapp, now we can make messaging dapp, and then i will explain what we done.

Let's go to dapp folder in your terminal:

```sh
cd dapps/<dappid>/
```

Replace **<dappid>** with your dapp id. Now we need to ask crypti-cli to create new contract:

```sh
crypti-cli contract -a 
```

It will ask you few questions include contract name, let's choose "Message" for it.

```sh
? Contract file name (without .js) Message
New contract created: ./contracts/Message.js
Update list of contracts
Done
```

Great, new contract existing.
