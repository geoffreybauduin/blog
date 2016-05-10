---
title: 'Working with promises: nested http requests in Angular.js'
date: 2016-05-10 22:49:01
tags:
 - angular.js
 - javascript
categories:
 - Code
---

It's been a while since I posted here, but I thought I could share something that happened to me at work today.
I am now almost entirely dedicated to backend development, but sometimes, I need to take one for the team and work on frontend. We are using Angular, and we've been doing some amazing stuff so far with that.

One of my colleague, who is totally new to Angular, was asking me about how I would do the following: "be able to execute the function of my choice when a 2-step http request has been performed".

Knowing some stuff about Angular, I directly told her she could use *promises*, with the [`$q`](https://docs.angularjs.org/api/ng/service/$q) package from Angular, and gave her some piece of code so that she could understand the whole thing.
I thought that it could be useful to someone else, so I am just going to leave this here

```
function fn1 () {
  var deferred = $q.defer();
  $http.get("http://a.com/first").then(function (response) {
    $http.get("http://a.com/second").then(function (response) {
      deferred.resolve(response);
    }, function (response) {
      deferred.reject(response);
    });
  }, function (response) {
    deferred.reject(response);
  });
  return deferred.promise;
}

fn1().then(function (response) {
  console.log("success");
}, function (response) {
  console.log("failure");
});

fn1().then(function (response) {
  console.info("another success");
}, function (response) {
  console.info("another failure");
});
```

With this simple `fn1` function, you can have a multiple behaviors linked to the same requests process.

[Gist link](https://gist.github.com/lght/ea5b2e633463f87aacf2bbf61d5ee8c6)