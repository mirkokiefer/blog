---
layout: post
title: "Spawning a Node"
date: 2011-05-02 21:49
comments: true
categories: 
---
I just published the source of what we’ve extracted out of whats been at the core of LivelyCouch.
The result is a tiny generic library that gives you only a single function – “spawn”.

It allows you to spawn a Javascript function in a new Node.js instance and returns you an EventEmitter to communicate with it.

You can find more details on github:

[https://github.com/livelycode/spawn.js](https://github.com/livelycode/spawn.js)