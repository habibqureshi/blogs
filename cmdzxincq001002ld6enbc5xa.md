---
title: "Case Study: From MVP to Scalable Logistics SaaS"
datePublished: Wed Aug 06 2025 12:13:14 GMT+0000 (Coordinated Universal Time)
cuid: cmdzxincq001002ld6enbc5xa
slug: case-study-from-mvp-to-scalable-logistics-saas
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1754393666007/f54c0bec-41c1-4f9a-b2e7-109e43c0f5fd.png
tags: startup, technology, development, mvp-development

---

## The Birth

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754481257385/27b93937-66d8-4133-9d5e-1a9365ac944b.png align="center")

When we started building **Techship**, a logistics platform, our priority was speed. Like most MVPs, we made intentional trade-offs to launch quickly and validate the idea:

* A monolithic Spring Boot backend with a SQL database
    
* A React frontend based on module needs
    
* No complex scaling or deployment setup
    

We focused only on the core operations — order creation, shelf picking, and delivery tracking — and got it live fast. This lean setup helped us test quickly with real users.

## The First Crisis

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754481980347/bdaad80a-0407-4d1f-b0de-2feafd07e965.png align="center")

Orders were flowing in. Customers were happy. But behind the scenes, the cracks were forming.

When we launched, a single server ran everything — order placement, deliveries, and updates — and it worked perfectly for our initial user base. But as more users came on board, the system began to struggle: it would slow down, run out of memory, and even freeze during peak times.

This wasn’t a bug — it was a sign of growth.

## Growing the Monolith

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754481999921/36e7cc1b-f2b9-4be5-8266-cb714145197d.png align="center")

It became clear: user growth and system growth are **directly proportional**. Supporting more users meant evolving the MVP into something more scalable and resilient.

We tried vertical scaling. That meant upgrading the same server — more CPU, more RAM, more disk. It worked... for a while. But the same issues kept returning every time user traffic spiked.

## One Solution, Two New Problems

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754482012815/07a3c643-a618-47af-910e-c5327499a6fa.png align="center")

So we scaled the server — problem solved, right? Not quite.

The problem? We had to scale the whole machine, even if only one part of the app was struggling. It was a manual, inefficient process that drove our cloud costs up by 75% — especially since our traffic wasn’t high 24/7. We were paying for peak capacity all the time, even when we didn’t need it.

It became clear: this fix wasn’t scalable — it was just a delay.

## Auto-Scaling: A Better Fit, Not a Perfect One

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754482025336/e64899a7-467a-4cf9-af0a-ff131c41ba92.png align="center")

To overcome the limitations of vertical scaling, we migrated to a **managed instance group with auto-scaling** on Google Cloud Platform. Instead of upgrading a single server, this setup allowed us to **scale horizontally** — adding or removing virtual machines based on real-time traffic.

## Benefits of migrating to auto-scaling instance groups:

* ✅ **Improved reliability:** The system automatically handled spikes in traffic without downtime.
    
* ✅ **Reduced manual effort:** Scaling was automatic — no need for engineers to intervene.
    
* ✅ **Cost efficiency:** Idle servers were shut down, so we only paid for what we used.
    
* ✅ **No over-provisioning:** We avoided paying for peak capacity 24/7.
    
* ✅ **Consistent performance:** Users experienced stable performance even during high loads.
    

**But it wasn’t perfect.**

Cold starts caused delays during traffic spikes, as each new instance took time to boot and initialize. And often, one service would trigger a new instance, while the rest of the server stayed mostly idle. We were spinning up full machines for partial workloads — and paying for all of it.

This is a common issue — studies show that 30–35% of cloud spend is wasted due to idle or underused infrastructure.

## Scaling Smarter with Microservices

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1754482042182/4d0acc2b-1ce4-495e-ba1f-a13dcab0f0c8.png align="center")

To fix the issues with auto-scaling VMs, we moved to a **container-based architecture** using **Kubernetes (GKE)**. We broke our app into **microservices**, each running in its own Docker container,enabling true horizontal scaling at the service level

> “Think of vertical scaling like upgrading your laptop — faster CPU, more RAM. Eventually, it still slows down. Horizontal scaling is like adding more laptops and sharing the load.”

This allowed us to **scale each service independently**, instead of spinning up full servers. Kubernetes handled the heavy lifting — from placing containers on the right machines to balancing traffic and restarting anything that failed.

Because our services are **stateless**, Kubernetes could move them around freely, making the system more reliable and easier to scale. We also used **auto-scalers** that adjust both the number of containers (pods) and machines (nodes) based on real usage — so we only pay for what we actually need.

**Benefits of Scaling with Microservices and Kubernetes:**

* ✅ **Independent scaling:** Each service scales on its own based on demand — no need to scale the entire app.
    
* ✅ **Better resource usage:** No more idle servers — containers use only what they need.
    
* ✅ **Improved reliability:** Kubernetes restarts failed services and balances traffic automatically.
    
* ✅ **Faster deployments:** Smaller services are easier to update and release without affecting the whole system.
    
* ✅ **Cost efficiency:** Auto-scalers ensure we only use (and pay for) the resources we need.
    
* ✅ **High availability:** Stateless services can run anywhere, making the system fault-tolerant and flexible.
    

### **Key Takeaways**

* **Start simple.** At the MVP stage, simplicity is key. You need to move fast, test your idea, and keep costs low. A basic, monolithic setup is perfect for that — quick to build, easy to launch.
    
* **Growth changes everything.** As users grow, so do system demands. What worked for 100 users starts breaking at 1,000. Performance drops, costs rise, and the cracks begin to show.
    
* **Vertical scaling gives quick wins — but doesn’t last.** Adding more power (CPU, RAM) to a single server helped short-term, but was expensive and manual. We were scaling the entire system just to fix one part.
    
* **Auto-scaling improved reliability — with tradeoffs.** Moving to Google Cloud’s auto-scaling instances gave us stability during spikes. But cold start delays and underutilized servers meant we were still wasting resources and paying for idle capacity.
    
* **Microservices and Kubernetes made scaling smarter.** By breaking our app into smaller parts (microservices) and running them in containers, we could scale only what was needed. Kubernetes managed everything — balancing traffic, restarting failures, and adjusting automatically with demand.
    
* **The result: flexibility, reliability, and cost control.** With a stateless, containerized system and autoscaling in place, we now scale efficiently, avoid waste, and deliver a more stable experience to users — without overpaying for cloud resources we don’t need.
    

> Scaling isn’t a one-time fix — it’s a process every growing product must go through. Start simple, but be ready to evolve.