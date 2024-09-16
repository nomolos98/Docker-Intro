# Docker Image and Container Creation with NGINX

This guide demonstrates how to create a Docker image, run a container using NGINX, and push your custom image to Docker Hub. You will also learn how to serve a static web page using Docker.

## Introduction to Docker Images ads Docker Hub

Docker images are the fundamental units for creating containers. These images are lightweight, portable, and self-contained packages that include everything necessary to run an application: code, runtime, libraries, and system tools. Images are created using a set of instructions called the Dockerfile.

Docker Hub is a cloud-based repository that hosts a vast collection of Docker images.

## Dockerfile
A Dockerfile is a plaintext configuration file that contains instructions for building a Docker image. It specifies the environment for your application, including the base image, the working directory, files to copy, dependencies to install, and runtime configurations.

## Creating a Dockerfile

In this example, we use the official NGINX image to serve a static HTML file. NGINX is a high-performance web server and reverse proxy. Here's how to create a Dockerfile:

1. Create a file named `Dockerfile` in your project directory.
2. Add the following code to the `Dockerfile`:

    ```dockerfile
    # Use the official NGINX base image
    FROM nginx:latest

    # Set the working directory in the container
    WORKDIR /usr/share/nginx/html/

    # Copy the local HTML file to the NGINX default public directory
    COPY index.html /usr/share/nginx/html/

    # Expose port 80 to allow external access
    EXPOSE 80

    # No CMD required as NGINX has a default command to run the server
    ```

3. Create an `index.html` file in the same directory as your Dockerfile:

    ```bash
    echo "Welcome to Docker Image and Container Creation with NGINX" > index.html
    ```

4. Build the Docker image from the Dockerfile:

    ```bash
    docker build -t my-nginx-image .
    ```
![image](https://github.com/user-attachments/assets/adb28dc9-3bdb-4577-af05-658b2046a788)
![image](https://github.com/user-attachments/assets/5f5fe915-0676-4e3b-b549-37391031cc0c)

## Running a Container

After building the image, run a container based on the custom NGINX image we created with dockerfile:

```bash
docker run -p 8080:80 my-nginx-image
```
![image](https://github.com/user-attachments/assets/3a54475c-279c-48f4-ae13-8cd8da12115e)
This command maps port 8080 on your host machine to port 80 on the container where the NGINX server is running.

Use **docker ps -a** to see list of available running containers
![image](https://github.com/user-attachments/assets/59cdac3d-9a0e-4e21-8dfc-be3cb948206b)

Use the **docker start** to start a stopped container
![image](https://github.com/user-attachments/assets/0ea89b4f-cdfd-44aa-a5d7-665fa7c6b781)

