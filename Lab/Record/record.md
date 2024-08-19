<div style="page-break-after: always;"></div>

<table style="width: 100%; border-collapse: collapse; padding:0;">
  <tr>
    <td style="width: 20%; border: 1px solid black; padding: 0;">
      <table style="width: 100%; border-collapse: collapse; border: none;">
        <tr>
          <td style="padding-top: 0; border-bottom: 1px solid black; text-align: center; font-weight: bold; border-left: none; border-top: none; vertical-align: middle;">Ex. No. 1</td>
        </tr>
        <tr>
          <td style="padding-bottom:0; text-align: center; border-bottom: none; border-right: none; vertical-align: middle;">12/07/2024</td>
        </tr>
      </table>
    </td>
    <td style="width: 80%; border: 1px solid black; text-align: center; font-weight: bold; vertical-align: middle;">Git & GitHub</td>
  </tr>
</table>

#### AIM

Algorithm for Git and GitHub Operations

#### Algorithm

1. **Create a Repository**:
   - Initialize a new Git repository named "Master".
   - Verify repository initialization.

2. **Add and Commit Changes**:
   - Create a new text file named `README.md`.
   - Add content to the `README.md` file.
   - Add the file to the staging area.
   - Commit the changes with a message.

3. **Exploring History**:
   - Modify or add content to the text file.
   - Add and commit the changes.

4. **Branching and Merging**:
   - Create a new branch named `Updated_ReadMe`.
   - Commit changes in the new branch.
   - Merge changes from `Updated_ReadMe` branch into `Master` branch.

5. **Collaborating with Remote Repositories**:
   - Link the local repository to a remote repository.

6. **Push Changes**:
   - Push local commits to the remote repository.

7. **Cloning a Repository**:
   - Clone the repository from GitHub.

8. **Making Changes and Creating a Branch**:
   - Navigate into the cloned repository.
   - Make necessary changes.
   - Check the status of the repository.

9. **Pushing Changes to GitHub**:
   - Add the changes to the staging area.
   - Commit the changes.
   - Push the local branch to the remote repository.

10. **Collaborating through Pull Requests**:
    - Create a pull request on GitHub.
    - Choose base branch and compare with the new branch.
    - Review and merge the pull request.
    - Add title, description, and assign reviewers.
    - Reviewers approve and merge the pull request into the base branch.

11. **Syncing Changes**:
    - Update local repository after the pull request is merged.

#### Input

```sh
# Task 1
## a. Create a Repository
git init

## b. Add and Commit Changes
touch README.md
echo "# This is the readme file for devops" > README.md
git add README.md
git commit -m "Added README.md"

## c. Exploring History
echo "# This is the README file for DevOps" > README.md
git add README.md
git commit -m "Corrected content of README.md"

## d. Branching and Merging
git checkout -b Updated_ReadMe
echo "# This is the updated README file for DevOps" > README.md
git add README.md
git commit -m "Updated README.md"
git checkout main
git merge Updated_ReadMe

## e. Collaborating with Remote Repositories
git remote add origin https://github.com/mukesh-tp/SNU-DevOps.git

## f. Push Changes
git branch -M main
git push -u origin main

# Task 2
## a. Cloning a Repository
git clone https://github.com/mukesh-tp/WebTechLab.git

## b. Making Changes and Creating a Branch
cd WebTechLab
touch README.md
echo "# This is the README file for WebTechLab" > README.md
git status

## c. Pushing Changes to GitHub
git add .
git commit -m "Added README.md"
git push -u origin main

## d. Collaborating through Pull Requests
# Performed on GitHub:
# 1. Create a pull request.
# 2. Choose base branch and compare with new branch.
# 3. Review and merge the pull request.
# 4. Add title and description.
# 5. Assign reviewers.
# 6. Reviewers approve and merge the pull request.

## e. Syncing Changes
git pull origin main
```

#### Output

1. **Repository Creation**:
   - A new Git repository named "Master" is created.
   - Confirmation message displayed.

   ![1a](../photos/Ex1/1a.png?raw=true)

2. **Add and Commit Changes**:
   - `README.md` file is created.
   - File contents are added.
   - File is added to the staging area and committed.

   ![1b](../photos/Ex1/1b.png?raw=true)

3. **Exploring History**:
   - `README.md` file is modified and changes committed.

   ![1c](../photos/Ex1/1c.png?raw=true)

4. **Branching and Merging**:
   - New branch `Updated_ReadMe` is created and changes committed.
   - Changes are merged into the `main` branch.

   ![1d](../photos/Ex1/1d.png?raw=true)

5. **Collaborating with Remote Repositories**:
   - Local repository is linked to the remote repository.

   ![1e](../photos/Ex1/1e.png?raw=true)

6. **Push Changes**:
   - Local commits are pushed to the remote repository.

   ![1f](../photos/Ex1/1f.png?raw=true)

7. **Cloning a Repository**:
   - Repository is cloned from GitHub.

   ![2a](../photos/Ex1/2a.png?raw=true)

8. **Making Changes and Creating a Branch**:
   - Changes are made and the status of the repository is checked.

   ![2b](../photos/Ex1/2b.png?raw=true)

9. **Pushing Changes to GitHub**:
   - Changes are pushed to the remote repository.

   ![2c](../photos/Ex1/2c.png?raw=true)

10. **Collaborating through Pull Requests**:
    - Pull request is created, reviewed, and merged on GitHub.

    ![2d](../photos/Ex1/2d.png?raw=true)

11. **Syncing Changes**:
    - Local repository is updated with the latest changes from the remote repository.

    ![2e](../photos/Ex1/2e.png?raw=true)

<div style="page-break-after: always;"></div>

<table style="width: 100%; border-collapse: collapse; padding:0;">
  <tr>
    <td style="width: 20%; border: 1px solid black; padding: 0;">
      <table style="width: 100%; border-collapse: collapse; border: none;">
        <tr>
          <td style="padding-top: 0; border-bottom: 1px solid black; text-align: center; font-weight: bold; border-left: none; border-top: none; vertical-align: middle;">Ex. No. 2</td>
        </tr>
        <tr>
          <td style="padding-bottom:0; text-align: center; border-bottom: none; border-right: none; vertical-align: middle;">07/08/2024</td>
        </tr>
      </table>
    </td>
    <td style="width: 80%; border: 1px solid black; text-align: center; font-weight: bold; vertical-align: middle;">Git & GitLab</td>
  </tr>
</table>

#### AIM
Algorithm for Implementing GitLab Operations using Git

#### Algorithm:

1. **Creating a Repository**:
   - Log into your GitLab account.
   - Click on the `New project` button.
   - Select `Create blank project`.
   - Fill in the project details and set the visibility level.
   - Click on the `Create project` button.

2. **Cloning a Repository**:
   - Copy the repository URL from GitLab.
   - Open the terminal.
   - Clone the repository using the URL.

3. **Making Changes and Creating a Branch**:
   - Navigate into the cloned repository.
   - Create a new text file named `test.txt`.
   - Add content to the `test.txt` file.
   - Check the repository status.
   - Stage the changes for commit.
   - Commit the changes with a message.
   - Create a new branch named `feature`.
   - Switch to the `feature` branch.

4. **Pushing Changes to GitLab**:
   - Add the repository URL to a variable.
   - Push the `feature` branch to GitLab.
   - Confirm the new branch is available in the GitLab repository.

5. **Collaborating through Merge Requests**:
   - Go to the `Merge Requests` tab in the GitLab repository.
   - Click on the `New merge request` button.
   - Select the `source branch` as `feature` and the `target branch` as `main`.
   - Click on the `Compare branches and continue` button.
   - Fill in the merge request details and create the merge request.
   - Review and merge the request.

6. **Syncing Changes**:
   - After merging, update the local repository with the latest changes from the remote repository.

#### Input

```sh
# Task 1: Creating a Repository
# 1. Log into your GitLab account.
# 2. Click on the `New project` button.
# 3. Select `Create blank project`.
# 4. Fill in the project details:
#    - Project name: `DevOpsLab`
#    - Project slug: `devopslab` (auto-filled)
#    - Visibility level: Choose between Private, Internal, or Public.
# 5. Click on the `Create project` button.

# Task 2: Cloning a Repository
# 1. Copy the repository URL.
# 2. Open terminal.
git clone https://gitlab.com/MukeshTheGreat/devopslab.git

# Task 3: Making Changes and Creating a Branch
cd devopslab
touch test.txt
echo "This is a test file." > test.txt
git status
git add test.txt
git commit -m "Added test.txt"
git branch feature
git checkout feature

# Task 4: Pushing Changes to GitLab
REPO_URL=https://gitlab.com/MukeshTheGreat/devopslab.git
git push -u origin feature

# Task 5: Collaborating through Merge Requests
# 1. Go to the GitLab repository.
# 2. Click on the `Merge Requests` tab.
# 3. Click on the `New merge request` button.
# 4. Select `source branch` as `feature` and `target branch` as `main`.
# 5. Click on the `Compare branches and continue` button.
# 6. Fill in the merge request details and click `Create merge request`.
# 7. Review and click `Merge` to merge the request.

# Task 6: Syncing Changes
git checkout main
git pull origin main
```

#### Output

1. **Creating a Repository**:
   - A new GitLab repository named `DevOpsLab` is created with the specified details.
   ![1-1](../photos/Ex2/1-1.png?raw=true)
   ![1-2](../photos/Ex2/1-2.png?raw=true)
   ![1-3](../photos/Ex2/1-3.png?raw=true)
   ![1-4](../photos/Ex2/1-4.png?raw=true)
   ![1-5](../photos/Ex2/1-5.png?raw=true)

2. **Cloning a Repository**:
   - The repository is successfully cloned to the local machine.
   ![2-1](../photos/Ex2/2-1.png?raw=true)
   ![2-2](../photos/Ex2/2-2.png?raw=true)
   ![2-3](../photos/Ex2/2-3.png?raw=true)

3. **Making Changes and Creating a Branch**:
   - Navigated into the cloned repository.
   - `test.txt` file created and modified.
   - Changes staged and committed.
   - New branch `feature` created and switched to.
   ![3-1](../photos/Ex2/3-1.png?raw=true)
   ![3-2](../photos/Ex2/3-2.png?raw=true)
   ![3-3](../photos/Ex2/3-3.png?raw=true)
   ![3-4](../photos/Ex2/3-4.png?raw=true)
   ![3-5](../photos/Ex2/3-5.png?raw=true)
   ![3-6](../photos/Ex2/3-6.png?raw=true)
   ![3-7](../photos/Ex2/3-7.png?raw=true)
   ![3-8](../photos/Ex2/3-8.png?raw=true)

4. **Pushing Changes to GitLab**:
   - `feature` branch pushed to GitLab.
   - Verified the new branch `feature` is available in the GitLab repository.
   ![4-1](../photos/Ex2/4-1.png?raw=true)
   ![4-2](../photos/Ex2/4-2.png?raw=true)
   ![4-3](../photos/Ex2/4-3.png?raw=true)

5. **Collaborating through Merge Requests**:
   - Merge request created, reviewed, and merged on GitLab.
   ![5-1](../photos/Ex2/5-1.png?raw=true)
   ![5-2](../photos/Ex2/5-2.png?raw=true)
   ![5-3](../photos/Ex2/5-3.png?raw=true)
   ![5-4](../photos/Ex2/5-4.png?raw=true)
   ![5-5](../photos/Ex2/5-5.png?raw=true)
   ![5-6](../photos/Ex2/5-6.png?raw=true)
   ![5-7](../photos/Ex2/5-7.png?raw=true)
   ![5-8](../photos/Ex2/5-8.png?raw=true)

6. **Syncing Changes**:
   - Local repository updated with the latest changes from the remote repository.
   ![6-1](../photos/Ex2/6-1.png?raw=true)

<div style="page-break-after: always;"></div>

<table style="width: 100%; border-collapse: collapse; padding:0;">
  <tr>
    <td style="width: 20%; border: 1px solid black; padding: 0;">
      <table style="width: 100%; border-collapse: collapse; border: none;">
        <tr>
          <td style="padding-top: 0; border-bottom: 1px solid black; text-align: center; font-weight: bold; border-left: none; border-top: none; vertical-align: middle;">Ex. No. 3</td>
        </tr>
        <tr>
          <td style="padding-bottom:0; text-align: center; border-bottom: none; border-right: none; vertical-align: middle;">07/08/2024</td>
        </tr>
      </table>
    </td>
    <td style="width: 80%; border: 1px solid black; text-align: center; font-weight: bold; vertical-align: middle;">Git & BitBucket</td>
  </tr>
</table>

#### AIM

Algorithm for Implementing Bitbucket Operations using Git

#### Algorithm

1. **Creating a Repository**:
   - Log into your Bitbucket account.
   - Click on the `Repositories` tab in the sidebar.
   - Click on the `Create repository` button.
   - Fill in the repository details and set the access level.
   - Click on the `Create repository` button.

2. **Cloning a Repository**:
   - Copy the repository URL from Bitbucket.
   - Open the terminal.
   - Clone the repository using the URL.

3. **Making Changes and Creating a Branch**:
   - Navigate into the cloned repository.
   - Create a new text file named `test.txt`.
   - Add content to the `test.txt` file.
   - Check the repository status.
   - Stage the changes for commit.
   - Commit the changes with a message.
   - Create a new branch named `feature`.
   - Switch to the `feature` branch.

4. **Pushing Changes to Bitbucket**:
   - Add the repository URL to a variable.
   - Push the `feature` branch to Bitbucket.
   - Confirm the new branch is available in the Bitbucket repository.

5. **Collaborating through Pull Requests**:
   - Go to the repository on Bitbucket.
   - Click on `Create pull request`.
   - Choose the source branch (`feature`) and the target branch (`main`).
   - Review the changes and create the pull request.
   - Review and merge the pull request.

6. **Syncing Changes**:
   - After merging, update the local repository with the latest changes from the remote repository.

#### Input

```sh
# Task 1: Creating a Repository
# 1. Log into your Bitbucket account.
# 2. Click on the `Repositories` tab in the sidebar.
# 3. Click on the `Create repository` button.
# 4. Fill in the repository details:
#    - Repository name: `example-repo`
#    - Access level: Choose between Private or Public.
# 5. Click on the `Create repository` button.

# Task 2: Cloning a Repository
# 1. Copy the repository URL.
# 2. Open terminal.
git clone https://mukeshtp@bitbucket.org/devopslab-mukesh/devopslab.git

# Task 3: Making Changes and Creating a Branch
cd example-repo
touch test.txt
echo "This is a test file." > test.txt
git status
git add test.txt
git commit -m "Edited test.txt"
git branch feature
git checkout feature

# Task 4: Pushing Changes to Bitbucket
REPO_URL=https://mukeshtp@bitbucket.org/devopslab-mukesh/devopslab.git
git push -u origin feature

# Task 5: Collaborating through Pull Requests
# 1. Go to the Bitbucket repository.
# 2. Click on `Create pull request`.
# 3. Choose the source branch (`feature`) and the target branch (`main`).
# 4. Review the changes and create the pull request.
# 5. Add a title and description for the pull request.
# 6. Assign reviewers if needed.
# 7. Once the pull request is approved, merge it into the target branch.

# Task 6: Syncing Changes
git checkout main
git pull origin main
```

#### Output

1. **Creating a Repository**:
   - A new Bitbucket repository named `example-repo` is created with the specified details.
   ![1-1](../photos/Ex3/1-1.png?raw=true)
   ![1-2](../photos/Ex3/1-2.png?raw=true)
   ![1-3](../photos/Ex3/1-3.png?raw=true)
   ![1-4](../photos/Ex3/1-4.png?raw=true)
   ![1-5](../photos/Ex3/1-5.png?raw=true)

2. **Cloning a Repository**:
   - The repository is successfully cloned to the local machine.
   ![2-1](../photos/Ex3/2-1.png?raw=true)
   ![2-2](../photos/Ex3/2-2.png?raw=true)
   ![2-3](../photos/Ex3/2-3.png?raw=true)

3. **Making Changes and Creating a Branch**:
   - Navigated into the cloned repository.
   - `test.txt` file created and modified.
   - Changes staged and committed.
   - New branch `feature` created and switched to.
   ![3-1](../photos/Ex3/3-1.png?raw=true)
   ![3-2](../photos/Ex3/3-2.png?raw=true)
   ![3-3](../photos/Ex3/3-3.png?raw=true)
   ![3-4](../photos/Ex3/3-4.png?raw=true)
   ![3-5](../photos/Ex3/3-5.png?raw=true)
   ![3-6](../photos/Ex3/3-6.png?raw=true)
   ![3-7](../photos/Ex3/3-7.png?raw=true)
   ![3-8](../photos/Ex3/3-8.png?raw=true)

4. **Pushing Changes to Bitbucket**:
   - `feature` branch pushed to Bitbucket.
   - Verified the new branch `feature` is available in the Bitbucket repository.
   ![4-1](../photos/Ex3/4-1.png?raw=true)
   ![4-2](../photos/Ex3/4-2.png?raw=true)
   ![4-3](../photos/Ex3/4-3.png?raw=true)

5. **Collaborating through Pull Requests**:
   - Pull request created, reviewed, and merged on Bitbucket.
   ![5-1](../photos/Ex3/5-1.png?raw=true)
   ![5-2](../photos/Ex3/5-2.png?raw=true)
   ![5-3](../photos/Ex3/5-3.png?raw=true)
   ![5-4](../photos/Ex3/5-4.png?raw=true)
   ![5-5](../photos/Ex3/5-5.png?raw=true)
   ![5-6](../photos/Ex3/5-6.png?raw=true)

6. **Syncing Changes**:
   - Local repository updated with the latest changes from the remote repository.
   ![6-1](../photos/Ex3/6-1.png?raw=true)
   ![6-2](../photos/Ex3/6-2.png?raw=true)

<div style="page-break-after: always;"></div>

<table style="width: 100%; border-collapse: collapse; padding:0;">
  <tr>
    <td style="width: 20%; border: 1px solid black; padding: 0;">
      <table style="width: 100%; border-collapse: collapse; border: none;">
        <tr>
          <td style="padding-top: 0; border-bottom: 1px solid black; text-align: center; font-weight: bold; border-left: none; border-top: none; vertical-align: middle;">Ex. No. 4</td>
        </tr>
        <tr>
          <td style="padding-bottom:0; text-align: center; border-bottom: none; border-right: none; vertical-align: middle;">09/07/2024</td>
        </tr>
      </table>
    </td>
    <td style="width: 80%; border: 1px solid black; text-align: center; font-weight: bold; vertical-align: middle;">Advanced Git Commands</td>
  </tr>
</table>

#### **AIM**

Algorithm for Advanced Git Commands

#### **Algorithm**

1. **Interactive Rebase**:
   - Review the commit history using `git log --oneline`.
   - Enter interactive rebase mode with `git rebase -i HEAD~N` (where N is the number of commits).
   - Modify, edit, or squash commits as necessary to clean up the history.
   - Rebase your branch onto another branch if needed using `git rebase <branch>`.

2. **Stashing Changes**:
   - Make changes in your working directory.
   - Stash changes using `git stash`.
   - Apply the stashed changes when required using `git stash apply`.

3. **Reverting and Resetting**:
   - Create a new commit and revert it using `git revert <commit_hash>`.
   - Experiment with `git reset --soft`, `--mixed`, and `--hard` to understand the differences in resetting commit history.

4. **Cherry-Picking a Commit**:
   - Select a commit from another branch and apply it using `git cherry-pick <commit_hash>`.
   - Resolve any conflicts that arise and continue the cherry-pick process.

5. **Working with Submodules**:
   - Add a submodule to your repository using `git submodule add <repository_url> <path>`.
   - Clone a repository with submodules using `git clone --recurse-submodules <repository_url>`.
   - Update submodules using `git submodule update --remote --merge`.

6. **Implementing Git Hooks**:
   - Create a pre-commit hook in the `.git/hooks` directory to prevent commits with "TODO" comments.
   - Make the script executable and test it by attempting to commit a file with a "TODO" comment.

#### **Input**

```sh
# Task 1: Interactive Rebase
git log --oneline
git rebase -i HEAD~N
# Task 2: Stashing Changes
git stash
git stash apply
# Task 3: Reverting and Resetting
git revert <commit_hash>
git reset --soft <commit_hash>
git reset --mixed <commit_hash>
git reset --hard <commit_hash>
# Task 4: Cherry-Picking a Commit
git cherry-pick <commit_hash>
# Task 5: Working with Submodules
git submodule add <repository_url> <path>
git clone --recurse-submodules <repository_url>
git submodule update --remote --merge
# Task 6: Implementing Git Hooks
echo "#!/bin/sh
if grep -r \"TODO\" .; then
    echo \"Commit rejected: please remove TODO comments.\"
    exit 1
fi" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

#### **Output**

1. **Interactive Rebase**:
   - Successfully rebased the commit history to clean up and combine multiple commits.
   ![a-1](../photos/Ex4/a-1.png?raw=true)
   ![a-2](../photos/Ex4/a-2.png?raw=true)

2. **Stashing Changes**:
   - Successfully stashed and reapplied changes.
   ![b-1](../photos/Ex4/b-1.png?raw=true)
   ![b-2](../photos/Ex4/b-2.png?raw=true)

3. **Reverting and Resetting**:
   - Successfully reverted a commit and experimented with different reset options.
   ![c-1](../photos/Ex4/c-1.png?raw=true)
   ![c-2](../photos/Ex4/c-2.png?raw=true)
   ![c-3](../photos/Ex4/c-3.png?raw=true)

4. **Cherry-Picking a Commit**:
   - Successfully cherry-picked a commit from another branch and resolved any conflicts.
   ![d-1](../photos/Ex4/d-1.png?raw=true)
   ![d-2](../photos/Ex4/d-2.png?raw=true)

5. **Working with Submodules**:
   - Successfully added, cloned, and updated submodules in the repository.
   ![e-1](../photos/Ex4/e-1.png?raw=true)
   ![e-2](../photos/Ex4/e-2.png?raw=true)

6. **Implementing Git Hooks**:
   - Successfully created a pre-commit hook that prevents commits with "TODO" comments.
   ![f-1](../photos/Ex4/f-1.png?raw=true)
   ![f-2](../photos/Ex4/f-2.png?raw=true)

#### **Result**

By following this AIM Algorithm, you have successfully mastered advanced Git operations, including interactive rebase, stashing, reverting, resetting, cherry-picking, managing submodules, and implementing Git hooks. This exercise enhances your ability to manage commit histories effectively, collaborate efficiently, and enforce coding standards within your projects.

<div style="page-break-after: always;"></div>
