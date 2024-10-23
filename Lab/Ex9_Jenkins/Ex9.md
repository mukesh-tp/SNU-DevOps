# DevOps Lab - Mukesh T P

## Exercise 9

### Applying CI/CD Principles to Web Development Using Jenkins, Git, and Local HTTP Server

### Step 1: Set Up the Web Application and Local HTTP Server

1. **Create a Basic Web Application**:
   - In your project directory, create a simple HTML page to simulate a web app:

     ```bash
     mkdir ~/my-web-app
     cd ~/my-web-app
     echo "<html><body><h1>My Web App</h1></body></html>" > index.html
     ```

   ![1-1](../photos/Ex9/1-1.png?raw=true)

2. **Start the Python HTTP Server**:
   - Run the following command to start a local HTTP server:

     ```bash
     python3 -m http.server 8000
     ```

   - This serves the content of the current directory (in this case, `~/my-web-app`) on `http://localhost:8000`.
   ![1-2](../photos/Ex9/1-2.png?raw=true)

3. **Test the Local HTTP Server**:
   - Open a browser and go to `http://localhost:8000`. You should see the content of `index.html` displayed.
   ![1-3](../photos/Ex9/1-3.png?raw=true)

### Step 2: Set Up a Git Repository

1. **Create a Repository on GitHub**:
   - Go to GitHub and create a new repository (or use an existing one).
   ![2-1](../photos/Ex9/2-1.png?raw=true)

2. **Clone the Repository Locally**:

   ```bash
   cd ~/my-web-app
   git init
   git remote add origin <your-git-repo-url>
   git add index.html
   git commit -m "Initial commit"
   git push -u origin main
   ```

   ![2-2](../photos/Ex9/2-2.png?raw=true)

### Step 3: Install and Configure Jenkins

1. **Install Jenkins (using Homebrew)**:

   ```bash
   brew install jenkins
   ```

   ![3-1](../photos/Ex9/3-1.png?raw=true)

2. **Start Jenkins**:

   ```bash
   brew services start jenkins
   ```

   ![3-2](../photos/Ex9/3-2.png?raw=true)

3. **Access Jenkins**:
   - Open `http://localhost:8080` in your browser.
   - Unlock Jenkins using the following command to get the admin password:

     ```bash
     cat /Users/mukeshtp/.jenkins/secrets/initialAdminPassword
     ```

   - Complete the Jenkins setup by installing recommended plugins and creating an admin account.
   ![3-3](../photos/Ex9/3-3.png?raw=true)

### Step 4: Create a Jenkins Freestyle Project

1. **Create a New Jenkins Job**:
   - In Jenkins, go to the dashboard → "New Item" → Enter a name → Select "Freestyle Project" → Click "OK."
   ![4-1](../photos/Ex9/4-1.png?raw=true)

2. **Configure Source Code Management**:
   - In the job configuration, go to the "Source Code Management" section.
   - Select "Git" and enter the URL of your GitHub repository (e.g., `https://github.com/yourusername/your-repo.git`).
   - If necessary, add credentials (such as a GitHub personal access token) for Jenkins to access your repository.
   ![4-2](../photos/Ex9/4-2.png?raw=true)

3. **Enable Webhook Trigger**:
   - Under "Build Triggers," check the box for "GitHub hook trigger for GITScm polling."
   ![4-3](../photos/Ex9/4-3.png?raw=true)

### Step 5: Set Up the Build Steps (Execute Shell)

1. **Configure the Build Section**:
   - In the "Build" section of the job configuration, click "Add build step" → Select "Execute shell."

2. **Define the Shell Commands**:
   - In the "Command" field, add the following commands to pull the latest code, clean the directory, and deploy it to the Python server:

     ```bash
     # Clean the directory where the server serves the files
     rm -rf ~/my-web-app/*

     # Pull the latest code from the repository
     git clone https://github.com/yourusername/your-repo.git ~/my-web-app/

     # (Re)start the Python HTTP server
     pkill -f "python3 -m http.server"  # Stop any running server
     cd ~/my-web-app
     nohup python3 -m http.server 8080 &
     ```

   ![5-1](../photos/Ex9/5-1.png?raw=true)

### Step 6: Set Up a Webhook in Git Repository

Since Jenkins is running locally, GitHub cannot directly communicate with Jenkins via localhost. To solve this, we will use **ngrok** to expose your local Jenkins instance to the internet temporarily.

#### Install and Set Up ngrok

1. **Install ngrok**:
   - If ngrok is not already installed, you can install it using Homebrew:

     ```bash
     brew install ngrok
     ```

   ![6-1](../photos/Ex9/6-1.png?raw=true)

2. **Start ngrok**:
   - Run ngrok on the Jenkins port (`8080`):

     ```bash
     ngrok http 8080
     ```

   - ngrok will output a public URL that tunnels to your local Jenkins instance. The output will look like this:

     ```text
     Forwarding        http://randomstring.ngrok.io -> http://localhost:8080
     ```

   ![6-2](../photos/Ex9/6-2.png?raw=true)

3. **Copy the Public URL**:
   - Copy the `http://randomstring.ngrok.io` URL for the next step.

#### Set Up Webhook in GitHub

1. **Create a Webhook in GitHub**:
   - Go to your GitHub repository → "Settings" → "Webhooks" → "Add webhook."

2. **Configure the Webhook**:
   - In the "Payload URL" field, enter the public `ngrok` URL followed by `/github-webhook/`:

     ```bash
     http://randomstring.ngrok.io/github-webhook/
     ```

   - Set the "Content type" to `application/json`.
   ![6-3](../photos/Ex9/6-3.png?raw=true)

3. **Save the Webhook**.

### Step 7: Trigger the CI/CD Pipeline

1. **Push Changes to GitHub**:
   - Make changes to your `index.html` or other files, commit, and push:

     ```bash
     echo "<html><body><h1>Updated Web App</h1></body></html>" > index.html
     git add index.html
     git commit -m "Updated the web app"
     git push origin main
     ```

   ![7-1](../photos/Ex9/7-1.png?raw=true)

2. **Automatic Jenkins Trigger**:
   - The GitHub webhook will notify Jenkins through the ngrok URL, triggering the pipeline.
   - Monitor the build progress on the Jenkins dashboard.

### Step 8: Verify the CI/CD Pipeline

1. **Visit the Local HTTP Server**:
   - After Jenkins finishes the build and deployment, open your browser and visit `http://localhost:8000`.
   - You should see the updated web application.
   ![8-1](../photos/Ex9/8-1.png?raw=true)

### Optional

- If you want Jenkins to deploy to a staging or production server later, you can enhance the pipeline by adding additional stages to your build process.
