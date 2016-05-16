title: Forever service and symlinks
date: 2015-02-20 18:04:13
tags:
 - nodejs
 - symlinks
 - forever
categories:
 - Admin sys
---

For those who have no clue what Forever is, just check here: https://github.com/foreverjs/forever . It's a basic NodeJS application that keeps a NodeJS running if it crashes or if it shutdowns.

Today I've been contacted by a client asking some changes in a NodeJS server I developed. The change made, I just pushed and my continuous integration script on Codeship (http://codeship.io) synced everything and restarted the daemon.
I've been contacted a bit later by this client, saying that the problem he mentioned had not been fixed by my update. This is when I realized that something went wrong on the server, obviously, since everything was working locally.

Basically, I create a folder for every push (of form YYYYMMDDHHMMSS), and I just update the symlink to the newest version, so that I don't have to struggle to find the correct folder in which the newest application is.

My init.d script has been generated automatically by `forever-service` (https://github.com/zapty/forever-service), a Node module. It didn't take the link path, but the target path (`/home/node/deploys/20141223100000` instead of `/home/node/current/`), so everytime I restarted my server, I ended up launching an old version of it.

Quick fix:

** Change the link to your folder under `/etc/init.d/node` **