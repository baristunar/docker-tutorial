# Docker Tutorial - Node.js API

This project demonstrates how to containerize a Node.js Express API using Docker.

## Table of Contents

- [Project Structure](#project-structure)
- [Features](#features)
- [API Endpoints](#api-endpoints)
- [Requirements](#requirements)
- [Installation and Setup](#installation-and-setup)
  - [Using Docker Hub Image](#1-using-docker-hub-image-api-only---fastest)
  - [Using Docker Compose](#2-using-docker-compose-recommended-for-development)
  - [Manual Docker Build](#3-manual-docker-build)
- [Access](#access)
- [Development](#development)
- [Docker Commands](#docker-commands)
- [Technologies](#technologies)
- [Port Information](#port-information)
- [Notes](#notes)
- [What I Learned](#what-i-learned)

## Project Structure

```
docker-tutorial/
├── api/
│   ├── app.js              # Express server
│   ├── package.json        # Node.js dependencies
│   └── Dockerfile         # Docker configuration
├── docker-compose.yaml    # Multi-container orchestration
└── README.md             # This file
```

## Features

- **Express.js** RESTful API
- **CORS** support
- **Nodemon** with hot reload (development)
- **Docker** containerization
- **Docker Compose** orchestration

## API Endpoints

- `GET /` - Returns a list of blog posts

### Example Response:
```json
[
  {
    "id": "1",
    "title": "Book Review: The Name of the Wind"
  },
  {
    "id": "2", 
    "title": "Game Review: Pokemon Brillian Diamond"
  },
  {
    "id": "3",
    "title": "Show Review: Alice in Borderland"
  }
]
```

## Requirements

- Docker
- Docker Compose

## Installation and Setup

### 1. Using Docker Hub Image (API Only - Fastest)

```bash
# Pull the pre-built API image from Docker Hub
docker pull baristunardev/myapi-hello-docker

# Run the API container
docker run --name api_container -p 4000:4000 --rm baristunardev/myapi-hello-docker
```

**Note:** This option only runs the API service. For the full project with myblog, use options 2 or 3.

### 2. Using Docker Compose (Recommended for Development)

```bash
# Clone the project
git clone https://github.com/baristunar/docker-tutorial
cd docker-tutorial

# Build and run containers
docker-compose up --build

# Run in background
docker-compose up -d --build
```

### 3. Manual Docker Build

```bash
# Navigate to API folder
cd api

# Build Docker image
docker build -t myapp .

# Run container (development mode)
docker run --name api_container -p 4000:4000 --rm \
  -v $(pwd):/app \
  -v /app/node_modules \
  myapp
```

## Access

After running the API, you can access it at:

- **API:** http://localhost:4000

## Development

### Hot Reload

Thanks to Nodemon, your code changes are automatically detected and the server restarts.

### Volume Mounting

- `./api:/app` - Syncs code changes with the container
- `/app/node_modules` - Prevents node_modules from mixing with host

## Docker Commands

```bash
# Stop containers
docker-compose down

# View logs
docker-compose logs -f

# Connect to container shell
docker exec -it api_c sh

# Clean up images
docker image prune -a

# Clean up everything (DANGER: Removes all Docker data!)
docker system prune -a --volumes -f

# Step by step cleanup
docker stop $(docker ps -aq)           # Stop all containers
docker rm $(docker ps -aq)             # Remove all containers
docker rmi -f $(docker images -aq)     # Remove all images
docker volume prune -f                 # Remove all volumes
docker network prune -f                # Remove all networks
```

## Technologies

- **Node.js** v17
- **Express.js** v5.1.0
- **CORS** v2.8.5
- **Nodemon** (development)
- **Docker** & **Docker Compose**

## Port Information

- **API:** 4000 (Host) → 4000 (Container)

## Notes

- Use `CMD ["node", "app.js"]` for production
- `CMD ["npm", "run", "dev"]` is used for development
- Alpine Linux base image is used to optimize image size

## What I Learned

Through this Docker tutorial project, I gained hands-on experience with:

### Docker Fundamentals
- **Dockerfile creation** - Writing efficient multi-stage builds
- **Image optimization** - Using Alpine Linux to reduce image size
- **Container management** - Running, stopping, and cleaning up containers
- **Volume mounting** - Syncing local code with container for development

### Development Workflow
- **Hot reload setup** - Configuring Nodemon with `-L` flag for Docker
- **Environment separation** - Different commands for development vs production
- **Port mapping** - Exposing container ports to host system

### Docker Compose
- **Multi-container orchestration** - Managing API and other services
- **Service dependencies** - Linking containers in a network
- **Volume management** - Handling node_modules and code synchronization

### Best Practices
- **Layer caching** - Copying package.json first for better build performance
- **Clean builds** - Using `--build` flag to ensure fresh images
- **Resource cleanup** - Proper container and image management

### Docker Hub Integration
- **Image tagging** - Understanding semantic versioning and tag strategies
- **Registry push/pull** - Publishing and distributing containerized applications
- **Public repositories** - Sharing projects with the developer community

This project served as a practical introduction to containerization concepts and modern deployment workflows.
