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

Great, new contract existing. Open Crypti folder in your IDE and go to dapps folder, there is **"modules/contracts"** folder, you must be interesting only in this folder right now. Open contracts folder and see there our Message contract under **Message.js** file.

What we see there?

```js
var private = {}, self = null,
	library = null, modules = null;

function Message(cb, _library) {
	self = this;
	self.type = 7
	library = _library;
	cb(null, self);
}

Message.prototype.create = function (data, trs) {
	return trs;
}

Message.prototype.calculateFee = function (trs) {
	return 0;
}

Message.prototype.verify = function (trs, sender, cb, scope) {
	setImmediate(cb, null, trs);
}

Message.prototype.getBytes = function (trs) {
	return null;
}

Message.prototype.apply = function (trs, sender, cb, scope) {
	setImmediate(cb);
}

Message.prototype.undo = function (trs, sender, cb, scope) {
	setImmediate(cb);
}

Message.prototype.applyUnconfirmed = function (trs, sender, cb, scope) {
	setImmediate(cb);
}

Message.prototype.undoUnconfirmed = function (trs, sender, cb, scope) {
	setImmediate(cb);
}

Message.prototype.ready = function (trs, sender, cb, scope) {
	setImmediate(cb);
}

Message.prototype.save = function (trs, cb) {
	setImmediate(cb);
}

Message.prototype.dbRead = function (row) {
	return null;
}

Message.prototype.normalize = function (asset, cb) {
	setImmediate(cb);
}

Message.prototype.onBind = function (_modules) {
	modules = _modules;
	modules.logic.transaction.attachAssetType(self.type, self);
}

module.exports = Message;
```

Yep, it's our contract! It's inherit of transaction, so, in Crypti, each contract is something like transaction, that can contain new data, execute new logic, etc. As we can see, in **Message.js** you can calculate fee, add new types of data in blockchain, verify that data is right, see that data is ready to apply, etc. 

In our new DApp we will send messages from user to user. It's means we need:

  * Create new fields to store message data.
  * Create api to send/recieve messages.

## Transaction creation

Ok, so, let's modificate **.create** function of dapp, it will recieve message in data, and add message to add:

```js
Message.prototype.create = function (data, trs) {
	// create transaction container
	trs.asset = {
		message: new Buffer(data.message, 'utf8').toString('hex') //save message as hex string
	};

	return trs;
}
```

Let's set fee for message sending operation, 1 XCR for example:

```js
Message.prototype.calculateFee = function (trs) {
	return 100000000;
}
```

Let's set max length of message in 160 characters, if we store data in hex, max size of hexed message is 320 characters (160*2). So, let's modificate **verify** function to check max size of message:

```js
Message.prototype.verify = function (trs, sender, cb, scope) {
	// check if message length is much more then 320 characters
	if (trs.asset.message.length > 320) {
		return setImmediate(cb, "Max length of message is 320 characters");
	}

	setImmediate(cb, null, trs);
}
```

Now we need valid signature of transaction, because we need to sign message bytes, modificate **getBytes** function to return message bytes:

```js
Message.prototype.getBytes = function (trs) {
	return new Buffer(trs.asset.message, 'hex');
}
```

Javascript is dynamic type-checking, because we need to verify that all data is good. Normalize function and our validator will help here:

```js
Message.prototype.normalize = function (asset, cb) {
	// call validator on our asset object
	library.validator.validate(asset, {
		type: "object", // it's object
		properties: {
			message: { // it's contains property message
				type: "string", // it's string
				format: "hex",  // validate to hex
				minLength: 1 // minimum length of string is 1 character
			}
		},
		required: ["message"] // message property is required and can't be missed
	}, cb);
}
```
So, we missed only few steps to close our first step, it's: read/save to database, and apply fees.

First of all, let's create database tables. All databases tables stored **blockchain.json** file, in root folder of your dapp. There is sql schemas, let's look of base sql schema:

```json
{
	"table": "table_name",
	"alias": "table_alias",
	"type": "type of content",
	"tableFields": [
		{
			"name": "name of field",
			"type": "type of field",
			"length": "length of field"
		}
	]
}
```

Let me describe each type of field:

	* table - Name of your table.
	* alias - Alias of your table, just choose t and first letter(s) of your table name.
	* type - Write "table" all time.
	* tableFields - Fields of your table.

Let's create schema for us:

```json
{
      "table": "asset_messages",
      "alias": "tm",
      "type": "table",
      "tableFields": [
	      	{
	      		"name": "message",
	      		"type": "String",
	      		"length": 320
	      	},
	      	{
	      		"name": "transactionId",
	      		"type": "String",
	      		"length": 21
		}
	]
}
```

We created table **asset_messages**, set **tm** alias for it, and create two fields:

	* message - message file to store messages data in hex. 
	* transactionId - required for all tables fields, link to transaction that contain message or other data that you created.

Now we need to save and read data from database:

```js
Message.prototype.save = function (trs, cb) {
	modules.api.sql.insert({
		table: "asset_messages",
		values: {
			transactionId: trs.id,
			message: trs.asset.message
		}
	}, cb);
}

Message.prototype.dbRead = function (row) {
	if (!row.tm_transactionId) {
		return null;
	} else {
		return {
			message: row.tm_message
		};
	}
}
```

Great! Now your message will go to blockchain and will be saved.

Now we need to process transaction fee, and all done for first step.

We have apply/applyUnconfirmed methods for it, all our transactions can be in two states - unconfirmed (when transaction sent, but still not in block), and confirmed (when transaction applied in block). Same for account balances, we have unconfirmed balance and confirmed balance. applyUnconfirmed make effect on unconfirmed balance, apply make effect on confirmed balance.

Same here for undo/undoUnconfirmed, if transaction was applied in fork, transaction must rollback. So, we need to write logic here, but it's very easy. 

```js
Message.prototype.apply = function (trs, sender, cb, scope) {
	modules.blockchain.accounts.mergeAccountAndGet({
		address: sender.address,
		balance: -trs.fee
	}, cb);
}

Message.prototype.undo = function (trs, sender, cb, scope) {
	modules.blockchain.accounts.undoMerging({
		address: sender.address,
		balance: -trs.fee
	}, cb);
}

Message.prototype.applyUnconfirmed = function (trs, sender, cb, scope) {
	if (sender.u_balance < trs.fee) {
		return setImmediate(cb, "Sender don't have enough amount");
	}

	modules.blockchain.accounts.mergeAccountAndGet({
		address: sender.address,
		u_balance: -trs.fee
	}, cb);
}

Message.prototype.undoUnconfirmed = function (trs, sender, cb, scope) {
	modules.blockchain.accounts.undoMerging({
		address: sender.address,
		u_balance: -trs.fee
	}, cb);
}
```

As you see, all is your need is check that sender really have enough balance to send transaction in **applyUnconfirmed**.

```js
if (sender.u_balance < trs.fee) {
	return setImmediate(cb, "Sender don't have enough amount");
}
```

And then we remove fee from balance of sender using modules.blockchain.accounts.mergeAccountAndGet, that get sender.address and sum to change balance in arguments. Same here for undo functions, but we use modules.blockchain.accounts.undoMerging method.

Congrats! All done! But we still need to see how our dapp work, and we need to create message transaction somewhere, etc. In nutshell, we need **API**. Let's make it.

## API

First, let's create new few methods for our Message object.

```js
Message.prototype.add = function (cb, query) {
}

Message.prototype.list = function (cb, query) {

}
```

	* **add** - this method will be api call to create new message.
	* **list** - this method will be api call to get list of your messages.

First argument of each api function is callback, second is query, it's contains request parameters. After you called "cb", it's means that you sent response. First argument of "cb" is error, second is result of api call execution. 

Let's add this methods to api routes. Open **routes.json** file in root folder of your dapp. Add this lines to the start of routes.json file.

```json
{
	"path": "/messages/add",
	"method": "put",
	"handler": "contracts.Message.add"
},
{
	"path": "/messages/list",
	"method": "get",
	"handler" : "contracts.Message.list"
},
```

So, let's start of add message method, we need this parameters from query:

	* secret - secret of sender account.
	* recipientId - id of recipient.
	* message - message to send.

Let's validate this parameters before send transaction to blockchain, we need to use our library.validator.validate function:

```js
Message.prototype.add = function (cb, query) {
	// validate query object
	library.validator.validate(query, {
		type: "object",
		properties: {
			recipientId: {
				type: "string",
				minLength: 1,
				maxLength: 21
			},
			secret: {
				type: "string",
				minLength: 1,
				maxLength: 100
			},
			message: {
				type: "string",
				minLength: 1,
				maxLength: 160
			}
		}
	}, function (err) {
		// if error exists, execute callback with error as first argument
		if (err) {
			return cb(err[0].message);
		}

		
	});
}
```

After validation passed, we need keypair, we using modules.api.crypto.keypair to generate private and public key:

```js
var keypair = modules.api.crypto.keypair(query.secret);
```

Next line, we need to get sender account:

```js
// get account
modules.blockchain.accounts.getAccount({
			publicKey: keypair.publicKey.toString('hex')
		}, function (err, account) {
			// if error happened, call cb with error argument
			if (err) {
				return cb(err);
			}
		});
```

And finally, let's send transaction to blockchain:

```js
// create new transaction
try {
	var transaction = library.modules.logic.transaction.create({
		type: self.type,
		message: query.message,
		recipientId: query.recipientId,
		sender: account,
		keypair: keypair,
	});
} catch (e) {
	// catch error if something went wrong
	return setImmediate(cb, e.toString());
}

// send transaction on processing
modules.blockchain.transactions.processUnconfirmedTransaction(transaction, cb);
```

Great, now we can just send API POST query to [http://localhost:7040/api/dapps/<dappid>/api/messages/add]([http://localhost:7040/api/dapps/<dappid>/api/messages/add])

```sh
curl -XPUT -H "Content-type: application/json" -d '{
"recipientId": "58191895912485C",
"message": "Hello, world!",
"secret": "mysecret"
}' 'http://localhost:7040/api/dapps/<dappid>/api/messages/add'
```
