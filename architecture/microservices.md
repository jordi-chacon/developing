## Microservices

The microservice architecture is a pattern to architect large, complex,
long-lived applications as a set of cohesive services that evolve over
time.

The essence of the microservice architecture is not new.
The concept of a distributed system is very old.
The microservice architecture also resembles SOA.

Microservices don't have to be tiny, that's not the point. The point is for each
service to have a small set of very related responsibilities. They can be tiny
or rather large.

A service could be responsible for:
* handling a particular use case
* handling all operations for a particular resource or entity

The decoupling of services also must occur at data level. Each service must have
its own database in order to be fully decoupled from other services.
When necessary, consistency between databases is maintained using either
database replication mechanisms or application-level events.



### Monolith vs microservices

#### Benefits of monoliths
When the monolith is not big, they are:
* simpler to deploy (you just deploy one binary).
* simpler to monitor (just monitor one server, or a set of servers running the
same binary).
* simpler to do end-to-end testing.



#### Drawbacks of monoliths
* All eggs in one basket. If a component in the monolith is leaking memory, it
can potentially affect the performance of all other components and it can also
bring all components down.
* Large codebase intimidates new developers.
* Large codebase can get difficult to understand and modify.
* Lack of hard module boundaries means that usually modularity breaks over time.
* Quality declines and development typically slows down.
* Continuous deployment is difficult. Eventually, as the app grows in size and
complexity, the risk associated with redeployment increases, which discourages
frequent updates.
* Encourages a centralized deployment management, where each development team
working on the monolith is not responsible for the pipeline, but rather a
Release team is. This depowers development teams from releasing their changes
quickly and by themselves.
* It is likely to get painful and slow when several teams are working on the
same codebase.
* Requires a long-term commitment to a tech stack. It is hard to incrementally
adopt a newer stack.
* Development speed slows down also due to longer compilation time and much
higher amount of tests that need to run to validate your change.
* Cannot scale each component of the application independently according to
the needs of that component. You can only scale the whole application.



#### Benefits of microservices architectures
* Fault isolation. If a component is misbehaving or goes down, this doesn't have
to affect other services. Most of them can keep running without caring at all.
Others can degrade gracefully upon any service being unavailable.
* Each service can run in a hardware that fits its needs.
* Each service can scale at a different speed than others, depending on the load
that each service receives.
* Each service is relatively small, which makes its codebase easier to
understand.
* New developers in a given team can get up to speed much faster as the codebase
owned by that team is smaller and simpler than that of a monolith.
* Each service can be deployed independently of other services.
* Each development team can own its own deployment pipeline. This empowers
them to release as often as they want whenever they want. They do not depend
on any Release team.
* Easier to scale development.
* Eliminates long-term commitment to a tech stack.
* When building completely new services, you can choose to try out new tech
stacks.
* Fast development flow: compilation of a service is much faster. Running
the tests of a particular service whenever you made a change is also much
faster. Quicker feedback loops.



#### Drawbacks of microservices architectures
* Higher deployment complexity overall.
* Higher operational complexity.
* Developers must deal with the additional complexity of working within a
distributed system.
* End-to-end testing becomes harder.



### More on microservices



#### When to use microservices architecture
One challenge with using this approach is deciding when it makes sense to use
it.

When developing the first version of an application, you often do not have
the problems that this approach solves. Moreover, using an elaborate,
distributed architecture will slow down development. This can be a major
problem for startups whose biggest challenge is often how to rapidly evolve
the business model and accompanying application.

Later on, however, when the challenge is how to scale and you need to use
functional decomposition then tangled dependencies might make it difficult
to decompose your monolithic application into a set of services.



#### How do clients talk to a microservice architected application?
A common approach is to have an `API gateway` service sitting in between
your client and the rest of your services. Clients talk to the API gateway.

The API gateway offers a set of endpoints. When called, each endpoint will
handle the incoming request by making requests to some number of services over
the high-performance LAN, receive results back from them, aggregate those
results and provide a response back to the client.

The API gateway encapsulates the details of the other services and knows how
to talk them.



#### Inter-service communication

##### Synchronous HTTP
It's easy to work with, most of us are used to the request/response style
of communication.

The biggest limitation this approach has is that both client and server
must be simultaneously available, which is not always the case since
distributed systems are prone to partial failures.

##### Asynchronous messaging
It decouples message producers from message consumers. The message broker will
buffer the messages until the consumer is able to process them.

Producers are completely unaware of the consumers.

The request/response style is not a natural fit.

One downside of using messaging is needing a message broker, which is yet
another moving part that adds to the complexity of the system.

There are pros and cons of both approaches. Applications are likely to use
a mixture of the two.


### Resources
http://martinfowler.com/articles/microservices.html
http://martinfowler.com/bliki/MicroservicePrerequisites.html
http://203.softover.com/2014/12/01/ultra-srevices-and-declaration-of-independence/
http://contino.co.uk/microservices-not-a-free-lunch/
http://capgemini.github.io/architecture/microservices-reality-check/
http://www.infoq.com/articles/microservices-intro
http://www.reactivemanifesto.org/
https://github.com/cer/event-sourcing-examples/wiki/WhyEventSourcing
http://queue.acm.org/detail.cfm?id=1394128