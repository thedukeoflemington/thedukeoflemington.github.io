---
title: "Cloud-Scale Architecture Patterns For The
Post-Moore’s Law Age"
image: /assets/images/posts/end-of-moores-law.jpg
excerpt_separator: "<!--more-->"
categories:
  - Architecture
tags:
  - architecture
  - patterns
  - cloud
  - domain driven
  - cqrs
  - event sourcing
---

Are you developing cloud-based applications or services, or migrating a legacy system to a cloud-hosted environment? Are you overwhelmed by the sea of cloud hosting providers, the multitude of services they provide, and the meaning or significance of all of the buzzwords thrown about in this space? Perhaps you are familiar with the landscape, but are you having difficulty weighing the pros and cons of all of these options and how best to apply them to solving your business problems? Is the pace of technologies, services, and frameworks moving so quickly that you feel paralyzed in committing to significant and impactful changes? You may even feel confident in your understanding of the technology options and are well underway in utilizing them in developing next generation solutions, but are you leveraging these platforms to their full potential? Have you ever wondered about the state-of-the-art in cloud-native architecture and how large-scale systems are designed for maximum scalability?

If you are looking for anything more than a simple Lift and Shift of your previous architecture solutions (and you should be), then you need to step back and look at the big picture: the architecture patterns and development methodologies that are aligned and proven under the current technology landscape.

# Motivations
Let's look into some of the pertinent motivations for moving to the cloud. 

## Scalability
This one is of such significance that it has been granted its own buzzword - Cloud Scale. Cloud platforms provide various scalability options to grow (and shrink) your resources as you need them. Scalability still comes at a cost, however, and the efficiency and flexibility of your resourcing needs can vary dramatically depending on the design of your system.

### The Influence of Moore’s Law
System design under the reign of Moore’s Law, which held true from its inception in 1965 until around 2000, relied on hardware advances outpacing software. Every few years, a hardware upgrade would guarantee an increase in CPU clock speed and, hence, the vertical scalability of the software it hosted.  Since the turn of the century CPU advancement has shifting from an increase in clock speed towards an increase in cores or energy efficiency. As a result, system architectures that are premised on and/or have benefited from the vertical scalability of Moore’s Law are seeing diminishing returns in platform upgrades (physical or virtual), and are faced with the need to find alternate approaches to maintain scalability. This generally translates to a shift away from designs premised on monoliths, shared state, thread-based concurrency, and synchronous blocking function calls.

### The Influence of Amdahl’s Law
Emphasis has shifted from systems dependent on Moore’s Law to those increasingly influenced by Amdahl’s Law, i.e. parallel computing. Infrastructure barrier to entry has never been lower due to scalable and elastic cloud PAAS and SAAS offerings. As existing and startup enterprises pivot their system designs to exploit the business and competitive advantages of these offerings, architecture patterns are emerging, and in some cases re-emerging with renewed relevance, as more suitable and capable of leveraging the benefits of the current infrastructure landscape. If we can no longer ride the coattails of CPU clock speed increases, the scalability of our systems will be determined by how effectively the software is designed to leverage the resources it has and in a parallel manner, with a focus on addressing bottlenecks that result from such a paradigm shift. This generally translates to designs premised on distributed services, light-weight co-operative concurrency, immutable state, and asynchronous non-blocking function calls.

## Software as a Service
Cloud-native services have proven the ability and demonstrated the alure of the hosting and deployment model known as Software as a Service (SaaS), in which a system is offered under the premise of a subscription model and backed by a multi-tenant system design that supports all clients. This model is an alternative to maintaining multiple and customized versions and deployments. Instead, all customers are collectively subject to the continuous rollout of new features, improvements, and fixes. This subscription model approach tends to lead to architecture patterns that support more frequent and incremental agile service-based deployment.

## Leveraging Cloud-Native Services
Cloud platforms typically support common infrastructure services, such as persistence and caching, that leverage efficiencies in pricing as well as functional capabilities that are costly and complex to roll out on your own. This includes data sharding and geo-based routing, replication and failover.

## Managing Complexity
Cloud-scale systems are inherently complex. The same factors that enable flexibility and scalability in performance also encourage systems that grow organically in complexity over time. Therefore, suitable architecture patterns are critical to manage this complexity and support maintainability of systems over their lifetime. 

Let's explore alternative approaches that are designed to address such challenges.

# Patterns and Methodologies
This list can certainly be extended, but I consider these to be the pillars of Cloud Scale design. If you Google any two of them, you’ll see how they are often combined in a complementary manner due to the alignment of interests and synergies they share.

## Domain Driven Design
This is as much a development methodology as it is an architecture pattern, though there are architecture patterns that are very much aligned with and support it. The premise of domain-driven design is the following:
* placing the project's primary focus on the core domain and domain logic;
* basing complex designs on a model of the domain;
* initiating a creative collaboration between technical and domain experts to iteratively refine a conceptual model that addresses particular domain problems.

At the core of a software system is a set of domain model assets that directly reflect the bounded contexts and ubiquitous language used by both domain experts and developers to describe and model the domains. These are the primary software assets of the business. They are developed and tested independently of all other architectural components, which play a supporting role and are of secondary importance.

### References
[Domain-Driven Design: Tackling Complexity in the Heart of Software](https://read.amazon.ca/kp/embed?asin=B00794TAUG&preview=newtab&linkCode=kpe&ref_=cm_sw_r_kb_dp_J2GmCbJWHZWSX)
I.e. The Big Blue Book, by Eric Evans the seminal text on the subject.

[Implementing Domain Driven Design](https://read.amazon.ca/kp/embed?asin=B00BCLEBN8&preview=newtab&linkCode=kpe&ref_=cm_sw_r_kb_dp_A4GmCb9RCP75T)
An updated and more implementation-focused complement to The Big Blue Book, by Vaugn Vernon

[Wikipedia: Domain-driven Design](https://en.wikipedia.org/wiki/Domain-driven_design)

## The Reactive Manifesto
A set of guiding principles and expectations for reactive design patterns.

### References
[The Reactive Manifesto](https://www.reactivemanifesto.org/)

## The Actor Model
In contrast to legacy concurrency models based primarily on threads, locks, and shared immutable state, the actor model is based on the following key principles:
* No shared state
* Lightweight processes
* Asynchronous message-passing
* Mailboxes to buffer incoming messages
* Mailbox processing with pattern matching

[Wikipedia: The Actor Model](https://en.wikipedia.org/wiki/Actor_model)

## Command Query Responsibility Segregation
This architecture pattern decouple the read and update models, resulting in more optimized persistence models for both sets of use cases, as well as improved maintainability by removing the complexity of managing both considerations in the same code at the same time. This pattern is often coupled with Event Sourcing.

### References
[CQRS Documents by Greg Young](https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf)

[CQRS](https://martinfowler.com/bliki/CQRS.html)

[Greg Young - CQRS and Event Sourcing - Code on the Beach 2014](https://youtu.be/JHGkaShoyNs)

## Event Sourcing
This pattern is based on the premise of modeling events and, specifically, the sequence of events over time rather than modeling current state. This allows for highly performant append only persistence and simplified schema.
Probably the best-known example of Event Sourcing (to developers, at least) is [Git](https://git-scm.com/) and similar distributed source code management solutions that manage a history of changeset 'events'. This pattern is often coupled with CQRS to decouple and optimize the read and write persistence models.

### References
[Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)

[Event Sourcing: What it is and why it's awesome](https://dev.to/barryosull/event-sourcing-what-it-is-and-why-its-awesome)

## Clean Architecture
I'm using the term here in reference to a collection of similar architecture patterns described by Robert C. Martin (Uncle Bob). The common premise of these patterns is that the primary business intent that the architecture supports - the business domain models and use cases - form an independent core to which all dependencies point inward. Supporting infrastructure services, frameworks, and libraries to support concerns such as user interfaces, network and persistence integration are external, with layering from abstraction to implementation directed from the inside out. Inversion of Control using Dependency injection is a common design pattern to enforce dependencies between abstract interfaces, rather than on concrete implementations. You can see how these architecture patterns support Domain Driven Design.

### References
[Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
