# DevOps Lab - Mukesh T P

## Exercise 8

### Question 1: Customizing Maven Build Lifecycle

***Your team requires that unit tests should only be executed during the integration-test phase and not during the standard test phase, which is part of the default Maven lifecycle.
How would you modify the Maven build lifecycle to achieve this requirement? What changes would you make in the pom.xml file?***

To ensure that unit tests are only executed during the `integration-test` phase and not during the standard `test` phase, you can configure the `maven-surefire-plugin` (responsible for running unit tests) to be executed in the `integration-test` phase instead of the `test` phase. Here’s how you can modify the `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version>
            <executions>
                <execution>
                    <id>integration-tests</id>
                    <phase>integration-test</phase> <!-- Running unit tests in integration-test phase -->
                    <goals>
                        <goal>test</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

By placing the unit tests in the `integration-test` phase, they will not be run during the default `test` phase.

### Question 2: Adding External Dependencies and Managing Versions

***Your project requires the latest stable version of the Spring Framework, but the repository’s current version is outdated. You also need to ensure that the same version of the Spring Framework is used across all modules of your multi-module project.
How would you manage the external dependency in your pom.xml and ensure version consistency across multiple modules?***

To ensure that the latest stable version of Spring Framework is used across all modules, you can declare the version in a parent `pom.xml` and use dependency management. This way, all child modules inherit the version.

In the parent `pom.xml`:

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.9</version> <!-- Latest stable version of Spring -->
        </dependency>
    </dependencies>
</dependencyManagement>
```

In each module’s `pom.xml`, you don’t need to specify the version:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
    </dependency>
</dependencies>
```

This ensures consistency across all modules.

### Question 3: Skipping Tests During Build

***You are in a rush to deploy a hotfix to production. Running the full suite of unit and integration tests is time-consuming, and you want to skip them during the build process for this hotfix.
How would you configure Maven to skip tests during the build? Is there a specific command you can use to achieve this?***

To skip tests during a build for a hotfix, you can either:

- Use the Maven command:

  ```bash
  mvn install -DskipTests
  ```

  or
- Add the following configuration to your `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version>
            <configuration>
                <skipTests>true</skipTests>
            </configuration>
        </plugin>
    </plugins>
</build>
```

This will skip the tests during the build process.

### Question 4: Managing Plugins for Code Coverage

***Your project team wants to ensure that the code coverage is above 80% and wants to integrate code coverage reports as part of the build process.
How would you integrate a code coverage tool like JaCoCo into the Maven build lifecycle, and ensure it breaks the build if the coverage falls below 80%?***

To integrate JaCoCo for code coverage and ensure the build fails if the coverage is below 80%, add the following configuration to your `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.7</version>
            <executions>
                <execution>
                    <goals>
                        <goal>prepare-agent</goal>
                    </goals>
                </execution>
                <execution>
                    <id>report</id>
                    <phase>test</phase>
                    <goals>
                        <goal>report</goal>
                    </goals>
                </execution>
                <execution>
                    <id>check</id>
                    <goals>
                        <goal>check</goal>
                    </goals>
                    <configuration>
                        <rules>
                            <rule>
                                <element>BUNDLE</element>
                                <limits>
                                    <limit>
                                        <counter>INSTRUCTION</counter>
                                        <value>COVEREDRATIO</value>
                                        <minimum>0.80</minimum>
                                    </limit>
                                </limits>
                            </rule>
                        </rules>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

The `jacoco-maven-plugin` will check the coverage, and the build will fail if the coverage is below 80%.

### Question 5: Managing Multi-Module Project Dependencies

***You are working on a multi-module project where Module A is dependent on Module B. You need to ensure that any changes in Module B are automatically reflected in Module A without requiring external builds or manual version management.
How would you structure the pom.xml files for both modules to handle this dependency? How would you ensure that changes in Module B are integrated into Module A during the build?***

In a multi-module project, you can manage dependencies between modules by declaring them in the `pom.xml` files. For example, if Module A depends on Module B, add the following to Module A's `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>module-b</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>
</dependencies>
```

Ensure both modules are part of the same parent project. In the parent `pom.xml`, include both modules:

```xml
<modules>
    <module>module-a</module>
    <module>module-b</module>
</modules>
```

This ensures that when Module B is updated, Module A automatically gets the latest changes during the build process without manual version management.

### Question 6: Overriding a Dependency Version in a Child Module

***You are using a third-party library (e.g., Hibernate) in both parent and child modules of your project. However, the child module needs to use a different version of Hibernate from the one declared in the parent POM.
How would you override the dependency version in the child module’s pom.xml without affecting the parent module?***

To override a dependency version (e.g., Hibernate) in the child module without affecting the parent module, you can simply redefine the dependency in the child module’s `pom.xml`. Even if the parent declares a version, the child can override it by specifying its own version.

In the child `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>5.4.32.Final</version> <!-- Overriding version -->
    </dependency>
</dependencies>
```

This ensures that the child module will use the specified version of Hibernate, while the parent and other child modules remain unaffected.

### Scenario 7: Excluding Transitive Dependencies

***You have a project that includes a third-party library, but the library comes with unwanted transitive dependencies that are causing conflicts with your existing dependencies. You want to exclude these transitive dependencies.
 How would you exclude a specific transitive dependency from a third-party library in your pom.xml?***

To exclude specific transitive dependencies from a third-party library, you can use the `<exclusions>` tag in the `pom.xml`.

For example, if you're including `spring-core` but want to exclude `commons-logging` (a transitive dependency):

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.9</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```

This will prevent Maven from pulling in the unwanted transitive dependency `commons-logging`.

### Question 7: Using Maven Properties to Manage Project Information

***You want to reuse specific information, such as the project version or database URL, across multiple places in the pom.xml. Instead of hardcoding values, you want to manage them using Maven properties.
How would you define and use Maven properties in the pom.xml to avoid duplicating values across different configurations? (Use properties tag)***

To avoid duplicating values like the project version or database URL across multiple places, you can define Maven properties in the `pom.xml` under the `<properties>` section and then reference them.

For example:

```xml
<properties>
    <project.version>1.0.0</project.version>
    <db.url>jdbc:mysql://localhost:3306/mydb</db.url>
</properties>

<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>${project.version}</version> <!-- Using Maven property -->
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <version>${project.version}</version> <!-- Using Maven property -->
        </plugin>
    </plugins>
</build>

<configuration>
    <url>${db.url}</url> <!-- Using Maven property -->
</configuration>
```

This way, you can maintain values in one place and reuse them across the `pom.xml`.

### Question 8: Enforcing a Minimum Java Version for the Project

***Your project requires a minimum version of Java (e.g., Java 11) to build successfully. You want Maven to fail the build if a lower version of Java is used.
How would you configure the pom.xml to ensure that the project only builds with Java 11 or higher?***

To enforce a minimum Java version (e.g., Java 11), you can configure the Maven `maven-compiler-plugin` with the appropriate `source` and `target` values.

In your `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>11</source>
                <target>11</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

This will fail the build if a lower Java version is used, ensuring compatibility with Java 11 or higher.

### Question 9: Customizing the Default Build Lifecycle

***You are working on a Maven project where your team has decided that static code analysis using Checkstyle should be enforced before the unit tests are executed. Currently, Checkstyle is not part of the default Maven lifecycle.
How would you modify the build lifecycle to ensure that Checkstyle runs before the test phase? Describe the changes needed in the pom.xml and explain how the Maven build lifecycle would work after the changes.***

To ensure that Checkstyle runs before the test phase, you can bind the Checkstyle plugin to a phase before `test`, such as `validate` or `compile`.

In your `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-checkstyle-plugin</artifactId>
            <version>3.1.2</version>
            <executions>
                <execution>
                    <phase>validate</phase> <!-- Run Checkstyle during the validate phase -->
                    <goals>
                        <goal>check</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

This configuration ensures that Checkstyle runs during the `validate` phase, before `test`. The modified Maven lifecycle will now execute Checkstyle checks before proceeding to compile and test the code.

### Question 10: Skipping Specific Lifecycle Phases

***You are preparing a quick build for a production hotfix. Your team has decided to skip running unit tests temporarily, but you still want to perform integration tests.
How would you skip the test phase and still execute the integration-test and verify phases in your Maven build? What commands and configurations would you use?***

To skip the `test` phase while still running `integration-test` and `verify` phases, you can use the following Maven command:

```bash
mvn install -DskipTests=false -DskipITs=true
```

or, you can configure the `maven-surefire-plugin` to only skip unit tests:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version>
            <configuration>
                <skipTests>true</skipTests> <!-- Skips unit tests but allows integration tests -->
            </configuration>
        </plugin>
    </plugins>
</build>
```

This allows you to skip unit tests (`test` phase) while still executing `integration-test` and `verify` phases.

### Question 11: Binding Goals to Custom Phases

***In your project, you need to perform a database schema migration using Flyway right before the integration-test phase. The migration should only be performed in certain environments (e.g., staging or production).
How would you configure the Maven lifecycle and bind the Flyway plugin to run during a custom phase, ensuring it only runs for the correct environments?***

To perform a database schema migration using Flyway before the `integration-test` phase, and ensure it only runs in specific environments (e.g., staging or production), you can bind the Flyway plugin to the appropriate phase and use Maven profiles to control when it runs.

Example configuration in `pom.xml`:

```xml
<profiles>
    <profile>
        <id>staging</id>
        <activation>
            <property>
                <name>env</name>
                <value>staging</value>
            </property>
        </activation>
        <build>
            <plugins>
                <plugin>
                    <groupId>org.flywaydb</groupId>
                    <artifactId>flyway-maven-plugin</artifactId>
                    <version>8.0.0</version>
                    <executions>
                        <execution>
                            <phase>pre-integration-test</phase>
                            <goals>
                                <goal>migrate</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </build>
    </profile>

    <profile>
        <id>production</id>
        <activation>
            <property>
                <name>env</name>
                <value>production</value>
            </property>
        </activation>
        <!-- Same Flyway config for production -->
    </profile>
</profiles>
```

To activate this profile, run:

```bash
mvn clean install -Denv=staging
```

This ensures the Flyway migration only happens in the `staging` or `production` environments before the `integration-test` phase.

### Question 12: Handling Failed Builds

***During the build process, you notice that your Maven project fails during the package phase due to a compilation error in one of the modules. However, the other modules compile and package successfully.
How would you troubleshoot and isolate the cause of the build failure? Which Maven commands would you use to focus on the failing module without rerunning the entire build?
(Key : Usage of  -pl (projects list) and -am (also make) options to run the build for the affected module and its dependencies only)***

To troubleshoot a build failure and focus on the failing module, you can use the `-pl` (project list) option to run the build only for the affected module and its dependencies using the `-am` (also make) option.

Steps:

1. Identify the module causing the issue from the build log.
2. Use the following command to build only that module and its dependencies:

   ```bash
   mvn clean install -pl :module-name -am
   ```

This will isolate the failing module, allowing you to address the issue without rerunning the entire project build.

### Question 13: Using the Maven Site Lifecycle

***Your team wants to generate a project site with documentation, code reports, and dependency analysis. You need to ensure that the site is generated automatically after the build is successful.
How would you configure Maven to automatically generate a project site as part of the build process? What goals or phases would you bind the site generation to?***

To generate a project site with documentation, code reports, and dependency analysis, configure the `maven-site-plugin` in the `pom.xml` and bind it to the `site` phase. You can also ensure it runs after the `install` phase so that it’s automatically generated after a successful build.

Example:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-site-plugin</artifactId>
            <version>3.9.1</version>
            <executions>
                <execution>
                    <phase>site</phase>
                    <goals>
                        <goal>site</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

After a successful build, run:

```bash
mvn site
```

This generates a site that includes documentation, reports, and other insights.

### Question 14: Multi-Module Build with Independent Modules

***You have a multi-module Maven project, but some modules are independent and do not rely on others. You want to be able to build certain modules independently without building the entire project.
How would you structure your pom.xml and use Maven commands to allow independent builds of specific modules?***

To build specific independent modules in a multi-module project without building the entire project, you can structure the `pom.xml` to treat each module as an independent entity.

In the root `pom.xml`, define your modules:

```xml
<modules>
    <module>module-a</module>
    <module>module-b</module>
    <!-- Other modules -->
</modules>
```

When you want to build a specific module:

```bash
mvn clean install -pl module-a
```

This builds only `module-a` without triggering the build for the other modules.

### Question 15: Resolving Dependency Conflicts

***Your project is facing issues due to conflicting transitive dependencies. Multiple versions of the same library are being pulled in by different dependencies, causing build failures or unexpected runtime behavior.
How would you resolve this dependency conflict in Maven? What are the possible strategies for managing different versions of the same library in the pom.xml?***

To resolve dependency conflicts caused by different versions of the same library being pulled in, you can use dependency management and exclusion strategies in your `pom.xml`.

1. **Use `<dependencyManagement>`** to define a unified version for the conflicting library:

   ```xml
   <dependencyManagement>
       <dependencies>
           <dependency>
               <groupId>com.example</groupId>
               <artifactId>conflicting-library</artifactId>
               <version>1.2.3</version>
           </dependency>
       </dependencies>
   </dependencyManagement>
   ```

2. **Exclude transitive dependencies** that cause conflicts:

   ```xml
   <dependencies>
       <dependency>
           <groupId>com.example</groupId>
           <artifactId>main-library</artifactId>
           <version>2.0.0</version>
           <exclusions>
               <exclusion>
                   <groupId>com.example</groupId>
                   <artifactId>conflicting-library</artifactId>
               </exclusion>
           </exclusions>
       </dependency>
   </dependencies>
   ```

3. **Use the `mvn dependency:tree`** command to visualize the dependencies and ensure that the correct versions are being used.

### Question 16: Ensuring a Clean Build for a Multi-Module Project

***You are managing a multi-module Maven project, and you notice that sometimes old or generated files from previous builds interfere with the current build, causing failures. To prevent this, you need to ensure that a clean operation is always performed before any new build.
How would you ensure that the clean phase is executed every time before a new build in a multi-module project? Which command would you run to ensure a clean build across all modules?***

To ensure that the `clean` phase is executed before any new build in a multi-module Maven project, you can run the following command:

```bash
mvn clean install
```

This command will first clean the build (removing old files) and then execute the `install` phase for all modules. The `clean` phase will be applied to every module in the project.

### Question 17: Adding a Custom Clean Goal

***In addition to the standard cleaning of the target directory, your project generates temporary files in a custom folder (temp) outside of the target directory. You want to ensure that these files are also deleted during the clean phase.
How would you customize the clean lifecycle to include the deletion of files from the temp directory? How would you configure the pom.xml to achieve this?***

To delete additional files from a custom directory (e.g., `temp`) during the clean phase, you can use the `maven-antrun-plugin` to execute custom tasks, like deleting a folder outside the `target` directory.

Example configuration in `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-antrun-plugin</artifactId>
            <version>1.8</version>
            <executions>
                <execution>
                    <phase>clean</phase>
                    <goals>
                        <goal>run</goal>
                    </goals>
                    <configuration>
                        <tasks>
                            <delete dir="temp"/>
                        </tasks>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

This configuration ensures that the `temp` directory is deleted during the `clean` phase.

### Question 18: Handling Dependencies that Generate Files

***Your project has a dependency on a third-party library that generates temporary files in a specific directory (generated-files/). You need to make sure these files are cleaned up before the next build starts.
How would you ensure that the files generated by the third-party dependency are cleaned up when the clean lifecycle is triggered? What changes to the pom.xml would you make?***

If a third-party library generates files in a specific directory (e.g., `generated-files/`), you can also ensure these files are cleaned up by adding a custom clean goal using the `maven-antrun-plugin`.

Example configuration:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-antrun-plugin</artifactId>
            <version>1.8</version>
            <executions>
                <execution>
                    <phase>clean</phase>
                    <goals>
                        <goal>run</goal>
                    </goals>
                    <configuration>
                        <tasks>
                            <delete dir="generated-files"/>
                        </tasks>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

This ensures that the `generated-files/` directory is deleted during the `clean` phase.

### Question 19: Automatically Cleaning Before Testing

***You are working on a project where stale files from previous builds sometimes cause unit tests to fail. You want to ensure that every time the test phase is executed, a clean operation is automatically performed before it.
How would you modify the Maven lifecycle to ensure that the clean phase runs automatically before the test phase? How can you ensure that this happens without manually typing mvn clean test each time?***

To ensure that the `clean` phase runs automatically before the `test` phase, without having to manually type `mvn clean test`, you can configure the `test` phase to depend on the `clean` phase. In your `pom.xml`, you can use Maven's build lifecycle to bind the `clean` goal to the `test` phase.

Example configuration:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.1.0</version>
            <executions>
                <execution>
                    <id>clean-before-test</id>
                    <phase>pre-test</phase>
                    <goals>
                        <goal>clean</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

This ensures that the `clean` phase is executed automatically before the `test` phase, so you can just run `mvn test`, and the clean will happen first.

### Question 20: Customizing the Clean Phase with Additional Goals

***In addition to cleaning the build directory, you need to perform additional cleanup actions such as clearing cache files and deleting logs that are stored outside the project structure (e.g., in the user’s home directory).
How would you extend the clean lifecycle to include additional cleanup actions, such as clearing a cache directory and removing log files?***

To extend the clean lifecycle and include additional cleanup actions, such as clearing cache files and deleting logs located outside the project structure, you can again leverage the `maven-antrun-plugin` to perform these additional tasks during the `clean` phase.

Example configuration:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-antrun-plugin</artifactId>
            <version>1.8</version>
            <executions>
                <execution>
                    <phase>clean</phase>
                    <goals>
                        <goal>run</goal>
                    </goals>
                    <configuration>
                        <tasks>
                            <!-- Delete cache directory -->
                            <delete dir="${user.home}/.cache/myapp"/>
                            <!-- Delete log files -->
                            <delete>
                                <fileset dir="${user.home}/logs/myapp" includes="**/*.log"/>
                            </delete>
                        </tasks>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

This configuration will delete the cache directory and all log files in the specified locations during the `clean` phase.

### Question 21: Cleaning Dependent Projects in a Multi-Module Build

***In a multi-module project, certain modules depend on each other. You want to ensure that the clean phase is executed across all dependent modules if one module is cleaned.
How would you ensure that cleaning one module in a multi-module project triggers the clean phase for all dependent modules? How would you configure the build to handle this situation?***

In a multi-module Maven project, you can ensure that cleaning one module triggers the clean phase for all dependent modules by using the `-pl` (project list) and `-am` (also make) options.

For example, if you want to clean a specific module and all its dependencies, you would run the following command:

```bash
mvn clean -pl <module-name> -am
```

This command cleans the specified module (`<module-name>`) and also cleans all dependent modules in the project. You don’t need to modify the `pom.xml` for this behavior, as it's handled by Maven’s multi-module build capabilities.

### Question 22: Managing Build Artifacts During the Clean Phase

***Your project is using third-party libraries that download files into a local repository or external folders during the build process. However, you don’t want these downloaded files to be removed during the clean phase because they are needed for future builds.
How would you exclude certain directories or files (e.g., the repository directory) from being deleted during the clean phase while still cleaning the main target directory?***

To exclude specific directories (such as a local repository or external folders) from being deleted during the `clean` phase while still cleaning the main `target` directory, you can configure the `maven-clean-plugin` to include and exclude specific directories.

Example configuration:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <filesets>
                    <fileset>
                        <directory>${project.build.directory}</directory>
                        <includes>
                            <include>**/*</include>
                        </includes>
                        <excludes>
                            <exclude>path/to/local/repository/**</exclude>
                        </excludes>
                    </fileset>
                </filesets>
            </configuration>
        </plugin>
    </plugins>
</build>
```

This configuration ensures that everything in the `target` directory is cleaned, except for the `path/to/local/repository`.

### Question 23: Reusing Common Build Configurations

***You are managing a set of Maven projects, and they all share common configurations such as Java version, plugin configurations, and dependency versions. You want to centralize these configurations so that each child project does not need to repeat them.
How would you structure a parent POM file to manage shared configurations (such as Java version and commonly used plugins) that all child projects can inherit? What elements of the parent POM would you define for reuse?***

To centralize common configurations across multiple Maven projects, you can create a parent POM that defines shared configurations such as Java version, plugin management, and dependency versions. Child projects will inherit these configurations.

Example `parent-pom.xml`:

```xml
<project>
    <groupId>com.example</groupId>
    <artifactId>parent-project</artifactId>
    <version>1.0</version>
    <packaging>pom</packaging>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencyManagement>
        <dependencies>
            <!-- Shared dependencies -->
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
                <version>5.3.10</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <!-- Common plugin configurations -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>${maven.compiler.source}</source>
                    <target>${maven.compiler.target}</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

Child projects can then inherit these configurations by specifying the parent in their `pom.xml`:

```xml
<parent>
    <groupId>com.example</groupId>
    <artifactId>parent-project</artifactId>
    <version>1.0</version>
</parent>
```

### Question 24: Overriding Parent Configurations in Child Projects

***You have a parent POM that defines shared configurations, but one of your child projects requires a different Java version (Java 11 instead of Java 8) and an additional plugin. You want to override the Java version and add the new plugin in the child POM without affecting other child projects.
How would you override the Java version and add a new plugin in the child POM? What parts of the child POM would you need to modify?***

To override a parent configuration, such as changing the Java version and adding a new plugin in a child POM, you modify the relevant sections of the child POM.

Example `child-pom.xml` to override Java version and add a plugin:

```xml
<parent>
    <groupId>com.example</groupId>
    <artifactId>parent-project</artifactId>
    <version>1.0</version>
</parent>

<properties>
    <maven.compiler.source>11</maven.compiler.source>
    <maven.compiler.target>11</maven.compiler.target>
</properties>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.22.2</version>
        </plugin>
    </plugins>
</build>
```

This child POM overrides the Java version from 1.8 to 11 and adds a new plugin (`maven-surefire-plugin`) without affecting other child projects.

### Question 25: Managing Dependencies in Parent and Child Projects

***Your parent POM defines several common dependencies, but a child project requires a different version of one of these dependencies. You want to override the version of this dependency in the child project without modifying the parent POM.
How would you override the version of a dependency in a child project while inheriting other dependencies from the parent? What part of the child POM would you modify to achieve this?***

If a child project requires a different version of a dependency than the one defined in the parent POM, you can override the dependency version in the child project’s `pom.xml` while inheriting other dependencies from the parent.

Example `child-pom.xml` to override a dependency version:

```xml
<parent>
    <groupId>com.example</groupId>
    <artifactId>parent-project</artifactId>
    <version>1.0</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.12</version> <!-- Overriding the version -->
    </dependency>
</dependencies>
```

In this example, the `spring-core` dependency is overridden to version `5.3.12` in the child project, while other dependencies from the parent are still inherited.

### Question 26: Using Profiles in Parent POM for Environment-Specific Configurations

***You have a parent POM that defines different configurations for various environments (development, staging, production). Each child project should automatically inherit these configurations, and you want to use Maven profiles to switch between environments.
How would you set up environment-specific configurations using Maven profiles in the parent POM? How can the child projects inherit and use these profiles?***

To set up environment-specific configurations in a parent POM using Maven profiles, you can define multiple profiles in the parent POM, each corresponding to a specific environment (e.g., development, staging, production). These profiles can contain different properties or plugin configurations, which will be inherited by child projects.

Example `parent-pom.xml`:

```xml
<project>
    <profiles>
        <profile>
            <id>dev</id>
            <properties>
                <env>development</env>
                <database.url>jdbc:mysql://localhost/dev_db</database.url>
            </properties>
        </profile>
        <profile>
            <id>staging</id>
            <properties>
                <env>staging</env>
                <database.url>jdbc:mysql://staging.server/staging_db</database.url>
            </properties>
        </profile>
        <profile>
            <id>prod</id>
            <properties>
                <env>production</env>
                <database.url>jdbc:mysql://prod.server/prod_db</database.url>
            </properties>
        </profile>
    </profiles>
</project>
```

Child projects automatically inherit these profiles. To activate a profile, you can pass the `-P` flag when running Maven commands:

```bash
mvn clean install -Pdev
```

This activates the `dev` profile, and the child projects will inherit the environment-specific properties or configurations.

### Question 27: Inheriting and Extending Build Plugins

***The parent POM defines several build plugins that are used across all projects. However, one of the child projects requires additional configuration for one of these plugins (e.g., a different goal or execution phase). You need to extend the plugin configuration in the child POM without affecting other projects.
How would you extend the configuration of an inherited plugin in the child POM? What changes would you make to the child POM to achieve this?***

To extend the configuration of an inherited plugin in a child POM, you can redefine the plugin in the child POM and add additional goals or executions while still inheriting the base configuration from the parent POM.

Example `parent-pom.xml` with a plugin:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <executions>
                    <execution>
                        <id>default-compile</id>
                        <goals>
                            <goal>compile</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

In the `child-pom.xml`, extend the plugin configuration:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <executions>
                    <execution>
                        <id>custom-compile</id>
                        <goals>
                            <goal>compile</goal>
                        </goals>
                        <configuration>
                            <source>11</source>
                            <target>11</target>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

This allows you to add custom executions for the plugin in the child POM while inheriting the original configuration from the parent POM.

### Question 28: Managing Parent-Child Relationships in a Multi-Module Project

***You are working on a multi-module Maven project where each child module inherits from a common parent POM. However, one of the child modules has specific requirements that need a new plugin or different configuration that should not affect the other child modules. You want to ensure that only this child module includes the new plugin without altering the configurations in other modules.
How would you handle the situation where one child module requires a new plugin or different configuration, but this should not impact the other child modules? What changes would you make in the child POM to meet this requirement?***

If one child module requires a new plugin or different configuration, but you do not want to affect other modules, you can add the new plugin only in the specific child module’s POM without modifying the parent POM or other child modules.

Example `child-pom.xml`:

```xml
<project>
    <build>
        <plugins>
            <!-- Additional plugin specific to this child module -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.2</version>
                <configuration>
                    <!-- Custom configuration -->
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

This ensures that only the specific child module includes this new plugin, and other modules remain unaffected.

### Question 29: Inheriting and Customizing Dependency Versions in Child Projects

***Situation: You have a parent POM that defines common dependencies using `<dependencyManagement>`. Some child projects need to use the same dependencies but with different versions. You need to ensure that child projects can override the versions without modifying the parent POM.
How would you allow child projects to inherit common dependencies from the parent POM but use different versions where needed? What changes would you make in the child POM to override the dependency versions?***

When using `<dependencyManagement>` in the parent POM, you can allow child projects to override dependency versions by defining the dependency in the child POM with a different version.

Example `parent-pom.xml`:

```xml
<project>
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
                <version>5.3.10</version>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```

To override the version in the `child-pom.xml`:

```xml
<project>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.12</version>
        </dependency>
    </dependencies>
</project>
```

This allows the child project to use a different version of `spring-core`, while still inheriting other dependencies from the parent.

### Question 30: Customizing the Clean Lifecycle

***You have a multi-module project, and one of the child modules requires a custom action during the clean phase (such as deleting specific files that are not included in the standard Maven clean). The other child modules should retain the default behavior of the clean phase.
How would you customize the Maven clean phase for a specific module while retaining the default clean behavior for other modules? What changes would you make in the child POM to customize the clean phase?***

To customize the Maven clean phase for a specific module while retaining the default behavior for other modules, you can configure the `maven-clean-plugin` in the child module’s POM.

Example `child-pom.xml`:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-clean-plugin</artifactId>
                <version>3.1.0</version>
                <executions>
                    <execution>
                        <id>custom-clean</id>
                        <phase>clean</phase>
                        <goals>
                            <goal>clean</goal>
                        </goals>
                        <configuration>
                            <filesets>
                                <fileset>
                                    <directory>${project.basedir}/temp</directory>
                                    <includes>
                                        <include>**/*</include>
                                    </includes>
                                </fileset>
                            </filesets>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

This customizes the clean phase for the specific child module by deleting files in the `temp` directory. Other child modules will retain the default clean behavior.

### Question 31: Using Plugin Inheritance with Custom Execution Goals

***The parent POM defines several common plugins used by all child modules. One of the child modules, however, requires an additional goal for one of these plugins (e.g., running tests with a specific configuration).
How would you extend the plugin configuration in the child POM to add a custom execution goal for a plugin that is inherited from the parent POM? What changes would you make to the child POM to include the additional goal?***

To add a custom execution goal for an inherited plugin in a child POM, you can extend the plugin configuration and add the new goal in the child POM.

Example `parent-pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.22.2</version>
        </plugin>
    </plugins>
</build>
```

To add a custom goal in the `child-pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <executions>
                <execution>
                    <id>custom-test</id>
                    <goals>
                        <goal>test</goal>
                    </goals>
                    <configuration>
                        <includes>
                            <include>**/*Test.java</include>
                        </includes>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

This configuration allows you to add a custom test execution for this child module while still inheriting the base plugin setup from the parent.
