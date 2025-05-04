# Docker Usage Guide

This README provides instructions for building, tagging, and pushing the ansible environment container.

## Building the Container

Build the Docker image locally:

```bash
docker build -t personal_ansible -f docker/Dockerfile .
```

## Publishing to GitHub Container Registry

Login to GitHub Container Registry:

```bash
docker login ghcr.io -u geugenm
```

Tag the local image for the registry:

```bash
docker tag personal_ansible ghcr.io/geugenm/personal-ansible:latest
```

Push the image to the registry:

```bash
docker push ghcr.io/geugenm/personal-ansible:latest
```

## Using the Container

Pull the container from GitHub Container Registry:

```bash
docker pull ghcr.io/geugenm/personal-ansible:latest
```

Run the container:

```bash
docker run -it --rm -v $(pwd):/workspace ghcr.io/geugenm/personal-ansible:latest
```
