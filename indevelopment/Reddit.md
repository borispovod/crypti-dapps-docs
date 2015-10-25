# Reddit DApp

In this tutorial i will show how make connections between contracts and data stored in this contracts. 
I will make "Reddit" DAapp as example. It's not full copy of Reddit, it will contain only one board with posts, 
comments, and likes.

Source code of this DApp placed here: https://github.com/crypti/RedditDapp

## Structure

I have few contracts:

 * **Post.js** - Contract that control Posts.
 * **Comment.js** - Contact that control Comments.
 * **Like.js** - Contract that control Likes.

In my implementation anyone can post new post to board, but he need to pay fee. Anyone can post comment for fee, and anyone can send Like. Like is gift for posted. Part of fees will go to author of post, part of fees will go to author of DApp.

So, let me show my fees example:

  * **Post** - 0,1 XCR going to master nodes.
  * **Comment** - 0,01 XCR going to master nodes.
  * **Like** - 0,1 XCR going to author of post, 0,0001 going to master nodes. (0,1 percent of gift).

In result authors of posts can make money on posts and master nodes can make money on their dapp.

## Post contract

[Here](https://github.com/crypti/RedditDapp/blob/master/modules/contracts/Post.js) is standart contact, that allow users to create posts for 0,1 XCR free (10000000) with title (100 letters max) and text (5k letters max).

To get details see previous repositories, [example](https://github.com/crypti/crypti-dapps-docs/blob/master/MessagingDapp.md).

## Comments

Comments must be linked at Post. All contacts in DApp Toolkit working inside transactions, it's means we need to get id of transaction where post was saved. 

My code is [here](https://github.com/crypti/RedditDapp/blob/master/modules/contracts/Comment.js)

Let's see details where i connect Comment and Post.

```js
Comment.prototype.create = function (data, trs) {
	trs.asset = {
		comment: {
			postId: data.postId,
			text: data.text
		}
	};

	return trs;
}
```

Here i ask for postId and text. Post id is id of transaction where Post was saved. All contracts works inside transactions, it's means each transaction have id, and you refer to this id.

Then i verify text and that's post with this id really existing:
```js
Comment.prototype.verify = function (trs, sender, cb, scope) {
	if (trs.asset.comment.text.length == 0 || trs.asset.comment.text.length > 160) {
		return setImmediate(cb, "Text must contain from 0 to 160 letters, now there is " + trs.asset.comment.text.length + " letters");
	}

	modules.api.sql.select({
		table: "transactions",
		alias: "t",
		condition: {
			id: trs.asset.comment.postId,
			type: 6
		}
	}, function (err, rows) {
		if (err || rows.length == 0) {
			return cb(err || "Post didn't found");
		}

		return cb(null, trs);
	});
}
```

It's just sql query to database transactions tables to see that post existing in blockchain and i can refer on it. More, i have in condition two fields:
```js
condition: {
	id: trs.asset.comment.postId,
	type: 6
}
```
First is id of transaction that postId refer, and type is 6, because Post contract type is 6.

Then i filled all other functions to get my Contract work, and it's all. Now it's possible to make api that will return comments by post id.

