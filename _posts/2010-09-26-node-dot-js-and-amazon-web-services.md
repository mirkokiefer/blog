---
layout: post
title: "Node.js and Amazon Web Services"
date: 2010-09-26 21:38
comments: true
categories: 
---
I got pretty excited about Node.js during the last day, especially after discovering that there are already a whole bunch of modules available for it:

[http://github.com/ry/node/wiki/modules](http://github.com/ry/node/wiki/modules)

I needed clients for both Amazon EC2 and the Product Advertising API so I had a closer look at Blake Mizerany’s swirl-node.
As swirl-node only supports EC2 calls I decided to code my own little module.  I thought it would be best to have a generic part every Amazon API requires and more specific parts for EC2, Product Advertising and what else I may need in the future.

After a few hours of hacking and browsing the Node.js documentation I finally got it working.

Some simple usage examples:

``` js
var aws = require("./lib/node-aws");


ec2 = aws.createEC2Client(yourAccessKeyId, yourSecretAccessKey);
ec2.call("DescribeInstances", {}, function(result) {
console.log(JSON.stringify(result));
})
```

Returns you details about your EC2 instances:

``` js
[...]
{"item":{
"instanceId":"i-acb2d1db","imageId":"ami-03765c77",
"instanceState": {"code":"80","name":"stopped"},
"privateDnsName":{},"dnsName":{},
"reason":"User initiated (2010-07-28 19:37:54 GMT)"
[...]
```

or when using the Product Advertising API:

``` js
prodAdv = aws.createProdAdvClient(yourAccessKeyId, yourSecretAccessKey, yourAssociateTag);
prodAdv.call("ItemSearch", {SearchIndex: "Books", Keywords: "Javascript"}, function(result) {
console.log(JSON.stringify(result));
})
```

In fact returns you a long list of Books with details…

Everyone who needs something similar can give it a try at github and hopefully give me feedback:

[http://github.com/livelycode/aws-lib](http://github.com/livelycode/aws-lib)