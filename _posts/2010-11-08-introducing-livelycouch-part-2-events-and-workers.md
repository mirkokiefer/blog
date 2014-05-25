---
layout: post
title: "Introducing LivelyCouch Part 2 – Events and Workers"
date: 2010-11-08 21:44
comments: true
categories: 
---
The LivelyCouch Event System can be used in your apps whenever you want to trigger some code that should run in the background. This could for example be:

- sending out e-mails
- resizing images
- watching a database for changes
- triggering an action every minute

The only means of communication in the Event System are HTTP messages.
You start with defining LivelyEvents as documents in an events database that listen to certain HTTP messages. Each Event document in turn defines which pieces of code should be executed when they are triggered.
These pieces of code are managed in so called LivelyWorkers. Workers reside as documents in their own database – similar to Handlers they store their code in the form of attachments.

Lets look at a sample Event document that triggers a Worker to send out e-mails:

``` js
{
   "_id": "email_event",
   "trigger": {
       "/send_email": {
           "method": "GET"
       }
   },
   "workers": {
       "send_email": {
           "recipient": "support@yourcompany.com",
       }
   }
}
```

This event would be triggered by a request of the form:

    http://127.0.0.1:5984/_events/email_event

You see that it passes a “recipient” argument to the “send_email” worker – when the worker has been started, these arguments combined with the HTTP message are sent to him using stdin.

The worker document in the worker database is quite simple:

``` js
{
   "_id": "send_email",
   "arguments": {
   },
   "delegate": "sendmail.js",
   “type”: “node”,
   "_attachments": {
       "sendmail.js": {...},
      “someOtherScript.js”: {...}
   }
}
```

The delegate property defines which of the attached scripts should be executed – other scripts may be attached because they are required dependencies.
The type property tells the event system that sendmail.js is a Node.js script – it would be easy to implement workers in any other language as long as necessary interpreters are installed on the system.
When you write your own workers you only need to make sure you listen on stdin for incoming data. The Event System manages the rest like starting the Worker when triggered through an Event, sending it data and stopping the Worker when its no longer needed.

When the LivelyCouch code is ready to release I will work on some more practical tutorials. But I hope this explains the main concepts and look forward to suggestions and critique.
