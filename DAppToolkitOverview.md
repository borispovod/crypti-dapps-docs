# DApp Toolkit

For DApp developers we created DApp Toolkit. It's set of functional, that allow you easy, in few commands, create new sidechain, change forgers of sidechain, and start developing dapp, without care about other things.

When you add DApp via **crypti-cli** it's clone DApps Toolkit from our [repository](https://github.com/crypti/testdapp) and place in your DApp repository. 

So, i will describe DApp Toolkit in this tutorial, to follow me open our [repository](https://github.com/crypti/testdapp) or just create new DApp via **crypti-cli**.

## Structure overview

Let's open DApp Toolkit and look what there:

  * **modules** - Folder contains modules of DApp Toolkit. Hear of DApp.
  * **public** - Folder that will contain UI of your DApp.
  * **blockchain.json** - JSON file contains SQL tables schemas. You need if you want to store some new data in DApp.
  * **config.json** - JSON file contains configuration of DApp. By default there is list of base peers of DApp.
  * **genesis.json** - Contains genesis block of DApp.
  * **index.js** - Js file that start your DApp.
  * **modules.full.json** - List of modules, that will be required by **index.js**.
  * **modules.genesis.json** - Pending Paul description.
  * **routes.json** - Contains http schema for API calls that you need to update to make any new http api call.
  
Let's take much interesting files and describe it more.

### Routes.json

This file, as i wrote above, contains schemas of http api calls, let's see example:

```json
[
	{
		"path": "/",
		"method": "get",
		"handler": "system.api.helloworld"
	},
	{
		"path": "/message",
		"method": "post",
		"handler": "system.api.message"
	},
	{
		"path": "/openAccount",
		"method": "post",
		"handler": "blockchain.accounts.open"
	},
	{
		"path": "/transaction",
		"method": "put",
		"handler": "blockchain.transactions.addTransaction"
	},
	{
		"path": "/transactions",
		"method": "get",
		"handler": "blockchain.transactions.getTransactions"
	},
	{
		"path": "/blocks/get",
		"method": "get",
		"handler": "blockchain.blocks.getBlock"
	},
	{
		"path": "/blocks",
		"method": "get",
		"handler": "blockchain.blocks.getBlocks"
	},
	{
		"path": "/blocks/after",
		"method": "get",
		"handler": "blockchain.blocks.getBlocksAfter"
	},
	{
		"path": "/blocks/height",
		"method": "get",
		"handler": "blockchain.blocks.getHeight"
	},
	{
		"path": "/blocks/common",
		"method": "get",
		"handler": "blockchain.blocks.findCommon"
	},
	{
		"path": "/blocks/count",
		"method": "get",
		"handler": "blockchain.blocks.count"
	},
  	{
		"path": "/withdrawal",
		"method": "post",
		"handler": "contracts.withdrawaltransfer.withdrawal"
	}
]
```

It's json array, that contains objects, each object it's path to any api. Let's see path object:

```json
{
	"path": "/",
	"method": "get",
	"handler": "system.api.helloworld"
}
```

  * **path** - Path of url to call api. Like '/', '/some/call'.
  * **method** - Method of http request to call api, like: GET, POST, PUT, DEL. (Yeah, we support restfull api).
  * **handler** - Method of object, that handle api call.

### Config.json

This is config file, right now there is only array of peers, but you can add additional parameters:

```json
{
	"peers": [
	]
}
```

To get access to config object from Crypti use this object:
```js
library.config
```

## Genesis.json

It's file contains your genesis block in json. We don't recommend to touch this file, modificate it only via **crypti-cli**.

### Blockchain.json

File contains SQL schemas. Read more in messaging dapp [tutorial]( https://github.com/crypti/crypti-dapps-docs/blob/master/MessagingDapp.md).

### Modules

So, let's go to modules folder and overview content there.

  * **api** - API that allow you to communicate with Crypti from VM.
  * **blockchain** - Sidechain logic, include accounts, blocks, loader, dapp forgers, transaction work, etc.
  * **contracts** - Place where developers can add new transactions and run it under new logic.
  * **helpers** - Some helpers of code.
  * **logic** - Some additional logic for blocks and transactions.
  * **system** - Some system helpers. 

All modules start work after onBind will be called, before - we don't recommend to do anything. Work with **blockchain** must be started only when **onBlockchainLoaded** happened. 

If you don't want to go deep, 90% of time you will spent in contracts folder. Little later we will provide full documentation about modules, and how it works.

## Event Emitter

DApp Toolkit have event emitter, you can send event via:

```js
library.bus.message("event", {});
```

You can call it in any place. Each module can catch event, just add to module object next code:

```js
MyModule.prototype.onEvent = function (args) {
}
```

Where **onEvent** is name "on" + name of event.
