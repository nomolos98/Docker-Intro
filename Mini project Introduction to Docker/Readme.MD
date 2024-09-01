# Docker Overview

## Project Goals

By the end of this course, you should aim to achieve the following:

1. The concept of containers, their isolation, and their role in packaging applications.
2. Familiarize with key Docker features, commands, and best practices.
3. Comprehend how Docker containers contribute to resource efficiency compared to traditional virtual machines.
4. Learn how Docker ensures consistent application behavior across different development, testing, and production environments.
5. Master the techniques for quickly deploying and scaling applications using Docker.

## Getting Started With Docker

### Installing Docker

#### Step 1: Launch an Ubuntu Instance

First, launch an Ubuntu instance and connect to it.

#### Step 2: Add Docker's Official GPG Key

Before installing Docker Engine for the first time on a new host machine, it is necessary to configure the Docker repository. Following this setup, we can proceed to install and update Docker directly from the repository.

1. **Update the package list**:

    ```bash
    sudo apt-get update
    ```

    This command refreshes the package list on a Debian-based system, ensuring the latest software information is available for installation.

2. **Install essential packages**:

    ```bash
    sudo apt-get install ca-certificates curl gnupg
    ```

    This installs essential packages including certificate authorities, a data transfer tool (curl), and the GNU Privacy Guard for secure communication and package verification.

3. **Create a directory for keyring files**:

    ```bash
    sudo install -m 0755 -d /etc/apt/keyrings
    ```

    This command creates a directory (`/etc/apt/keyrings`) with specific permissions (0755) for storing keyring files, which are used for Docker's authentication.

4. **Download the Docker GPG key and save it**:

    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

    This downloads the Docker GPG key using `curl` and saves it in a secure format.

5. **Set read permissions for the Docker GPG key file**:

    ```bash
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    ```

    This sets read permissions for all users on the Docker GPG key file within the APT keyring directory.

#### Step 3: Add the Docker Repository

1. **Add the repository to APT sources**:

    ```bash
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

    This command creates a Docker APT repository configuration entry for the Ubuntu system, incorporating the system architecture and Docker GPG key, and then writes this configuration to the `/etc/apt/sources.list.d/docker.list` file.

2. **Update the package list again**:

    ```bash
    sudo apt-get update
    ```

3. **Install the latest version of Docker**:

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

4. **Verify that Docker has been successfully installed**:

    ```bash
    sudo systemctl status docker
    ```
![docimg1](https://github.com/user-attachments/assets/b3171a1f-d1ab-42c3-a7a7-26e240597ac2)
![systatus](https://github.com/user-attachments/assets/d9e4f285-d0f9-4f2d-959d-c4288dab77a7)

By default, after installing Docker, it can only be run by the root user or using `sudo`.

5. **Allow non-root user to run Docker commands**:

    ```bash
    sudo usermod -aG docker ubuntu
    ```

    After executing this command, you can run Docker commands without using superuser privileges. 

### Running the "Hello World" Container

#### Using the `docker run` Command

The `docker run` command is the entry point to execute containers in Docker. It allows you to create and start a container based on a specified Docker image.

1. **Run the "Hello World" container**:

    ```bash
    docker run hello-world
    ```
**Note:** When getting a permission denied error when trying to run the docker run hello-world command. This is likely because the current user does not have the necessary permissions to interact with the Docker daemon. Please run Docker commands with sudo to execute them with elevated privileges: sudo docker run hello-world

#### When you execute this command, Docker performs the following steps:

    - Pulls the Image**: Docker checks if the `hello-world` image is available locally. If not, it automatically pulls it from the Docker Hub.
    - Creates a Container**: Docker creates a container based on the `hello-world` image.
    - Starts the Container**: The container is started, and it executes the predefined command in the `hello-world` image, which prints a friendly message.

#### Verifying the Successful Execution

You can check if the image is now in your local environment with:

```bash
docker images
