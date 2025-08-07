# Docker Tutorial - Node.js API

This project demonstrates how to containerize a Node.js Express API using Docker.

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

### 1. Using Docker Compose (Recommended)

```bash
# Clone the project
git clone https://github.com/baristunar/docker-tutorial
cd docker-tutorial

# Build and run containers
docker-compose up --build

# Run in background
docker-compose up -d --build
```

### 2. Manual Docker

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
