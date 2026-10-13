# Use of github organization

## Context
Distribuited systems have a variety of independent developed and deployed services. Each service also needs to have a source code versioning.  

## Options considered
* Create one organization and group all services/repositories together.
* Create one repository for all services and maybe separate them in branches. 
* Create separated repositories directly inside my github profile.

## Decision
The best solution provided by github is to create an organization and group all repositories there. It makes sense to group them, because although they are independent they also belong to the same application. Creating a single repo for all of them would be insanity, and one repo for each service directly inside my account doesn't group these services together in any way.

## Consequences
* Building the project requires fetching data for multiple repositories, which requires some setup especially with the introduction of versioning.
* Services have their implementation and updates isolated from others.
* Repositories can have the organization embedded to their urls, which makes sense semmantically because they belong to the same appication.
