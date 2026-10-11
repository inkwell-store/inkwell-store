# RabbitMQ for service communication

## Context
Services inside distributed systems have their own implementations and business rules, but they often need to communicate with each other. Communication between services can be either **synchronous** (like an http request) or **asynchronous**. For the latter a number of protocols and tools are available. One such protocol is the amqp (Advanced Message Queuing Protocol) and tools that manage this communication are called **message brokers**. Asynchronous communication is important because it allows services to have more autonomy, while a broker abstracts this communication away from, effectively decoupling these services.

## Options considered
* RabbitMQ
* Apache Kafka

## Decision
I'm choosing rabbitmq because it provides the queue-based messaging and flexible routing capabilities required by the application. Its exchange, queue, and binding model is suitable for routing messages between services. This decision prioritizes meeting current requirements with a (relatively) straightforward messaging model, without introducing event-streaming features that the project does not currently require.

## Consequences
* Services are decoupled by using a message broker.
* Asynchronous communications are effective, but they introduce temporary incosistency between data on different services. Eventual consistency needs to be accounted for on certain operations.
* Change to another broker, like Kafka, might require changing multiple service's implementations.
* The application has to manage a service for rabbitmq and I have to provide explicit configuration for it.
* The broker's data structures can be defined either by an internal configuration or by each service.