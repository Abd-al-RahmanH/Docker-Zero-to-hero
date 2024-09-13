# Docker for Windows - Installation & Basics By ABDUL RAHMAN H

## Overview
Docker is used to run any application in containers, along with all the required libraries and dependencies.

---

### **Today’s Class Outline:**

- **Docker Image:** Similar to an AMI (Amazon Machine Image) – it’s a blueprint for containers.
- **Container:** Like an instance of the image – a running application with all the configurations.
- **Docker Hub:** A centralized location for all Docker images.
- **Dockerfile:** A set of instructions to create an image.

---

## **Step-by-Step Guide:**

### **1. Launch Ubuntu (with 15 GB storage)**

- Enable all TCP connections.
- Connect to the instance using PuTTY.
- Run the following commands:
  ```bash
  sudo apt-get update
  sudo apt install docker.io
  ```

### **2. Basic Docker Commands:**

- **Check available images:**
  ```bash
  docker images
  ```

- **Pull an image (e.g., httpd):**
  ```bash
  docker pull httpd
  ```

- **Check running containers:**
  ```bash
  docker ps
  ```

- **Run a container with port mapping (example: httpd):**
  ```bash
  docker run -itd -p "7070:80" httpd
  ```

- Open a browser and enter `IP_ADDRESS:7070` to access the container.

---

## **3. Running Multiple Containers:**

You can run multiple instances of the same container (e.g., httpd) by changing the port number:
```bash
docker run -itd -p "8080:80" httpd
```

---

## **4. Modify Files Inside a Container:**

- Enter the container:
  ```bash
  docker exec -it CONTAINER_ID /bin/bash
  ```

- Once inside, you can use the following commands:
  ```bash
  ls -lrt
  cd htdocs
  apt-get update
  apt install vim
  ```

---

## **5. Essential Docker Commands:**

- **List all containers (running and stopped):**
  ```bash
  docker ps -a
  ```

- **Start a container:**
  ```bash
  docker start CONTAINER_ID
  ```

- **Stop a container:**
  ```bash
  docker stop CONTAINER_ID
  ```

- **Remove a container:**
  ```bash
  docker rm CONTAINER_ID
  ```

- **Delete an image:**
  ```bash
  docker rmi IMAGE_NAME
  ```

- **Run a container with a custom name and port:**
  ```bash
  docker run -itd --name Masthan -p "4567:80" httpd
  ```

- **View logs of a container:**
  ```bash
  docker logs CONTAINER_ID
  ```

- **Inspect details of a container:**
  ```bash
  docker inspect CONTAINER_ID
  ```

- **Monitor resource usage of containers:**
  ```bash
  docker stats CONTAINER_ID
  ```

---

## **6. Creating and Sharing Docker Images:**

### **Steps to Create an Image of a Container:**

1. **Create an image from a running container:**
   ```bash
   docker commit CONTAINER_ID myimage:v1.0
   ```

2. **Check created images:**
   ```bash
   docker ps -a
   ```

### **How to Share Docker Images:**

1. **Save the image locally:**
   ```bash
   docker save -o /usr/local/myimagebackup.tar myimage:v1.0
   ```

2. **Load the image from the backup:**
   ```bash
   docker load -i /usr/local/myimagebackup.tar
   ```

3. **Push Image to Docker Hub:**
   - Create a Docker Hub account.
   - Log in:
     ```bash
     docker login
     ```

   - Tag the image:
     ```bash
     docker tag myimage:v1.0 rahman/httpd_vim-git
     ```

   - Push the image to Docker Hub:
     ```bash
     docker push rahman/httpd_vim-git
     ```

4. **To pull the image from Docker Hub:**
   ```bash
   docker pull rahman/httpd_vim-git
   ```

---

## **Task:**

- Practice Docker commands.
- Learn the difference between **Microservices** and **Monolithic services**.
- Try running IIS in a Linux container.

---

 