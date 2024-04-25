# Deploying-kevintsafack.live-with-GitHub-Actions

This project is here to demonstrates a continuous integration and deployment (CI/CD) pipeline for deploying a React application (
kevintsafack.live) using GitHub Actions.

## Key Features:
- Automated build and push of Docker image to Docker Hub on main branch push.
- Secure storage of credentials using GitHub secrets (username/token for Docker Hub, server credentials).
- Deployment to a remote server using SSH action with a command timeout for development environment.

## Workflow Steps

- Checkout: The first step checks out the repository code.
- Login to Docker Hub: The workflow authenticates with Docker Hub using the provided credentials (DOCKERHUB_USERNAME and DOCKERHUB_TOKEN secrets).
- Set up Docker Buildx: This step sets up the Docker Buildx environment, which allows for building multi-platform Docker images.
- Docker meta: This step generates metadata for the Docker image, including the image name (${{ secrets.DOCKERHUB_USERNAME }}/kevinportfolio) and the tag (latest).
- Build and push: The workflow builds the Docker image based on the Dockerfile in the repository and pushes the image to Docker Hub with the generated tags.
- Deploy to server: In this step, the workflow establishes an SSH connection with the remote server using the provided credentials (SERVER_HOST, SERVER_USERNAME, and SERVER_SSH_KEY secrets). It then executes a series of commands on the server:
Stops any running containers
Prunes the Docker system to remove unused resources
Runs a new container using the recently pushed Docker image, mapping port 3000 of the container to the host
