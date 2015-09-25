# DApps UI

In root folder of your DApp you can find public folders, there must be stored DApps UI. Crypti support [Single-Page Applications](https://en.wikipedia.org/wiki/Single-page_application) as UI.

It's means UI in DApps, it's standart single-page application that can be developed with any single-page framework.

I don't want to provide full tutorial, just because UI it's mate of test, i will just describe how to right call api from javascript, other base things, etc.

## How to start make UI?

Just add **index.html** file to public folder, and start work on it, like you work on any site. 

When you will go to:
[http://localhost:7040/dapps/<dappid>/](http://localhost:7040/dapps/<dappid>/) - it will open **index.html** from public folder. You can make **css**, **js** folder there (or call it how you want), and require it from **index.html**, and then use it. 

Crypti DApps UI support only single pages applications, it's means you can create **hello.html* and render it from backend of DApp. You work only with DApp API from javascript.

## How to make an API call.

There is a lot of examples how to make Ajax api call from single page application. I will note only that base url of api call is: **/dapps/api/<dappid>/api/<yourapicallpath>**

Where:
  * dappid - Id of your dapp.
  * yourapicallpath - Path of your api call, that you provided in routes.json

Here is one problem, how to get dappid? Very easy, any dapp ui opened by link like it:

**http://localhost:7040/dapps/<dappid>/**

So, we can get dappid yes from url, i will show example how to do it on [Angularjs](http://angularjs.org):

```js
var url = $location.absUrl();
var parts = url.split('/');
var dappId = parts[parts.indexOf('dapps') + 1];
return dappId;
```

## Can i use less/sass in UI?

Yes, just prepare builder for less/sass using Grunt or something another, and build your less/sass to css, then place it to public folder. All easy! :)

## Still have any questions?

Join our slack: slack.crypti.me , we are there and ready to help you!
