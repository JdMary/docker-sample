# docker-sample
## Diffrent methods of image creation:
1. Create an image from Scratch 
2. Create an image from a Dockerfile
3. Create an image from a Container

### Creating a Docker Image FROM Scratch  

Building Docker images **FROM scratch** means starting from an **empty base**, without any preinstalled OS, ensuring **lightweight, secure, and fully controlled** containerization.

#### Why use FROM scratch?  
- **Minimal size**
- **Enhanced security**
- **Full control over dependencies**

####  Example: Ultra-Lightweight Docker Image  

```dockerfile
FROM scratch  
COPY hello /  
CMD ["/hello"]
```

### Dockerfile: The Preferred Method for Building a Docker Image  

A **Dockerfile** is a script that defines step by step how to build a Docker image in an **automated, efficient, and reproducible** way. It acts as a **recipe**, ensuring consistency across deployments. 

#### Building an Image: `docker build`  
The essential command to create a Docker image:
```
docker build -t image_name path
```
1. Define the base image
```
FROM ubuntu:20.04
```
2. Set up the environment
```
LABEL maintainer="Jrad Mariem"
ENV APP_ENV=production
WORKDIR /app
```
3. Define the startup behaviour
  * The CMD command is the default command that will be executed but if an argument is entered when running the container it would ignore the CMD Statement 
  * The Entypoint is a base command which prioritary comparing it with CMD .
  
> [!NOTE] 
> **`ENTRYPOINT` vs. `--entrypoint` in Docker**
> - `ENTRYPOINT` (Dockerfile) sets a fixed command that runs by default.
>   ```dockerfile
>   ENTRYPOINT ["ping", "-c", "4"]
>   ```
>   Running `docker run my-image google.com` executes: `ping -c 4 google.com`.
> - `--entrypoint` (CLI) temporarily overrides `ENTRYPOINT`.
>   ```sh
>   docker run --entrypoint ls my-image
>   ```
>   Runs `ls` instead of `ping`. 
> - **Use `ENTRYPOINT`** for default behavior, **`--entrypoint`** for runtime overrides. 


```
CMD ["echo", "Hello, World!"]
ENTRYPOINT ["echo"]
```
4. Run commands during build which creates a temporary container and executes the command and from it an image will be created
```
RUN apt-get update && apt-get install -y python3
```

### Create a Docker Image from a Container  

Use `docker commit` to save a container’s current state as a new image. 

#### Syntax  
```
docker commit [container_id] [image_name:tag]
```

