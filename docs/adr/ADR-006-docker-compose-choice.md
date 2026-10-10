# Docker compose choice

## Context
Distribuited systems are developed around services with clear boudaries. These services must be independently developed and deployed. Each service's life-cycle involves deployment, monitoring, failure response-recovery, scaling, service communication, service updates... To accomplish this a series of tools can be used, each with its own use cases.

## Options considered
* Develop and deploy using kubernets
* Develop and deploy using docker compose

## Decision
In truth, both compose and kubernets deal with container/service instantiation, but kubernets has more abstractions which make it an **orchstration** tool. Kubernets can create the services, but also deploy and scale them on different machines, restart a service that crashes, heathy checks and more. All these capabilities make it a great tool for production, but it comes with a cost in both complexity and cpu+memory consumption. 

The main reason to choose docker compose is because it's simpler to implement on a single machine. I can quickly create and test individual containers using compose files or a quick terminal command. The current configuration uses multiple compose files, so the environments are already in place.

Compose's simplicity is specially valuable for my development environment, as I'm using one machine and my computer has limited specs. Kubernets's abstractions add little here, more so because the application at this point is in its early stages with few features already created. I don't want to add a tool just to add it and, when I consider my current needs, compose is more than enough.

In the future, once more features are implemented adding kubernets is a certainty for a production environment, but right now it's not my priority.

## Consequences
* Docker compose makes development and service instantiation simpler and quick for a single machine, while being easily reproducible for other people.
* Although compose has properties like `depends_on` to control which service starts first it doesn't guarantee the service is available and working.
* I can avoid kubernets complexity at first, but the application becomes less robust because of the limited features of compose.
* Choosing compose right now doesn't exclude the possible adoption of kubernets in the future and even then the latter won't replace the former entirely.