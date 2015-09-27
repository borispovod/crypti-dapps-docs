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

## Queries

You can run sql queries DApp using SQL API. API can be found [here](http://docs.crypti.me/Sql.html), in our API docs. 

We have few methods:

	* batch  -  Insert group of records into table.
	* insert - Insert one record into table.
	* remove - Remove record from table. 
	* select - Select records from tables.

All this methods allow json sql queries. JSON query it's JSON object that will be converted to SQL query. Let's overview methods detailed. To call this API just use object **modules.api.sql.methodname** - where replace method name with real name of method.

## Queries#select

Let's base **select** query object:

```js
modules.api.sql.select({
	table: "tablename",
	condition: {
		field: value
	},
	or: {},
	sort: {},
	fields: [],
	map: []
})
```

* table - Name of table run query.
* condition - Condition like equal, great then, less then, in. More description 
* sort - Sort query by provided fields.
* fields - Fields to select from query. Will return array of fields.
* map - If fields will return array of fields value, map will map this values to objects.

### Queries#select.condition

*Equal condition:*

```js
{
	condition: {
		field: value
	}
}
```

*Great then condition:*
```js
condition: {
	field: {
		$gt: value
	}
}
```

To use great then or eaul use: *$gte*

*Less then condition:*
```js
condition: {
	field: {
		$lt: value
	}
}
```

To use less then or eaul use: *$lte*

*In condition:*
```js
condition: {
	field: {
		$in: [v1, v2, v3]
	}
}
```

*Not in condition:*
```js
condition: {
	field: {
		$nin: [v1, v2, v3]
	}
}
```


*Like condition:*
```js
condition: {
	field: {
		$like: value
	}
}
```

*Null condition:*
```js
condition: {
	field: $null
}
```

*Between condition:*

```js
condition: {
	field: {
		$between: [minvalue, maxvalue]
	}
}
```

*Equal:*

```js
condition: {
	field: {
		$eq: value
	}
}
```

*Not equal:*

```js
condition: {
	field: {
		$neq: value
	}
}
```

*OR:*

```js
condition: {
	field: {
		$or: [{
			field1: value1,
			field2: value2
		}]
	}
}
```

### Queries#select.sort

```js
sort: {
	field1: -1,
	field2: 1
}
```

Equal to 

```sql
order by field1 asc, field2 desc
```
## Expression

```js
fields: [{
	expression: 'count(*)'
}]
```

## Join, union, etc

This documentation enough for start, more documentation we have in our [module](https://github.com/crypti/json-sql/tree/master/docs).
