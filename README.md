# Dockerized React App Deployment

This project provides a Dockerized setup for deploying a React application using Vite.

## Features

- **Dockerized React App**: Runs the Vite-based React app in a container.
- **Custom Versioning**: Supports tagging versions using Git.
- **Push to Docker Registry**: Deployable to a personal Docker registry.
- **Custom Container Naming**: Run containers with specific names.

## Prerequisites

Ensure you have the following installed:

- [Docker](https://www.docker.com/get-started)

## Build and Push Docker Image

### **1. Clone the Repository**

```sh
git clone https://github.com/BhaskarDeb2000/react-docker.git
cd react-docker
```

### **2. Build Docker Image with Versioning**

```sh
docker build -t bhaskardeb120/react-docker:v1.0.0 .
```

### **3. Push Image to Docker Registry**

```sh
docker push bhaskardeb120/react-docker:v1.0.0
```

## Run Container with Custom Name

To run the container with a custom name:

```sh
docker run --name react-app -p 3000:3000 bhaskardeb120/my-app:$VERSION
```

For detached mode (running in the background):

```sh
docker run -d --name react-app -p 3000:3000 bhaskardeb120/my-app:$VERSION
```

## Managing Containers

Check running containers:

```sh
docker ps
```

Stop the running container:

```sh
docker stop react-app
```

Remove the container:

```sh
docker rm react-app
```

## Dockerfile Overview

```dockerfile
FROM node:20-alpine3.18

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["npm", "run", "preview"]
```
