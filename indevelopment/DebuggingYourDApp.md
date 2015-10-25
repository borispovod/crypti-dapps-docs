# Debugging Your DApp

Required:

  * [Crypti Sandbox](https://www.npmjs.com/package/crypti-sandbox) - version **1.0.3**.

**Important**: If you had installed Crypti Sandbox module before (see in node_modules/crypti-sandbox), check version,
it's must be great or equal 1.0.3. If you have older version of Crypti sandbox, run next commands: 

```sh
rm -rf node_modules/crypti-sandbox
npm install crypti-sandbox
```

To debug your dapp your need to run Crypti node with your DApp via next command:

```sh
DEBUG=1 node app.js
```

## Debug via Node-inspector

Install [node-inspector](https://github.com/node-inspector/node-inspector)

```sh
npm install -g node-inspector
```

Launch app:
```sh
DEBUG=1 node app.js
```

Launch node-inspector:
```sh
node-inspector
```

## Debug via Webstorm

Click on:

```
Run->Edit Configurations->Nodejs Remote Debug
```

Add new configuration for debug, settings are default.

Then launch app:
```sh
DEBUG=1 node app.js
```

And then launch remote debugger for webstorm.
