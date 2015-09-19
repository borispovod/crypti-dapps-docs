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

