# DApps SQL API

Crypti stores blockchain data in sqlite database, same with Sidechain, it's stores sidechain data in sidechains tables, in **blockchain.db** file.
From DApp you can select/insert/del data from sidechain database.

## Schemas

To start stole your data in sidechain, you need to initialize tables. To initialize table, you need to describe table schema.
So, let's do it. Go to **blockchain.json** file in root of your DApp and see that array of objects:

```json
{
	"table": "blocks",
	"alias": "b",
	"type": "table",
	"tableFields": []
}
```

It's schema of blocks table. Let's describe properties of this schema:

  * table - Name of table.
  * alias - Alias of table. Technical field, but need to be provided. Can be first characters of table name.
  * type - Table of schema, we allow to describe in schemas tables and indexes. In our case there is type "table".
  * tableFields - List of table fields.

## Table fields.

Table fields descrbied in **tableFields** in schema, each **tableField** is object, that describe one field in table.
Let's see:

```json
{
	"name": "id",
	"type": "String",
	"length": 21
},
{
  "name": "timestamp",
  "type": "BigInt"
},
{
	"name": "height",
	"type": "BigInt"
},
	{
  "name": "payloadLength",
  "type": "BigInt"
},
	{
  "name": "payloadHash",
  "type": "String",
  "length": 32
},
{
	"name": "prevBlockId",
	"type": "String",
	"length": 21
},
{
	"name": "pointId",
	"type": "String",
	"length": 21
},
{
	"name": "pointHeight",
	"type": "BigInt"
},
{
	"name": "delegate",
	"type": "String",
	"length": 64
},
{
	"name": "signature",
	"type": "String",
	"length": 128
},
{
	"name": "count",
	"type": "BigInt"
}
```

Each object is field that content:

  * name - Name of field.
  * type - Type of field, we allow "String", "BigInt", "Binary".
  * length - Required for fields that required length, like "String" or "Binary".

We don't recommend to use "Binary", because it's increase traffic between Crypti and DApp, because just convert your Binary 
data to hex string and save it as "String", if you have 32 bytes binary buffer, convert it to hex and save to "String" with 64 chars length.

