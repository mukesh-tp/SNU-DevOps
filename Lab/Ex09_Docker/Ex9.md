# DevOps Lab - Mukesh T P

## Exercise 10

### Exploring Containerization and Application Deployment with Docker

### Step 1: Install Docker (Cask Version)

Since you want the cask version of Docker (which provides the Docker Desktop app):

1. Open the terminal on your MacBook.
   ![1-1](../photos/Ex9/1-1.png?raw=true)
2. Run the following command to install Docker via Homebrew:

   ```bash
   brew install --cask docker
   ```

   ![1-2](../photos/Ex9/1-2.png?raw=true)

3. Once Docker is installed, open Docker from your Applications folder to start Docker Desktop.

   **Note:** You might be asked to provide permissions or log in to a Docker account.
   ![1-3](../photos/Ex9/1-3.png?raw=true)

### Step 2: Create a Simple HTML Page

1. Open a terminal or use Finder to create a new directory for the project:

   ```bash
   mkdir ~/docker-apache-server
   cd ~/docker-apache-server
   ```

   ![2-1](../photos/Ex9/2-1.png?raw=true)

2. Create the `index.html` file with a simple HTML message:

   ```bash
   echo "Hello, Docker!" > index.html
   ```

   This HTML file will be served by your Apache web server.
   ![2-2](../photos/Ex9/2-2.png?raw=true)

### Step 3: Create a Dockerfile

1. In the same directory as `index.html`, create a `Dockerfile`:

   ```bash
   touch Dockerfile
   ```

   ![3-1](../photos/Ex9/3-1.png?raw=true)

2. Open the `Dockerfile` with your preferred text editor (e.g., `nano`, `vim`, or use a code editor like VS Code), and add the following content:

   ```Dockerfile
   # Use the official Apache image from Docker Hub
   FROM httpd:2.4

   # Copy your custom HTML file to the Apache web server document root
   COPY index.html /usr/local/apache2/htdocs/
   ```

   ![3-2](../photos/Ex9/3-2.png?raw=true)

### Step 4: Build the Docker Image

1. Build the Docker image using the following command:

   ```bash
   docker build -t my-apache-server .
   ```

   Replace `my-apache-server` with a suitable name if you prefer.
   ![4-1](../photos/Ex9/4-1.png?raw=true)

### Step 5: Run the Docker Container

1. Run the Docker container with the following command:

   ```bash
   docker run -p 8080:80 -d my-apache-server
   ```

   This maps port 80 of the container to port 8080 on your host machine and runs the container in detached mode.
   ![5-1](../photos/Ex9/5-1.png?raw=true)

### Step 6: Access Your Apache Web Server

1. Open your web browser and go to:

   ```text
   http://localhost:8080
   ```

   You should see the "Hello, Docker!" message from the `index.html` file served by the Apache web server inside the Docker container.
   ![6-1](../photos/Ex9/6-1.png?raw=true)

### Step 7: Cleanup

1. To stop the running container, first list the running containers:

   ```bash
   docker ps
   ```

   Note the `<container_id>` of your running container, and stop it using:

   ```bash
   docker stop <container_id>
   ```

   ![7-1](../photos/Ex9/7-1.png?raw=true)

2. Optionally, remove the container and the Docker image:

   ```bash
   docker rm <container_id>
   docker rmi my-apache-server
   ```

   ![7-2](../photos/Ex9/7-2.png?raw=true)
