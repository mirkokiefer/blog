---
layout: post
title: "LivelyCouch source is available"
date: 2010-11-30 21:46
comments: true
categories: 
---
Johannes Auer and I made great progress on the LivelyCouch framework I’ve written about before.

LivelyCouch now allows you to:

store your entire Node.js web application in CouchDB, being able to replicate it
changes on your source files are automatically written to CouchDB using a filesystem watcher
use “Handlers” to write your own views in Node.js
keep server-side code decoupled in small “Workers” that communicate through Events via publish/subscribe
Thanks to Johannes’ help we added a pattern-matching mechanism to Event subscriptions, today. This gives you maximum flexibility when wiring Events and Workers together.

We are now working on some tutorials to get you started on the framework.
Adventurous developers can check out our source at Github already now:

[https://github.com/livelycode/LivelyCouch](https://github.com/livelycode/LivelyCouch)

Let us know if you have any problems – we hope to get lots of feedback!