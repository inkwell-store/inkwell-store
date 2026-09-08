# End-to-end resource server validation

## Context
The OAuth framework establishes that a **client** might request a resource from a **resource server**, given the former has some form of credential (usually an access token emitted by an **authorization server**) that can be validated.

The resource server checks if the token sent by the client is valid and if it has the right permissions to access that particular resource.

The inkwell store is built as a distributed system and on such architectures is common to use an **API Gateway**. This service is the main entry-point of the application to which clients send requests. The gateway then reads the requests and send it to the appropriate services. This promotes decoupling between the services and client, while exposing a clear API to clients.

Because the services are never exposed outside the system itself adding a gateway provides an interesting dilema: where should the access token validation happen?

## Options considered
1. Add a resource server only inside the API Gateway, while other services trust it will validate the tokens.
2. Add one resource server on each service that needs it, while using the API Gateway only as proxy.
3. Add a resource server on all services, including the API Gateway. 

## Decision
I choose to add one resource server on each service, including the gateway. The main reason for this choice is security redunancy. Each service must enforce their own security rules instead of blindly trusting other services, even though they might run only inside a private network.

Security measures are often redundant by their own nature, and having the overhead from multiple token validations is well worth it. Also, while the gateway acts as the main entry-point it does not mean it needs to be the only security-enforced service. This is especially important when working with senstive data, such as people's bank, address or persinal information, which is precisely the case of this system.

## Consequences
1. This approach introduces an overhead on each http request, that needs to be validated multiple times. This increases cpu and memory usage for the system as a whole.
2. Invalid requests stop at the gateway level, which avoid unecessary service calls.
3. Token validation can be a bit messy if the token expires just after it's validated by the gateway, but before reaching the service.
4. Zero trust policy makes the system more resilient against attacks or poorly designed features.