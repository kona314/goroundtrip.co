---
title: 'Coming Soon: An All-New Pantograph'
description: Pantograph is being rebuilt from the ground up. 
date: 2025-09-18T11:00:00-0700
author:
    name: Kona Farry
---

Pantograph launched in March 2019, six and a half years ago. It was a big weekend: Late on Friday night, I rode the last bus in the Downtown Seattle Transit Tunnel; on Sunday afternoon, I rode one of the first Swift Green Line buses; and on Monday, the announcement went up on the Seattle Transit Blog. I was incredibly fortunate to have my simple visualization featured in the weeks that followed by The Seattle Times, KING 5, GeekWire, and more. 

Today, Pantograph is far more than I ever expected it to become—but in no place is this clearer than the codebase. 

Over time, adding new agencies and new features has become more challenging, and it became clear it was time to choose: Either I sunset development, or I double down and fundamentally rethink my approach. Nearly two years ago, I chose the latter, and it's almost time for this work to come to fruition. 

## Nerdy Stuff: What I Did Wrong 
Currently, the backend consists of two main components: A Python application handles fetching data from transit agencies and storing it in the database, while a JavaScript application responds to API requests from the clients. At the time, my goal was to leverage the language best suited for each job: I preferred the way Python handles text file processing and protobuf parsing over JavaScript, while JavaScript's Express.js matches my mental model of a web API framework. I also felt keeping these two concerns isolated reduced the risk of a catastrophic outage where client requests go unanswered due to an unrelated feed processing problem. 

What I found as time has gone on and this has become a "real project" is that this makes it exceedingly difficult to do just about anything. I have to implement most new features _four times in three different languages_: Once in the Python server application, once in the JS server application, once in the Swift iOS client app, and once in the JS web client app. I also made the sore mistake of doing all my feed configuration in code, so even simple tweaks are a whole ordeal. 

Further, on the server, every region in Pantograph operates as its own instance of the pair of these applications talking to its own database schema. This means new backend features or bug fixes, once implemented, have to be deployed twice for every region I support, and I have a growing number of databases to manage and evolve together. 

Yes, there are automations to streamline these things, and I have many of those in place. But this was getting impractical, and the distributed nature makes it difficult to implement certain functionality. As I looked at adding more regions, the maintenance burden of all these installations started to get daunting, and I've already been struggling to keep up with what I have while also working full time and living my life.

## Nerdy Stuff: The Route Ahead
Pantograph's new unified backend, codenamed Grand Central, _centralizes_ the two separate server applications I have now. It's written entirely in Swift, a fast, safe, compiled language[^1] that, when coupled with the [Vapor](https://vapor.codes) framework, enables me to do everything that I need to do on the server in one codebase. Since the iOS app is also written in Swift, I can focus my language skills more deeply, and both the server and the iOS client leverage a shared core framework to reduce code duplication and increase safety in the client layer. 

[^1]: Yes, I know Rust exists, please don't come at me. I prefer Swift.

Grand Central Server is designed to scale horizontally, which will make it far easier to match computing resources with need as I add new agencies and features. The unified codebase handles both feed processing and API requests, which can be done in one or more processes operating in a cluster on one or more machines.

This also provides a good opportunity to introduce a number of more detailed changes I've been interested in since very early on, when I began to understand the consequences of some fundamental choices I made in the very beginnings of the project. For instance, I'll be moving away from MySQL in favor of PostgreSQL (with PostGIS for spatial objects), introducing Redis to the stack for storing realtime data, and implementing a much more sensible approach to various identifiers—my initial numeric agency IDs (matching the US-specific FTA ID, as my local agencies do in their GTFS feeds) immediately feel apart when I added TransLink. 

I'm laying a new foundation built with the benefits of years of experience working with transit data, enabling me to incorporate new features now and for years to come. 

## Enough nerdy stuff. What does this mean for me?
I'm going to try to make the changeover as seamless as possible.

There will be noticeable performance and reliability improvements, and as I refresh the codebase, I am making a number of tweaks, improvements, and modernizations to the user interface. On iOS 26, the new version will feature an interface redesigned for Liquid Glass (which I have to say I am _loving_). The core of the app will be instantly recognizable, and there will be new agencies and some small new features on day 1. Importantly, the new backend addresses some key bugs in the current system, like the occasional breaking of some agencies' schedule feeds. 

A handful of features will be changing or going away where it's needed, but I don't take this lightly. Over time, I also expect to bring some features currently only on iOS to the web version, and I have some exciting bigger features in the pipeline, but for the initial launch I'm focused on parity with the current experience on each platform.

There will also be changes to the business model and the Pro subscription. I'll review this more deeply closer to launch time, but my goal is to have a better alignment between the perks of subscribing and my costs, while also holding true to my core belief that free transit data should be free. Pro will also now be on both the web and iOS versions, with one subscription unlocking both platforms via the new user account system. 

After it launches and the dust settles, I expect the pace of development to pick up. I've got a list of new features I'm excited about and plenty of agencies I want to add, all of which has sat on the back burner while I focus on this new era, which lays the tracks for all of this and more. 

## When will the new version come out?
I'm increasingly confident in a launch **this fall**/by the end of the year. I've had development builds of everything running for a while, and am setting up a staging environment of the new infrastructure this month. Most of the work right now is focused on finer details: edge cases, persisting preferences, and building out my administrative tools, for instance. 

That said, if you had asked me at the end of 2023 when I started all of this, I would've said it would probably ship by end of summer 2024, surely by the end of the year. So, maybe take this timeline with a grain of salt, but I'm feeling good about it, and I would very much like to be on the new architecture as soon as it's ready. 

I initially created Pantograph as a way to teach myself about transit operations with no intention of making a product for others to use. In that process, I accidentally created a somewhat advanced realtime map that found an audience, teaching myself not only about transit but also the fundamentals of how to write good code along the way. The new version benefits from all the learnings of the years since, setting a solid foundation for continued growth into the future with more features and more agencies.