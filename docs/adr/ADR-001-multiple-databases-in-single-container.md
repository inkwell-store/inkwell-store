# Multiple Databases in Single Container

## Context
In distributed systems, services must have clear boundrys, which usually means they own their data and it's schema. So, a database belongs to the service and only it can access the data. Now, where this database lives can vary greatly.

Since the inkwell store runs on docker containers, the most logical place to deploy and run a DBMS is within docker container and just let other services communicate with it. Now, it's necessary to define how are these databases deployed to their respective containers. 

## Options considered
* Run one container for each database/service.
* Run all databases in a single container.
* Run critical-service databases on their own container and group others on the same container.

## Decision
The main reason I choose to **multiple databases in a single docker container** is due to simplicity and performance. If the system has for example 7 services, that would required up to 7 databse containers, and for each new one added a potential new database container would be needed.

For development this could increase my cpu and memory usage drastically. And, for a project like this, that won't go into production the overhead of multiple containers for the sake of boundry limitation is not worth it in my opinion. Also, it's possible to restrict access to services from specific databases by using **roles** and **users** which can, at least, define some access boundries.

## Consequences
1. Creating new databases is simple and straighforward, just requiring a couple of statements in the creation script.
2. Small overhead from new databases.
3. All services are coupled to the DBMS container.
4. If the database container fails all other services are compromised.
5. Increased load for one service can affect others, which is a consequence of their coupling.
 