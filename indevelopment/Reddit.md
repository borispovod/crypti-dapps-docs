# Reddit DApp

In this tutorial i will show how make connections between contracts and data stored in this contracts. 
I will make "Reddit" DAapp as example. It's not full copy of Reddit, it will contain only one board with posts, 
comments, and likes.

Source code of this DApp placed here: https://github.com/crypti/RedditDapp

## Structure

I have few contracts:

 * Post.js - Contract that control Posts.
 * Comment.js - Contact that control Comments.
 * Like.js - Contract that control Likes.

In my implementation anyone can post new post to board, but he need to pay fee. Anyone can post comment for fee, and anyone can send Like. Like is gift for posted. Part of fees will go to author of post, part of fees will go to author of DApp.

So, let me show my fees example:

  * Post - 0,1 XCR going to master nodes.
  * Comment - 0,01 XCR going to master nodes.
  * Like - 0,1 XCR going to author of post, 0,0001 going to master nodes. (0,1 percent of gift).

In result authors of posts can make money on posts and master nodes can make money on their dapp.

