---
title: 'System Design'
date: 2022-05-16T02:29:36+07:00
draft: false
description: 'How to design a large scale system'
showToc: true
TocOpen: false
ShowBreadCrumbs: true
ShowPostNavLinks: true
tags: ['VTF-2022', 'VNG', 'Tech', 'System Design']
---

Hello everyone, this is my first blog. Today we will have a discussion on System Design.

# Introduction

In this era, writing blog is very popular, especially for software developers. They can write blog to get deeper understanding about a concept, a problem, or a technology as well as improve their writing skill and share knowledge to people.

Write a blog for just yourself or a few people to read is easy, but when the number of users scale up, the _transactions per second_ (tps) may increase rapidly, how can your system handle this situation? This lead to the problem we will discuss today.

# Problem

The problem my mentor assigns to me is to design a system for serving blogs to massive number of readers (about 10k tps).

# Solutions

From a fresher's perpective, I can propose some solutions:

- [Vertical Scaling](#vertical-scaling)
- [Horizontal Scaling](#horizontal-scaling)
- [Load balancing](#load-balancing)
- [Caching](#caching)
- [Using CDNs](#using-cdns)

![Scaling](https://images.viblo.asia/9a5cb149-a4e2-4c1b-8bbf-121e5372362b.png)

## Vertical Scaling

This is the first solution people can think of when talk about scaling. **Vertical Scaling** does not require any modification in your application. Suppose your system can serve 1000 tps well, but when your blog becomes popular, more and more people visit your site to read, the traffic will increase rapidly which leads to lagging and bad user experience. In this situation, your system does not have enough resource to handle a large number of requests, so you can simply add more resources like CPUs, RAMs, Disks to your existing system.

However, this simple way has some disadvantages. Firstly, when a computer in your system fails, it affects many users. Secondly, adding more resources to your existing system has a limit, there will be a time when you cannot add resources to your system anymore. Thirdly, when adding resources, users will be affected by downtime.

## Horizontal Scaling

The second way is to use **Horizontal Scaling**. By this way, instead of increasing the size of existing servers in our system, we can add more servers to our system. This solution helps us serve a large number of users without limitation like the above solution, it also does not require downtime because we only add more server which does not affect the existing services. The risk is also evenly distributed across servers instead of concentrating on one large server. The cost for this solution is also cheaper when using many litte servers instead of one large server.

However, this solution has a drawback that it requires more complex configuration than Vertical Scaling because it has an issue about data inconsistency across multiple machine, which need code for handling.

## Load balancing

![Load balancing](https://miro.medium.com/max/1400/1*tEaZGz-p1-E2ytNjl5RPJg.jpeg)
When using Horizontal Scaling, more and more servers getting added over time to our system, so how can we distribute the traffic effectively on a cluster of servers? It's the time **Load balancing** comes in to play.

**Load balancer** sits in front of servers and routing users' request to appropriate server. The traffic is distributed evenly on each server and when one server fails, the **Load balancer** directs the traffic to the remaining servers which make downtime nearly impossible.

This technique decreases the response time, increase throughput.

## Caching

![Caching](https://csharpcorner-mindcrackerinc.netdna-ssl.com/article/caching-mechanism-in-asp-net-core/Images/0_oGWlpmZJ05JaWXQC.png)

Up to now, our system has scaled quite good, but there are still some problems.
Imagine a user continuously performs the same request, for each request load balancer must find a server to handle, the assigned server must do some complex calculations or query a massive amount of data from database. This is the problem that **Caching** will solve.

**Caching** is a technique to increase data access and reduce the load on the system. Cache is a place to store a collection of data, often temporarily, allowing reuse of previously retrieved or calculated data, so it will help speed up data retrieval in the future. So when we faced the problem above, cache helps us solve it easily, just return the stored result to the user!

## Using CDNs

![CDNs](https://blog.vinahost.vn/wp-content/uploads/2020/08/20200715-163911-CDN-3.png)

One other way to scale our system is using CDNs. The CDN servers keep cached copies of the content (such as images, web pages, etc.) and serve them from the nearest location. By using CDNs, the page load time for our users is reduced very much because data is retrieved from the nearest location relative to user.

# Conclusion

That's what I haved learned through researching about design large scale system. This is just the surface level of system design, I will come back and write more detail about this interesting topic later after the final exam ^^! Thank you for reading.
