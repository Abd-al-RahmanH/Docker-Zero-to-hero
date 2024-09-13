# Docker - Part 2

## **1. Volumes in Docker**

### **What is a Volume?**
A volume in Docker allows you to sync files between a folder on the host system and a folder inside the container. It ensures data persistence even when containers are deleted.

### **Syncing a Folder with a Volume:**

- **Create a directory on the host:**
  ```bash
  mkdir /root/html
  ```

- **Download the `httpd` image:**
  ```bash
  docker pull httpd
  ```

- **Create a container with volume binding:**
  ```bash
  docker run -itd -p "7070:80" -v "/root/html:/usr/local/apache2/htdocs/" httpd
  ```

- **Edit the container’s files:**
  - Enter the container:
    ```bash
    docker exec -it CONTAINER_ID /bin/bash
    ```
  - Any changes in `/usr/local/apache2/htdocs/` within the container will reflect in `/root/html` on the host.

- **Persistence:**  
  Even if the container is deleted, the data stored in the volume (`/root/html`) will remain.

---

## **2. Managing Docker Volumes**

### **Creating and Inspecting Volumes:**

- **List all volumes:**
  ```bash
  docker volume ls
  ```

- **Create a new volume:**
  ```bash
  docker volume create my-vol
  ```

- **Inspect the volume:**
  ```bash
  docker inspect my-vol
  ```

- **Find the mount point and navigate to the path.**

### **Using Volumes in Containers:**

- **Run a container using a volume:**
  ```bash
  docker run -itd --mount source=my-vol,target=/usr/local/apache2/htdocs -p "5050:80" httpd
  ```

You can create multiple containers and link them to the same volume for shared data access.

---

## **3. Dockerfile**

### **What is a Dockerfile?**
A Dockerfile is a script containing instructions to create an image. It automates the process of building a Docker image.

### **Steps to Create a Dockerfile:**

1. **Create a folder:**
   ```bash
   mkdir /root/test
   ```

2. **Create a Dockerfile in the folder:**
   ```bash
   vi Dockerfile
   ```

3. **Add the following content to the Dockerfile:**
   ```dockerfile
   FROM centos
   LABEL Name="abdul"
   RUN yum install httpd -y
   ```

4. **Build the Docker image:**
   ```bash
   docker build -t myimage:v1.0 /root/test
   ```

5. **Check available images:**
   ```bash
   docker images
   ```

You can rename the image or tag it with different versions for better management.

---

## **4. Understanding Key Docker Run Flags**

### **Detached Mode (`-d`)**
- **Detached mode (`-d`)** runs the container in the background. Without this flag, the container runs in the foreground.
  ```bash
  docker run -d httpd
  ```

### **Interactive Mode (`-i`)**
- **Interactive mode (`-i`)** keeps STDIN open, allowing you to interact with the container’s terminal.

### **Terminal Mode (`-t`)**
- **Terminal mode (`-t`)** allocates a pseudo-terminal, allowing you to run commands inside the container.

Example command combining all flags:
```bash
docker run -itd httpd
```

---

## **5. Docker Instructions:**

### **Common Dockerfile Instructions:**

- **FROM**: Base image to start from.
- **WORKDIR**: Set the working directory inside the container.
- **COPY**: Copy files from the host to the container.
- **ENTRYPOINT**: Set a default command that always runs.
- **CMD**: Provide default arguments to the `ENTRYPOINT`.

### **RUN Instruction:**
- **Shell form**: Executes the command in a shell.
  ```bash
  RUN yum install httpd
  ```

- **Exec form**: Executes the command directly without a shell.
  ```bash
  RUN ["yum", "install", "httpd"]
  ```

---

## **6. Cleaning Up Docker Containers**

- **Remove all stopped containers:**
  ```bash
  docker container prune
  ```

---

## **7. Important Default Docker Commands:**

- **Run a container in detached and interactive mode:**
  ```bash
  docker run -itd httpd
  ```

- **Execute a command inside a running container:**
  ```bash
  docker exec -it CONTAINER_ID /bin/bash
  ```

---

This **Docker Part 2** guide is organized with clear topics and explanations to help you understand Docker volumes, Dockerfiles, and essential commands.