# DevOps Lab - Mukesh T P

## Exercise 2

### Implement GitLab Operations using Git

#### 1. Creating a Repository

1. Go to your GitLab account.
    ![1-1](../photos/Ex2/1-1.png?raw=true)

2. Click on the `New project` button.
    ![1-2](../photos/Ex2/1-2.png?raw=true)

3. Select `Create blank project`.
    ![1-3](../photos/Ex2/1-3.png?raw=true)

4. Fill in the project details:
   - Project name: `DevOpsLab`
   - Project slug: `devopslab` (auto-filled)
   - Visibility level: Choose between Private, Internal, or Public.
    ![1-4](../photos/Ex2/1-4.png?raw=true)

5. Click on the `Create project` button.
    ![1-5](../photos/Ex2/1-5.png?raw=true)

#### 2. Cloning a Repository

1. In your GitLab repository, find the `Clone` button and copy the repository URL.
    ![2-1](../photos/Ex2/2-1.png?raw=true)

2. Open your terminal.
    ![2-2](../photos/Ex2/2-2.png?raw=true)

3. Clone the repository using the following command:

   ```bash
   git clone https://gitlab.com/MukeshTheGreat/devopslab.git
   ```

    ![2-3](../photos/Ex2/2-3.png?raw=true)

#### 3. Making Changes and Creating a Branch

1. Navigate into the cloned repository:

   ```bash
   cd example-repo
   ```

    ![3-1](../photos/Ex2/3-1.png?raw=true)

2. Create a new text file named `test.txt`:

   ```bash
   touch test.txt
   ```

    ![3-2](../photos/Ex2/3-2.png?raw=true)

3. Add some content to the `test.txt` file.

    ```bash
    echo "This is a test file." › test.txt
    ```

    ![3-3](../photos/Ex2/3-3.png?raw=true)

4. Check the status of the repository:

   ```bash
   git status
   ```

    ![3-4](../photos/Ex2/3-4.png?raw=true)

5. Stage the changes for commit:

   ```bash
   git add test.txt
   ```

    ![3-5](../photos/Ex2/3-5.png?raw=true)

6. Commit the changes with a descriptive message:

   ```bash
   git commit -m "Edited test.txt"
   ```

    ![3-6](../photos/Ex2/3-6.png?raw=true)

7. Create a new branch named `feature`:

   ```bash
   git branch feature
   ```

    ![3-7](../photos/Ex2/3-7.png?raw=true)

8. Switch to the `feature` branch:

   ```bash
   git checkout feature
   ```

    ![3-8](../photos/Ex2/3-8.png?raw=true)

#### 4. Pushing Changes to GitLab

1. Add the repository URL in a variable:

   ```bash
   REPO_URL=<repository_url>
   ```

    ![4-1](../photos/Ex2/4-1.png?raw=true)

2. Push the `feature` branch to GitLab:

   ```bash
   git push -u origin feature
   ```

    ![4-2](../photos/Ex2/4-2.png?raw=true)

3. Check your GitLab repository to confirm that the new branch `feature` is available.
    ![4-3](../photos/Ex2/4-3.png?raw=true)  

#### 5. Collaborating through Merge Requests

1. Go to your GitLab repository.
    ![5-1](../photos/Ex2/5-1.png?raw=true)
2. Click on the `Merge Requests` tab.
    ![5-2](../photos/Ex2/5-2.png?raw=true)
3. Click on the `New merge request` button.
    ![5-3](../photos/Ex2/5-3.png?raw=true)
4. Select the `source branch` as `feature` and the `target branch` as `main` (or `master`).
    ![5-4](../photos/Ex2/5-4.png?raw=true)
5. Click on the `Compare branches and continue` button.
    ![5-5](../photos/Ex2/5-5.png?raw=true)
6. Fill in the details of the merge request and click on the `Create merge request` button.
    ![5-6](../photos/Ex2/5-6.png?raw=true)
7. Review the merge request and click on the `Merge` button to merge it.
    ![5-7](../photos/Ex2/5-7.png?raw=true)
    ![5-8](../photos/Ex2/5-8.png?raw=true)

#### 6. Syncing Changes

1. After the merge request is merged, update your local repository:

   ```bash
   git checkout main
   git pull origin main
   ```

    ![6-1](../photos/Ex2/6-1.png?raw=true)
