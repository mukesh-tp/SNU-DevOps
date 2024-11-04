# DevOps Lab - Mukesh T P

## CIA 2: Create an End-to-End CI/CD Pipeline using AWS for a Node.js Application

---

### Step 1: Create an S3 Bucket for Deployment

1. **Log in to AWS** and navigate to [Amazon S3](https://s3.console.aws.amazon.com/s3/).
   ![1-1](../photos/CIA2/1-1.png?raw=true)

2. **Create an S3 Bucket**:
   - Click **Create bucket**.
   - **Bucket name**: Give it a unique name, like `my-nodejs-app-bucket`.
   - **Region**: Select a region near your users.
   - **Block Public Access Settings**:
     - If you need the application to be publicly accessible (e.g., for a frontend), uncheck **Block all public access** and confirm.
   - **Bucket versioning** (optional): Enable versioning if you want to keep multiple versions of your deployed files.
   - Click **Create bucket**.
   ![1-2](../photos/CIA2/1-2.png?raw=true)

### Step 2: Prepare Your GitHub Repository

1. **Initialize the Node.js Project**:
   - Open your terminal, navigate to your project directory, and run:

     ```bash
     npm init -y
     ```

   - This will create a `package.json` file. Add any dependencies you need, for example:

     ```bash
     npm install express
     ```

   - Create your project files, such as `index.js` or any frontend files.

2. **Create a GitHub Repository**:
   - Go to GitHub and create a new repository (e.g., `my-nodejs-app`).
   - Follow the instructions to push your local Node.js project to this repository.

3. **Create a `buildspec.yml` file**:
   - In your project root directory, add a file called `buildspec.yml` to define the build instructions for AWS CodeBuild. Here’s an example:

     ```yaml
     version: 0.2

     phases:
       install:
         commands:
           - npm install
       build:
         commands:
           - npm run build
     artifacts:
       files:
         - '**/*'
       base-directory: build # adjust if your output directory is different
     ```

### Step 3: Create an AWS CodePipeline

1. **Go to the CodePipeline Console**:
   - Navigate to [AWS CodePipeline](https://console.aws.amazon.com/codepipeline/).
   - Click **Create pipeline**.
   ![3-1](../photos/CIA2/3-1.png?raw=true)

2. **Configure Pipeline Settings**:
   - **Pipeline name**: Enter a name (e.g., `MyNodeAppPipeline`).
   - **Service role**: Select **New service role** or **Existing service role** if you have one already.
   - **Artifact store**: Choose **Amazon S3** and select an S3 bucket for storing pipeline artifacts (it can be the same as your deployment bucket or a different one).
   - Click **Next**.
   ![3-2](../photos/CIA2/3-2.png?raw=true)

### Step 4: Configure the Source Stage

1. **Choose Source Provider**: Select **GitHub**.
   ![4-1](../photos/CIA2/4-1.png?raw=true)

2. **Connect GitHub**:
   - Click **Connect to GitHub** to authorize AWS to access your GitHub account.
   - Select the repository you created in Step 2.
   - **Branch**: Select the branch (e.g., `main`) that you want to trigger the pipeline.
3. **Output Artifact Name**: Set an artifact name like `SourceArtifact`.
4. Click **Next**.

### Step 5: Configure the Build Stage (CodeBuild)

1. **Add a New Build Stage**:
   - Click **Add build stage** and select **AWS CodeBuild** as the provider.
   ![5-1](../photos/CIA2/5-1.png?raw=true)

2. **Create a New CodeBuild Project**:
   - Click **Create project**.
   - **Project name**: Name it (e.g., `NodeJsAppBuild`).
   - **Environment**:
     - **Environment image**: Select **Managed image**.
     - **Operating system**: Choose **Ubuntu**.
     - **Runtime**: Choose the Node.js runtime that matches your app.
     - **Service role**: Select **New service role** (or an existing role if you have one).
   - **Buildspec**: Select “Use a buildspec file” and ensure your `buildspec.yml` file is in the root directory of your repository.
   ![5-2](../photos/CIA2/5-2.png?raw=true)

3. **Additional Settings** (optional):
   - In **Build logs**, enable **CloudWatch** logs to see detailed build logs.

4. Click **Continue to CodePipeline** once the CodeBuild project is created.

5. **Output Artifact Name**: Set it to `BuildArtifact` or match the artifact name in `buildspec.yml`.

### Step 6: Configure the Deploy Stage (S3)

1. **Add Deploy Stage**:
   - Click **Add deploy stage** and select **Amazon S3**.
   ![6-1](../photos/CIA2/6-1.png?raw=true)

2. **Select the S3 Bucket**:
   - Choose the bucket you created in Step 1 (e.g., `my-nodejs-app-bucket`).

3. **Set Deployment Options**:
   - **Extract artifact**: Ensure this is checked if you want the files to be extracted.
   - **Output Artifact Name**: Match the name you set for your build output (e.g., `BuildArtifact`).

4. **Path**: Optionally set a path in the bucket if you want to deploy to a specific directory.

5. Click **Next** to review your settings.

### Step 7: Review and Create Pipeline

1. Review all the stages to ensure settings are correct.
   ![7-1](../photos/CIA2/7-1.png?raw=true)

2. Click **Create pipeline**.
   ![7-2](../photos/CIA2/7-2.png?raw=true)

Your pipeline will be created and should start running automatically. You can observe each stage to see if there are any errors.

### Step 8: Verify the Deployment

1. **Check the S3 Bucket**:
   - Go to the S3 bucket you configured for deployment.
   - Verify that your application files have been uploaded.
   ![8-1](../photos/CIA2/8-1.png?raw=true)
