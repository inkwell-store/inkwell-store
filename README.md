# Inkwell e-commerce book store

## About
I created this project to learn more about distribuited systems, deployment security and software engeneering as a whole. It also give a nice project to test and implement new technologies as I advance in my careeer.

This repository works as an orchestration tool the application and bellow you will find information such as documentations, running the project and more.

## Documentation

### Getting Started
If you want to run and test the project yourself check the [getting started](./docs/getting-started.md) file. There you'll find instructions on how to run the project, build it yourself or a description of how the development environment is setup.

### Architecture Decision Record (ADR)
An ADR is a document used to explain **why** an architecture decision was made. It should be concise and information on the context, alternatives considered, consequences of the. These documents are in *.md* format and can be found [here](./docs/adr/).

### Diagrams
System wide documentation is available [here](/docs/diagrams/).

### Services
Each service has its own repository. Here you can find links for each one:

* [Web client](https://github.com/inkwell-store/front-end-client): web client built with angular, tailwind and angular materials. It communicates only with the api gateway.
* [API Gateway](https://github.com/inkwell-store/api-gateway-service): entrypoint of the application, built using spring's. Decouples the client from individual services by proxying request from the former to the latter.
* [Authorization Service](https://github.com/inkwell-store/authorization-service): it acts as an OAuth Authorization Server. Emits access and re
* [Customer Service](https://github.com/inkwell-store/customer-service): it groups customer related business data, such as personal information, addresses and profiles.
* [Notificatoin Service](https://github.com/inkwell-store/notification-service): service reponsible for sending emails to users in response to events.