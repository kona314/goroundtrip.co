---
title: A New Era of Pantograph is Here
date: 2026-09-14T11:00:00-0700
summary: Introducing an all-new Pantograph
---

Pantograph's backend has been completely rewritten from the ground up.

The brand new architecture, codenamed Grand Central, centralizes all of Pantograph's backend components into one codebase; it even shares a core package with the iOS client, reducing code duplication. Powering the new backend is [Vapor](https://vapor.codes), a blazing fast server-side Swift framework. 

Overall, the new features you'll see today are limited. The focus has been on getting (most) existing features working in the new version. As an independent developer, for me, a key improvement is that updating Pantograph and adding new features is *way* simpler in the new version, which means faster development and rollout of new functionality—I've already got some great stuff in the works. 

Today's updates aren't without anything new, though:

### New agencies
* Link Transit (Wenatchee, WA)
* Ben Franklin Transit (Tri-Cities, WA)
* Yakima Transit (Yakima, WA)
* Cherriots (Salem, OR)
* Valley Regional Transit (Boise, ID)
* WestCAT (Contra Costa County, CA)
* Metrolink (Southern CA)
* Culver CityBus (Culver City, CA)
* Capital District Transportation Authority (Albany, NY)
* CTtransit (Connecticut)
* Many more soon!

### iOS app
* Redesigned for Liquid Glass in iOS 26, 27, and beyond.
* Route and vehicle information screen designs are improved.
* Enhanced presentation of service alerts.
* Missed trips includes options for which routes to count in the total.
* Pro: Get push notifications when select vehicles are put in service. 

### Web version
* New vehicle info popup, featuring full trip schedule and realtime information, auto-scrolling to the next stop, and a friendlier UI.
* Realtime stop statuses show on the map for the selected vehicle.
* Enhanced presentation of service alerts.
* Route filters are easier to use. 
* Missed trips includes options for which routes to count in the total.
* Design enhancements across the board.

One of the most important features of the new version is the one you can't see: I have a full set of administration tools, enabling me to maintain agency configuration and vehicle rosters easily and from anywhere. All vehicle rosters have been updated with the latest information I could get. 

## Pro Subscription
I'm also making some changes to the Pro subscription. Pro now requires an account and is accessed on both the web and on iOS. It comes in two tiers: Pro and Pro Starter, available respectively at $30 and $15 per year (or $4 and $2 per month). Existing Pro users will be converted to Pro Starter automatically. 

All information for ±1 week from the current date will be free for all users, while Pro Starter unlocks ±4 weeks, and Pro unlocks everything available. Vehicle push notifications are only availble at the Pro tier. Previous Pro features, like filtering, are now available for all.

This model better reflects the costs associated with running Pantograph while maintaing my core values that data on an essential public service should be free. I also have new features planned that will fit into this two-tier system and take more advantage of account-specific services. 

## Final Thoughts, and Thank You
I knew this would be a tremendous undertaking when I set out on this path nearly three years ago. [I didn't think it would be *quite* this tremendous](https://www.goroundtrip.co/posts/2025/new-pantograph-coming-soon/). Trying to write essentially a whole new application while working full-time at my local transit agency and attempting to maintain the current application and just have a life is, it turns out, kind of a lot to try to do at once. Updates to Pantograph slowed to nearly a halt while I sunk all my development time into the new version—now that it's out, expect the pace to pick back up.

Pantograph was originally built as a fun side project just for me, but it's grown into so much more because of *you*. Your support over the years has made it into what it is today, and I'm so excited to continue diving deeper into transit data with you. 