# Getting started
This guide assumes you have **docker engine** installed on your machine. If you don't, install it from the [official website](https://www.docker.com/get-started/).

## Table of contents
- [Pull from docker hub (recommended)](#pull-from-docker-hub-recommended)
- [Build it locally](#build-it-locally)
- [Development](#development)

## Pull from docker hub (recommended)
A list of releases can be found here:
[]

Once you've choosen a version execute the commands:
```bash
git clone path
cd infraestructure
docker compose -f compose.prod.yaml up
```

Compose will pull the correct tagged images from docker hub and instantaite the containers with their proper configuration.

Once all services are running the front-end client will be exposed under `localhost:4201`.

To stop the execution run:
```bash
docker compose down
```

## Build it locally
If you don't want to download the images from the repository you can build them on your machine. This is also useful if you want to change any configuration, but be aware that doing so might lead to unexpected bugs if not done properly.

Because the application is built as a distribuited system there's a good number of independent services, each with it's own repository, therefore you need to clone every single one and make it visible to compose. Doing this manually is brittle and error-prone, so there's a script to facilitate this process.

Choose a tagged version and clone it using:

```bash
git clone path
cd infraestructure
chmod +x build.sh
./build.sh
```

The script will clone all relevant repositories for the tagged version and place then at the root of `docker-compose.xml`.

After this you can run:
```bash
docker compose up
```

Once all services are running the front-end client will be exposed under `localhost:4201`.

To stop the execution run:
```bash
docker compose down
```

## Development
This section discuss how to set up the environment for the development. Most of it is just for me, Wilson, as I'm the only person working on this project. Regardless, if you want to know why the development mode was setup this way check out this [ADR-006: Docker compose choice](../docs/adr/ADR-006-docker-compose-choice.md).

Clone the infrastructure repository: 
```bash
git clone git@github.com:inkwell-store/inkwell-store.git
```

On root create a new folder called `services`:
```bash
mkdir services
```

Inside `services` you should put the repositories for the services. This should be the folder structure, because inside `infrastructure` there's a couple of compose files that, when combined, instantiate all containers and these files use relative paths that target the folder `services`.

As of now there are two types of development environments: one that uses **h2** and one that uses **postgresql**. These environments are created by using multiple compose files that, when executed in the *correct order*, create the full configuration. Either way, for both of these envivironments, when all containers are running, you might access:

* The API Gateway is available at `localhost:8080` 
* An Angular client is available at `localhost:4200`
* Rabbitmq UI tool is available at: `localhost:15672`

### H2 environment
H2 gives an in-memory database to quickly test new features.

To build the project using this configuration run:
```bash
docker compose -f compose.yaml -f compose.dev.yaml -f compose.dev.h2.yaml up
```

To shutdown the containers run:
```bash
docker compose -p inkwell-store down
```

### Postgresql environment
It's useful especially for testing flyway's migrations, database configuration and integrations. To know more about the DBMS setup check out [ADR-001: Multiple databases in single container](../docs/adr/ADR-001-multiple-databases-in-single-container.md)

To build the project using this configuration run:
```bash
docker compose -f compose.yaml -f compose.dev.yaml -f compose.dev.postgresql.yaml up
```

Since there's a postgresql Adminer will be available at `localhost:8079`.

To shutdown the containers run:
```bash
docker compose -p inkwell-store down
```