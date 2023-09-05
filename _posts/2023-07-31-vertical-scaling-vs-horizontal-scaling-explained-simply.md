---
title: "Vertical Scaling vs. Horizontal Scaling: Explained Simply"
date: "2023-07-31"
tags: 
  - "api"
  - "app-development"
  - "devops"
  - "scalability"
  - "web-development"
header:
    overlay_image: "/img/posts/pexels-photo-1181354.jpeg"
---

Scalability is one of the aspects to make any system future-proof. In this blog post, I will share my learnings about what the scaling is in software deployment, the difference between vertical scaling and horizontal scaling, and when to use each one.

## What is scaling?

An app or an API is useless unless it is deployed to a publicly available server. As you know, servers are computers with specifically designed hardware. These hardwares (CPU, Memory, Storage, processing units, GPUs, etc.) are designed to be switched on all the time, and endure under severe workloads and be durable. However, they have one drawback. They are not limitless. They can only process so much work, and when the workload is increased, they won't be able to process in a timely manner. This is when scaling comes into the play.

Scaling means increasing the capacity of a server with the goal of being able to process more requests/workloads. There are two ways of doing it.

## Vertical Scaling

Vertical Scaling is when we swap a server's hardwares with another hardware with higher capacity. For example, we swap the Memory or the storage to a bigger one. Or change the CPU with another one with more cores. When we change the server, in a way that it becomes bigger with more resources and capacity, this is called Vertical Scaling.

![Vertical Scaling explained simply](https://programmerbyday.files.wordpress.com/2023/07/vertical-scaling.png?w=761)

In today's world, most of the servers are created using Virtual Machines. Virtual machines are configurables and therefore each parts of them (such as CPU or memory or storage) can be increased or decreased via a configuration setting.

## Horizontal Scaling

It is not always possible to add a bigger resource to a server. However, sometimes we might be able to increase the number of servers. When we increase the number of servers, in a way that they collectively process more requests, this is called Horizontal Scaling.

![Horizontal Scaling explained simply](https://programmerbyday.files.wordpress.com/2023/07/horizontal-scaling-croped.png?w=686)

As I said, most servers are deployed as Virtual Machines, and duplicating a virtual machine is a simple task these days. However, with more servers, comes more complexity. Requests need to be distributed among multiple servers. This is usually done by a load-balancer server that sits in front of all the servers to do this distribution.

## Vertical Scaling vs. Horizontal Scaling

The are differences in terms of implementation, technicality, costs and etc. I've captured it in a simple table below:

|  | Vertical Scaling | Horizontal Scaling |
| --- | --- | --- |
| How it works | Increases the capacity of a single server | Increases the number of servers usually each with the same capacity |
| Pros | Easier to implement | \- Infinite scalability  
\- Can scale down easily when the load is less  
\- More cost effective |
| Cons | \- Scalability is limited to available hardwares in the market  
\- Can be more costly in the long run  
\- It takes time to spin up a new server with higher capacity and switch it with the current one  
\- Can cause disruption to the users | \- More complex to implement (needs a load-balancer)  
\- It Is not suitable with legacy system (e.g. [sticky sessions issue](https://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions))  
  
 |
| Best use case | When workload has increased and it is predicted to stay that high from now on OR for a long time | When the workload can increase/decrease at any time |

Vertical Scaling vs. Horizontal Scaling

## Conclusion

Vertical Scaling is when we increase the resources/hardwares in a single server, whereas Horizontal Scaling is when we increase the number of servers. Each has its own merits and pitfalls. I'd recommend to lean towards horizontal scaling for green field projects. Even if you are working on a legacy system, try to change it in a way that it is more deployable with horizontal scaling.

![Horizontal Scaling vs. Vertical Scaling compared in a simple image](https://programmerbyday.files.wordpress.com/2023/07/scaling-compared.png?w=849)
