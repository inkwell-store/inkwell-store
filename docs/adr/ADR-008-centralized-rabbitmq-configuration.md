# Centralized rabbitmq configuration

## Context
The message broker RabbitMQ allows communication between services using messages. These messages are sent by producers and delivered to consumers. This setup involves the use of certain structures, like queues, exchanges, topics and more. 

One interesting aspect of the model offered by rabbitmq is that services, either consumers or produces might define these structures internally and then ask rabbitmq to create them at runtime. A consumer, for example, can define a queue internally and, when it communicates with rabbitmq the latter will create said queue.

This configuration of how data flows in these abstractions is also called **schema**, **topology** or even **definitions**.

## Options considered
* Allow each service to define their own topology.
* Centralized topology away from services to rabbitmq itself.

## Decision
After some consideration I decided to define the topology away from services. This has several advantages, and the biggest is having a single source of truth for the system's topology.

If I were to allow services to create their own definitions, as the project grew it would become harder to debug and test data flows that interact with rabbitmq. Also, changing one service could produce a change inside the broker, and I don't think this is a good pattern.

With this approach I can separate the use of queues, bindings and exchanges of their implementations.

## Consequences
* Decouples topology definition from service implementation.
* Chances of typos during topology declaration by services.
* Easier to debug and test the schema because there's only one source of truth.
* The RabbitMQ container should have their definitions already in place before the services can interact with it.
* Even with this approach nothing stops services to define topologies within themselves.