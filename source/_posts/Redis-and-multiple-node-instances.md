title: Redis and multiple node instances
date: 2015-03-02 11:28:50
tags:
 - Redis
 - NodeJS
---

Basically, when building a horizontal-scaling application, one of the problem I encoutered was **how can I synchronize my Node.js instances so that they know what's changed on another instance** ?

Well, after some researches, it seems that most developer use the [`PUBLISH` command of Redis](http://redis.io/commands/publish), which consists in publishing a message onto a channel, while other processes are listening to this particular channel.