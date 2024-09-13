# Docker - Part 3

## **1. Docker Documentation Command-Line Reference**
To search and explore all Docker commands, use the official [Docker CLI Reference](https://docs.docker.com/engine/reference/commandline/). It provides a complete list of commands and their usage for quick reference.

---

## **2. Direct Container Access for Developers**

### **Accessing a Container Using SSH:**

Developers can access a container directly using **OpenSSH** with port forwarding. This method allows secure, remote access to the container.

### **Steps to Create an OpenSSH Container:**

1. **Create an OpenSSH container with port forwarding:**
   ```bash
   docker run -itd -p "2323:22" --name sshaccess openssh_image
   ```

2. **Connect using PuTTY:**
   - Enter the container's IP address and port (`2323`).
   - Log in with the username and password defined in the Dockerfile for the `openssh_image`.

---

## **3. Real-Life Scenario: Website Logs Monitoring**

### **Scenario:**
You need to provide a monitoring person with access to the production website logs without giving full control of the container. How can you achieve this?

### **Solution:**
Give the person read-only access to the logs by syncing the production container’s logs to the SSH container.

### **Steps:**

1. **Create a web server container (httpd) with log volume:**
   ```bash
   docker run -itd --name mywebserver1 -p "80:80" -v "/usr/local/apache2/logs" httpd
   ```

2. **Create an OpenSSH container and sync the logs from the webserver:**
   ```bash
   docker run -itd -p "2323:22" --volumes-from mywebserver1:ro sshaccess
   ```

3. **Connect to the SSH container via PuTTY:**
   - Use the container's IP and port (`2323`).
   - Access the logs in a read-only format (no modifications allowed).

The `--volumes-from mywebserver1:ro` flag ensures the logs are synced as read-only.

---

## **4. Monitoring Container Performance**

Use the `docker stats` command to view real-time performance metrics of containers, including CPU, memory, and network usage.

```bash
docker stats
```

---

## **5. Linking Containers**

### **Container Linking Example:**

To link a webserver container with a MySQL container (for example, WordPress using MySQL), use the `--link` option.

### **Steps:**

1. **Run a MySQL container:**
   ```bash
   docker run -itd -e MYSQL_ROOT_PASSWORD=12345678 --name db mysql:5.5
   ```

2. **Run a WordPress container linked to the MySQL container:**
   ```bash
   docker run -itd --name mywebserver --link db:mysql -p "80:80" wordpress
   ```

Here, the WordPress container (`mywebserver`) is linked to the MySQL container (`db`), allowing seamless interaction between the two services.

---

## **6. Docker Parameters Breakdown**

Common Docker parameters used in container management:

- **-p**: Publish container ports to the host.
- **--name**: Assign a custom name to the container.
- **-e**: Set environment variables (e.g., passwords).
- **-v**: Bind mount a directory from the host into the container.
- **--mount**: Mount volumes or directories with more advanced options.
- **--volumes-from**: Mount volumes from another container.
- **--link**: Link containers together for inter-container communication.

---

## **7. Docker Compose**

### **What is Docker Compose?**
Docker Compose allows you to define and manage multi-container Docker applications using a `docker-compose.yml` file.

### **Setting up WordPress and MySQL with Docker Compose:**

1. **Create a `docker-compose.yml` file:**
   ```yaml
   version: '3'
   services:
     db:
       image: mysql:5.5
       environment:
         MYSQL_ROOT_PASSWORD: 12345678
     wordpress:
       image: wordpress
       ports:
         - "80:80"
       environment:
         WORDPRESS_DB_HOST: db:3306
         WORDPRESS_DB_PASSWORD: 12345678
       depends_on:
         - db
   ```

2. **Run the containers using Docker Compose:**
   ```bash
   docker-compose up -d
   ```

3. **Check running containers:**
   ```bash
   docker-compose ps
   ```

With this setup, the WordPress container is linked to the MySQL container, and both services run in the background.

---

## **8. Docker Networking**

### **Viewing Docker Networks:**

To view all networks in Docker, use the command:
```bash
docker network ls
```

Docker automatically creates default networks, but you can also create custom networks to better organize container communication.

---

This **Docker Part 3** guide provides clear explanations of advanced Docker concepts like direct container access, syncing logs, container linking, and using Docker Compose for multi-container applications.

## Start learn and share it and give a start to this repo.