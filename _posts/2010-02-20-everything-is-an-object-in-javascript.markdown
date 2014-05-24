---
layout: post
title: "Everything is an Object in Javascript"
date: 2010-02-20 21:35
comments: true
categories: 
---
Most developers have heard about “object orientation” and many believe it has something to do with what are called “classes”, “instances” and “class/instance methods” in Java or C++. In fact true object orientation has very little to do with these features – at least not in the sense the original “inventors” have seen this concept.

But more on this in a later post.

For now I just want to share what I have learned about Javascript’s approach to OOP today. In Javascript essentially everything is an Object.

Javascript doesn’t have “classes”, it is a prototype-based language which means objects are created by cloning other objects:

``` js
var myNewObject = new Object();
```

Now, I can do whatever I want with this cloned object – for example I can give it new properties:

``` js
myNewObject.colour = ‘blue’;
myNewObject.anotherFancyAttribute = ‘blablub’;
```

You can also create functions:

``` js
function doSomething() { … };
```

This looks like functions are something different to objects – just like methods in Java are different to objects. But actually “functions” are just objects, too. In fact the function declaration above is just a shortcut for:

``` js
var doSomething = function() {…};
```

I can even add this function-object as a property to my object above:

``` js
myNewObject.doSomething = doSomething;
```

...and essentially get whats called a “method” in Java – I can invoke this function on the object and it will evaluate within the myNewObject context.

Realizing this everything-is-an-object concept is of great value if you want to do more advanced programming in Javascript. For me being in love with Smalltalk and having learned to appreciate the simplicity of a pure object language it is quite motivating to realize that Javascript isn’t as ugly as many tell you...