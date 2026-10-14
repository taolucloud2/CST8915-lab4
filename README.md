# CST8915 Lab4: Introduction to Docker

- **Student Name**: Tao Lu
- **Student ID**: 41284860
- **Course**: CST8915 Full-stack Cloud-native Development
- **Semester**: Fall 2026

---

## [Demo Video](https://www.youtube.com/watch?v=EmLuq9fVdj4)

## Reflection Questions

### What are the main differences between a Docker image and a Docker container?

- A Docker image contains the code, runtime, and dependencies needed to run an application, and it is read-only. When we run an image, it becomes a Docker container. A container has its own writable layer on top of the image layers, so we can create or modify files inside it. However, these changes only happen in the container's writable layer and do not change the read-only image.

### Explain how Docker's layered architecture improves efficiency.

- Docker's layered architecture saves storage and speeds up builds. First, layers can be shared. If two images use the same base layers, Docker only stores those layers once on disk, and both images reuse them. Containers started from the same image also share the read-only image layers, so running many containers does not use much extra space. Second, layers are cached during builds. When we rebuild an image, Docker only rebuilds the layer that changed and the layers after it, and reuses the cached layers before it. This makes rebuilding much faster.

### Why does each container get its own writable layer?

- The image layers are read-only, so a running container needs a writable layer to create, modify, or delete files. Each container gets its own separate writable layer so that containers are isolated from each other. Changes made in one container do not affect other containers or the original image. This also allows many containers to safely share the same read-only image layers, which saves storage. When a container is removed, its writable layer is deleted, but the image stays unchanged and can be used to start new containers.

### What are the benefits of using Docker Compose over running containers individually?

- We can use a Docker Compose YAML file to manage several services together, including their networks, volumes, ports, and environment variables. Instead of running a separate `docker run` command for each container, we can start all the services with a single command, `docker compose up`, and stop them the same way with `docker compose down`. Compose also creates a shared network automatically, so the services can communicate with each other by using their service names. Because all the configuration is saved in one file, it is easy to share and to reproduce the same environment on another machine.
