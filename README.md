# Docker
Docker is a platform that allows you to build, run, and manage applications in isolated environments called **containers**. Containers package an application with all its dependencies, ensuring it works consistently across different systems.

# Container
A container is a lightweight, standalone, and executable unit of software that includes everything needed to run an application—such as the code, runtime, libraries, and system tools. Containers are isolated from each other and the host system, ensuring consistency across different environments (development, testing, production).

They're often compared to virtual machines but are much more efficient because they share the host system's operating system kernel.

# Why We Need Containers

1. **Consistency Across Environments**  
   - Containers package applications and their dependencies, ensuring they run the same way across systems (e.g., development, testing, production).  
   - Solves the "it works on my machine" problem.  

2. **Isolation**  
   - Containers isolate applications, preventing dependency conflicts and ensuring security and stability.  

3. **Portability**  
   - Containers are lightweight and portable, making it easy to move applications between systems or platforms (e.g., from on-premises to the cloud).  

4. **Efficiency**  
   - Containers share the host OS kernel, using fewer resources compared to virtual machines, which require separate OS installations.  

5. **Faster Deployment**  
   - Containers start quickly, enabling rapid deployment and scaling of applications.  

6. **Improved Scalability**  
   - Applications can be scaled horizontally by deploying multiple container instances easily.  

7. **Easier CI/CD Pipelines**  
   - Containers streamline continuous integration and deployment by providing consistent environments for building, testing, and deploying code.  

# Bare Metal vs Virtual Machines (VMs) vs Containers

| Feature              | **Bare Metal**                     | **Virtual Machines (VMs)**                 | **Containers**                          |
|----------------------|-------------------------------------|--------------------------------------------|-----------------------------------------|
| **Definition**       | Direct use of physical hardware.   | Runs on a hypervisor with separate OS for each VM. | Lightweight environments sharing the host OS kernel. |
| **Performance**      | Best performance, no overhead.     | Moderate performance, some overhead due to hypervisor. | Near-native performance, minimal overhead. |
| **Isolation**        | No isolation (shared hardware).    | Strong isolation with separate OS.         | Process-level isolation using namespaces and cgroups. |
| **Startup Time**     | Immediate (OS already running).    | Slow (full OS boot).                       | Very fast (seconds to milliseconds).    |
| **Resource Usage**   | Entire hardware dedicated.         | High (each VM has its own OS).             | Low (shared OS kernel, minimal footprint). |
| **Scalability**      | Limited by physical hardware.      | Moderate (requires more hardware).         | High (can run many containers on one host). |
| **Portability**      | Tied to specific hardware.         | Limited portability between hypervisors.   | Highly portable across systems supporting containers. |
| **Use Case**         | Performance-critical applications. | Running multiple OS instances on one host. | Microservices, cloud-native applications. |

# Building Blocks of Docker

1. **Docker Engine**  
   - The core of Docker that runs and manages containers. It includes:  
     - **Docker Daemon**: Handles container management, image building, and communication with the host.  
     - **Docker CLI**: Command-line interface for interacting with Docker.  

2. **Docker Image**  
   - A lightweight, read-only template that contains the application and its dependencies.  
   - Used to create containers.  

3. **Docker Container**  
   - A runnable instance of a Docker image.  
   - Provides an isolated environment for running applications.  

4. **Docker Hub**  
   - A public repository for storing and sharing Docker images.  
   - Includes official images and allows users to upload custom images.  

5. **Docker Compose**  
   - A tool for defining and managing multi-container applications using a YAML file.  
   - Simplifies running services together (e.g., a web app and its database).  

6. **Dockerfile**  
   - A text file with instructions to build a Docker image.  
   - Defines the application's environment and dependencies.  

7. **Docker Network**  
   - Provides communication between containers and the host system.  
   - Types include bridge, host, overlay, and custom networks.  

8. **Docker Volume**  
   - A mechanism for persisting data generated by containers.  
   - Allows sharing of data between containers and the host.  


# Docker Image layers

1. **What Are Image Layers?**  
   - Docker images are built in layers, where each layer represents a set of changes (e.g., adding files, installing dependencies, modifying configurations).  
   - Layers are immutable (cannot be changed) and are stacked to form the final image.  

2. **Base Layer**  
   - The first layer in an image, usually derived from a minimal OS or official base image (e.g., `ubuntu`, `alpine`).  
   - Other layers build on top of this.  

3. **Layer Caching**  
   - Docker uses layer caching to speed up image builds.  
   - If a layer has already been built and hasn't changed, Docker reuses it instead of rebuilding.  
   - Reduces build time and improves efficiency.  

4. **Layer Reuse**  
   - Layers are shared across multiple images if they use the same base and intermediate layers.  
   - Saves disk space by avoiding duplication.  

5. **Read-Only Layers**  
   - All layers in a Docker image are read-only.  
   - When a container runs, Docker adds a writable layer on top of the image layers, called the **container layer**.  

6. **Layered Structure Benefits**  
   - **Portability**: Layers can be shared across systems.  
   - **Efficiency**: Layer reuse reduces disk space and build times.  
   - **Version Control**: Changes are easy to track as each layer corresponds to a specific step in the `Dockerfile`.  

7. **Best Practices for Managing Layers**  
   - **Combine Commands**: Use multi-line instructions in the `Dockerfile` to minimize the number of layers.  
   - **Order Matters**: Place frequently changing instructions (e.g., adding application code) toward the end of the `Dockerfile` to maximize layer caching.  
   - **Use Small Base Images**: Start with lightweight base images (e.g., `alpine`) to keep images small.  

8. **Layer Storage**  
   - Layers are stored in Docker's storage backend (e.g., OverlayFS).  
   - They are identified by a unique hash.  

9. **Writable Layer in Containers**  
   - When running a container, changes made are stored in the writable layer.  
   - These changes are lost when the container is stopped unless persisted using volumes.  

10. **Removing Unused Layers**  
    - Use `docker system prune` to clean up unused layers and free up disk space.  




# Important Tips
1. Optimization build time from layers by moving node modules before the frequent code changes.
