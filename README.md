# Microservice App - PRFT Devops Training

This is the application you are going to use through the whole traninig. This, hopefully, will teach you the fundamentals you need in a real project. You will find a basic TODO application designed with a [microservice architecture](https://microservices.io). Although is a TODO application, it is interesting because the microservices that compose it are written in different programming language or frameworks (Go, Python, Vue, Java, and NodeJS). With this design you will experiment with multiple build tools and environments. 

## Components
In each folder you can find a more in-depth explanation of each component:

1. [Users API](/users-api) is a Spring Boot application. Provides user profiles. At the moment, does not provide full CRUD, just getting a single user and all users.
2. [Auth API](/auth-api) is a Go application, and provides authorization functionality. Generates [JWT](https://jwt.io/) tokens to be used with other APIs.
3. [TODOs API](/todos-api) is a NodeJS application, provides CRUD functionality over user's TODO records. Also, it logs "create" and "delete" operations to [Redis](https://redis.io/) queue.
4. [Log Message Processor](/log-message-processor) is a queue processor written in Python. Its purpose is to read messages from a Redis queue and print them to standard output.
5. [Frontend](/frontend) Vue application, provides UI.

## Architecture

Take a look at the components diagram that describes them and their interactions.
![microservice-app-example](/arch-img/Microservices.png)

# Microservices Project Documentation

## General Architecture

The system follows a **microservices-based architecture**, structured as a **monorepo**, consisting of five core services developed in-house and two supporting services: **Zipkin** for distributed tracing and **Redis** for caching management.

---

## CI/CD with GitHub Actions

### Microservice Pipelines

Each microservice has an independent pipeline configured with **GitHub Actions**, performing the following tasks:

- When a **push or pull request is made to the `dev` branch**, the pipeline is triggered to build the Docker image and validate that everything works correctly.
- When a **merge to `dev`** occurs, a Docker image is built and published to **Azure Container Registry** with a **random tag**.
- When a **merge to `master`** occurs, a new Docker image is built and published with the **`latest` tag**, representing the stable and updated version.

### Deployment Pipeline

An additional pipeline is responsible for deploying the application. This pipeline:

- Is triggered **only if any of the microservice pipelines have completed successfully with new changes**.
- Connects via **SSH** to an **Azure virtual machine**.
- Executes a script that deploys all services using **Docker Compose**.

---

## Docker Compose for Deployment

The `docker-compose.yml` file defines the runtime environment with the following components:

- **7 containers**: 5 internal microservices + Zipkin + Redis.
- **Docker images**: pulled from Azure Container Registry.
- Defined **environment variables**, **exposed ports**, and **startup dependencies** for each service.
- Deployment is performed on the **virtual machine**, which is already authenticated with the container registry.

---

## Deployment Virtual Machine

The virtual machine:

- Is configured with credentials to access the **Azure Container Registry**.
- Exposes the **necessary external ports** so the deployed services can be accessed from local or testing environments.
- Executes the `docker-compose up -d` command from the pipeline to keep containers running and up to date.

---

## Project Status

✔️ Continuous Integration  
✔️ Automated Deployment  
✔️ Infrastructure on Azure  
✔️ Monitoring with Zipkin  
✔️ Caching with Redis
