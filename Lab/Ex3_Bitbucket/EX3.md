# DevOps Lab - Mukesh T P

## Exercise 3

### Implement Bitbucket Operations using Git

### 1. Creating a Repository

1. Go to your Bitbucket account.
    ![1-1](../photos/Ex3/1-1.png?raw=true)

2. Click on the `Repositories` tab in the sidebar.
    ![1-2](../photos/Ex3/1-2.png?raw=true)

3. Click on the `Create repository` button.
    ![1-3](../photos/Ex3/1-3.png?raw=true)
4. Fill in the repository details:
   - Repository name: `example-repo`
   - Access level: Choose between Private or Public.
    ![1-4](../photos/Ex3/1-4.png?raw=true)

5. Click on the `Create repository` button.
    ![1-5](../photos/Ex3/1-5.png?raw=true)

### 2. Cloning a Repository

1. In your Bitbucket repository, find the `Clone` button and copy the repository URL.
    ![2-1](../photos/Ex3/2-1.png?raw=true)

2. Open your terminal.
    ![2-2](../photos/Ex3/2-2.png?raw=true)

3. Clone the repository using the following command:

   ```bash
   git clone https://mukeshtp@bitbucket.org/devopslab-mukesh/devopslab.git
   ```

    ![2-3](../photos/Ex3/2-3.png?raw=true)

#### 3. Making Changes and Creating a Branch

1. Navigate into the cloned repository:

   ```bash
   cd example-repo
   ```

    ![3-1](../photos/Ex3/3-1.png?raw=true)

2. Create a new text file named `test.txt`:

   ```bash
   touch test.txt
   ```

    ![3-2](../photos/Ex3/3-2.png?raw=true)

3. Add some content to the `test.txt` file.

    ```bash
    echo "This is a test file." › test.txt
    ```

    ![3-3](../photos/Ex3/3-3.png?raw=true)

4. Check the status of the repository:

   ```bash
   git status
   ```

    ![3-4](../photos/Ex3/3-4.png?raw=true)

5. Stage the changes for commit:

   ```bash
   git add test.txt
   ```

    ![3-5](../photos/Ex3/3-5.png?raw=true)

6. Commit the changes with a descriptive message:

   ```bash
   git commit -m "Edited test.txt"
   ```

    ![3-6](../photos/Ex3/3-6.png?raw=true)

7. Create a new branch named `feature`:

   ```bash
   git branch feature
   ```

    ![3-7](../photos/Ex3/3-7.png?raw=true)

8. Switch to the `feature` branch:

   ```bash
   git checkout feature
   ```

    ![3-8](../photos/Ex3/3-8.png?raw=true)

### 4. Pushing Changes to Bitbucket

1. Add the repository URL in a variable:

   ```bash
   REPO_URL=<repository_url>
   ```

    ![4-1](../photos/Ex3/4-1.png?raw=true)

2. Push the `feature` branch to Bitbucket:

   ```bash
   git push -u origin feature
   ```

    ![4-2](../photos/Ex3/4-2.png?raw=true)

3. Check your Bitbucket repository to confirm that the new branch `feature` is available.
    ![4-3](../photos/Ex3/4-3.png?raw=true)

### 5. Collaborating through Pull Requests

1. Create a pull request on Bitbucket:

   - Go to the repository on Bitbucket.
   - Click on `Create pull request`.
   - Choose the source branch (`feature`) and the target branch (`main` or `master`).
   - Review the changes and click `Create pull request`.

    ![5-1](../photos/Ex3/5-1.png?raw=true)
    ![5-2](../photos/Ex3/5-2.png?raw=true)
    ![5-3](../photos/Ex3/5-3.png?raw=true)

2. Review and merge the pull request:

   - Add a title and description for the pull request.
   - Assign reviewers if needed.
   - Once the pull request is approved, merge it into the target branch.

    ![5-4](../photos/Ex3/5-4.png?raw=true)
    ![5-5](../photos/Ex3/5-5.png?raw=true)
    ![5-6](../photos/Ex3/5-6.png?raw=true)

### 6. Syncing Changes

1. After the pull request is merged, update your local repository:

   ```bash
   git checkout main
   git pull origin main
   ```

   ![6-1](../photos/Ex3/6-1.png?raw=true)
   ![6-2](../photos/Ex3/6-2.png?raw=true)
