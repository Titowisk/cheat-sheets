
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

# Componentization via Services

# Organized around Business Capabilities

# Products not Projects
Microservice proponents tend to avoid this model, preferring instead the notion that a team should own a product over its full lifetime

# Smart endpoints and dumb pipes

Applications built from microservices aim to be as decoupled and as cohesive as possible, they own their own domain logic and act more as filters in the classical Unix sense
receiving a request, applying logic as appropriate and producing a response. 

References:
https://martinfowler.com/articles/microservices.html
https://docs.microsoft.com/pt-br/dotnet/architecture/microservices/architect-microservice-container-applications/microservices-architecture

