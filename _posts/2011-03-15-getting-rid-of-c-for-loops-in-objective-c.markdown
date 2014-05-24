---
layout: post
title: "Getting rid of C for-loops in Objective-C"
date: 2011-03-15 21:48
comments: true
categories: 
---
Ever been annoyed by having to use C for-loops to do something simple like filtering or collecting objects from NSArray? Blocks finally allow you to get rid of them entirely!

As a Smalltalk lover I really had to write this simple library:

``` objective-c
[someArray forEach:^(id each) {
  // do something with each element
}];

NSArray* filteredArray = [someArray filter:^(id each) {
  return [each isEqual: aCoolObject];
}];

NSArray* collectedArray = [someArray collect: ^(id each) {
  if([each isEqual: aCoolObject]) {
    return @"cool";
  } else {
    return @"not cool";
  }
}];

[someDictionary keysAndValues: ^(id key, id value) {
  //do something with the current key and value
}];
```

Fork the source on github:

[https://github.com/mirkokiefer/LivelyBlocks](https://github.com/mirkokiefer/LivelyBlocks)