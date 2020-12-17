## Concepts (By Martin Fowler)
Services:
- concept in microservices:
services are out-of-process components who communicate with a mechanism such as a web service request, or remote procedure call (RPC). 
- concept in OOP:
Many object-oriented designers, including ourselves, use the term service object in the Domain-Driven Design sense for an object 
that carries out a significant process that isn't tied to an entity

Components:
Our definition is that a component is a unit of software that is independently replaceable and upgradeable.

Libraries:
We define libraries as components that are linked into a program and called using in-memory function calls
 
Application:
I don't think applications are going away for the same reasons why application boundaries are so hard to draw. Essentially applications are social constructions:
- A body of code that's seen by developers as a single unit
- A group of functionality that business customers see as a single unit
- An initiative that those with the money see as a single budget

## Componentization via Services

## Organized around Business Capabilities

## Products not Projects
Microservice proponents tend to avoid this model, preferring instead the notion that a team should own a product over its full lifetime

## Smart endpoints and dumb pipes

Applications built from microservices aim to be as decoupled and as cohesive as possible, they own their own domain logic and act more as filters in the classical Unix sense
receiving a request, applying logic as appropriate and producing a response. 

## Decentralized Governance
This can make room for different standards for differents teams around this microservices.
Each microservice can use a different language.

Perhaps the apogee of decentralised governance is the build it / run it ethos popularised by Amazon. Teams are responsible for all aspects of the software they build including operating the software 24/7.

## Decentralized Data Management
Microservices prefer letting each service manage its own database, either different instances of the same database technology, or entirely different database systems - an approach called Polyglot Persistence. 

Decentralizing responsibility for data across microservices has implications for managing updates. The common approach to dealing with updates has been to use transactions to guarantee consistency when updating multiple resources. This approach is often used within monoliths.

Using transactions like this helps with consistency, but imposes significant temporal coupling, which is problematic across multiple services. 

## Infrastructure Automation

## Design for failure

A consequence of using services as components, is that applications need to be designed so that they can tolerate the failure of services. Any service call could fail due to unavailability of the supplier, the client has to respond to this as gracefully as possible.

Netflix's Simian Army induces failures of services and even datacenters during the working day to test both the application's resilience and monitoring.
*Simian Army is deprecated, Netflix now uses different repositories for this: chaosmonkey and spinmaker 

Since services can fail at any time, it's important to be able to detect the failures quickly and, if possible, automatically restore service. Microservice applications put a lot of emphasis on real-time monitoring of the application, checking both architectural elements (how many requests per second is the database getting) and business relevant metrics (such as how many orders per minute are received). Semantic monitoring can provide an early warning system of something going wrong that triggers development teams to follow up and investigate.

## Evolutionary Design

This emphasis on replaceability is a special case of a more general principle of modular design, which is to drive modularity through the pattern of change [14]. You want to keep things that change at the same time in the same module. **Parts of a system that change rarely should be in different services to those that are currently undergoing lots of churn.** 
**If you find yourself repeatedly changing two services together, that's a sign that they should be merged.**

## Are Microservices the Future?

There are certainly reasons why one might expect microservices to mature poorly. In any effort at componentization, success depends on how well the software fits into components. It's hard to figure out exactly where the component boundaries should lie. Evolutionary design recognizes the difficulties of getting boundaries right and thus the importance of it being easy to refactor them. But when your components are services with remote communications, then refactoring is much harder than with in-process libraries. Moving code is difficult across service boundaries, any interface changes need to be coordinated between participants, layers of backwards compatibility need to be added, and testing is made more complicated.

References:
https://martinfowler.com/articles/microservices.html
https://docs.microsoft.com/pt-br/dotnet/architecture/microservices/architect-microservice-container-applications/microservices-architecture

