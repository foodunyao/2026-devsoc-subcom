# Docker & Kubernetes Assessment Report

> [!TIP]
> Use this document to explain your design choices, optimisations and any challenges you faced.

## Dockerfile

<!-- TODO: (Optional) Explain any specific goals or design decisions -->

- I chose the base image to be node:lts-slim over alpine, due to the tradeoff between compatibility and performance
  over size.
- As of now, as corepack is still included in the active lts source for node is still v24, I have no need to npm install
  corepack. Thus, I can enable pnpm through corepack. However, in future node versions, another RUN instruction might be
  needed before the activation.
- package.json and the pnpm\*.yaml files are copied first to take advantage of Docker layer caching, as not need require
  pnpm install to run every single time source code is changed

### Forked repository

<!-- TODO: If you submitted your changes to a fork, replace with your forked repository -->

`https://github.com/your-username/academic-calendar-api`

## Kubernetes

<!-- TODO: Document your process for deploying Navidrome on Kubernetes -->

- There were a lot of random confusing errors due to previous deployments that I had forgotten to delete
- Using kompose to conver docker-compose.yml to the kubernetes yaml files did not expose the port to localhost. To
  resolve this, navidrome-service.yaml was edited to change the service type to NodePort
  - For public routing I think using the LoadBalancer service would work?
