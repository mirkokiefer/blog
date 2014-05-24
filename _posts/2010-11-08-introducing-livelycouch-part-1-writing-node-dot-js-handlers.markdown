---
layout: post
title: "Introducing LivelyCouch Part 1 – writing Node.js handlers"
date: 2010-11-08 21:42
comments: true
categories: 
---
LivelyCouch is all about making life as a CouchDB developer easier. It is designed to fill the gap between a CouchApp and a full fledged web application.
Being all written in Node.js it allows you to stick to Javascript throughout your code. We are currently working on getting the source ready to release.


LivelyCouch consists out of two major parts – LivelyHandler and the Lively Event System. They both run as Node scripts behind CouchDB using the new externals and http proxy modules which is available in CouchDB trunk by now.
In this part I will focus on how handlers work – part 2 will explain the event system a bit more.

A LivelyHandler basically allows you to do all the things you can’t do in Design Documents. That could be for example:

Chaining multiple CouchDB views
Doing requests across Databases
Combining multiple outputs of show functions
LivelyCouch makes it easy to write such handlers – here is a simple example:

``` js
exports.run = function(parameters, response, handlerLib) {
  var client = handlerLib.couchdb.createClient(5984, '127.0.0.1', 'user', 'password');
  var userDb = client.db('people');
  var hairColour = parameters.query.haircolour;
  var startAge = parameters.query.startage;
  var endAge = parameters.query.endage;

  // calling a view to get all people between 30 and 40
  userDb.view('my-design-doc', 'people-per-age', {startkey=startAge, endkey=endAge}, function(data) {
    // filtering all rows that have the specified hair colour:
    var filteredRows = data.rows.filter(function(row) {
      return row.value.haircolor == hairColour;
    });
    // writing out all filtered rows to the response:
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.write(JSON.stringify(filteredRows));
    response.end();
  })
}
```

All Handler follow this pattern – you simply export a “run” function in your Node script and LivelyCouch will call it passing it

the request parameters
a response you can write on
a handlerLib which contains useful modules like node-couchdb and mustache
To be able to execute it through a HTTP request, you simply upload the file as an attachment to a handler document in the “lively_handler” database.
The structure of such a handler document looks like the following:

``` js
{
  “id”: “your_app”,
  “_attachments”: [
    “filtered_people.js”: {...},
    “another_handler.js”: {...}
  ],
  “mapping”: {
    “/filtered_people”: “filtered_people.js”,
    “/another_path”: “another_handler.js”
  }
}
```

Through the mapping property you can define which handler binds to which URL path – all URLs are automatically prefixed with “_handler” and the name of the handler document.
So to call our filtered_people handler you would request the URL:

    http://127.0.0.1:5984/_handler/your_app/filtered_people?haircolour=blond&startage=30&endage=40
