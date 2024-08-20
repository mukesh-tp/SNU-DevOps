# DevOps Lab - Mukesh T P

## Exercise 5

## Setting Up and Exploring Maven

### a. Installing Maven on macOS Using Homebrew

#### Step 1: Install Homebrew (if not already installed)

1. Open Terminal and run the following command to install Homebrew (if you don't have it installed yet):

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Follow the on-screen instructions to complete the installation.

#### Step 2: Install Maven Using Homebrew

1. Once Homebrew is installed, use the following command to install Maven:

   ```bash
   brew install maven
   ```

2. Homebrew will download and install Maven along with any dependencies.

#### Step 3: Verify the Installation

1. To confirm Maven is installed correctly, check the version by running:

   ```bash
   mvn -v
   ```

   ![Verify Maven](../photos/Ex5/verify_maven.png?raw=true)

2. You should see Maven version details, Java version, and other environment information.

### b. Creating and Building a Maven Project

#### Step 1: Generate a Maven Project

1. Use the following command to generate a new Maven project:

   ```bash
   mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

   ![Maven Project Generation](../photos/Ex5/maven_project.png?raw=true)
   ![Maven Project Generation 1](../photos/Ex5/maven_project1.png?raw=true)

2. Navigate to the newly created project directory:

   ```bash
   cd my-app
   ```

   ![Navigate Project](../photos/Ex5/navigate_project.png?raw=true)

#### Step 2: Build the Maven Project

1. Use Maven to compile the project:

   ```bash
   mvn compile
   ```

   ![Maven Compile](../photos/Ex5/maven_compile.png?raw=true)
   ![Maven Compile](../photos/Ex5/maven_compile1.png?raw=true)

2. Run the project:

   ```bash
   mvn exec:java -Dexec.mainClass="com.example.App"
   ```

   ![Run Maven Project](../photos/Ex5/run_maven_project.png?raw=true)
   ![Run Maven Project](../photos/Ex5/run_maven_project1.png?raw=true)

### c. Exploring Maven Commands

1. **Clean the Project**: Remove the `target` directory:

   ```bash
   mvn clean
   ```

   ![Maven Clean](../photos/Ex5/maven_clean.png?raw=true)

2. **Package the Project**: Build the project and create a JAR file:

   ```bash
   mvn package
   ```

   ![Maven Package](../photos/Ex5/maven_package.png?raw=true)
   ![Maven Package](../photos/Ex5/maven_package1.png?raw=true)

3. **Install the Project**: Install the JAR in the local Maven repository:

   ```bash
   mvn install
   ```

   ![Maven Install](../photos/Ex5/maven_install.png?raw=true)
   ![Maven Install](../photos/Ex5/maven_install1.png?raw=true)
