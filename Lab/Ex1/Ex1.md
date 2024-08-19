# DevOps Lab - Mukesh T P

## Exercise 1

### Task 1 - Exploring Git Commands through Collaborative Coding – Basic Git commands

#### a. Create a Repository

- Setting up a Git repository named "Master".

  ```sh
  git init
  ```

  ![1a](../photos/Ex1/1a.png?raw=true)

#### b. Add and Commit Changes

- Create a new text file named `ReadMe.txt` using any text editor.

  ```sh
  touch README.md
  ls
  ```

![1b](../photos/Ex1/1b.png?raw=true)

#### c. Exploring History

- Modify or add content to the text file.

  ```sh
  echo "# This is the readme file for devops" › README md
  git add README. md
  git commit -m "Added README. md"
  ```

![1c](../photos/Ex1/1c.png?raw=true)

#### d. Branching and Merging

- Create a new branch named `Updated_ReadMe` and commit the changes in the branch.
- Merge the changes from the `Updated_ReadMe` branch into the `Master` branch.

  ```sh
  git checkout Updated_README
  echo "# This is the README file for DevOps" > README. md
  git add README. md
  git commit -m "Corrected content of README. md"
  git checkout main
  git merge Updated_README

  ```

![1d](../photos/Ex1/1d.png?raw=true)

#### e. Collaborating with Remote Repositories

- Link your local repository to the remote repository.

  ```sh
  git remote add origin https://github.com/mukesh-tp/SNU-DevOps.git
  ```

![1e](../photos/Ex1/1e.png?raw=true)

#### f. Push Changes

- Push your local commits to the remote repository.

  ```sh
  git branch -M main
  git push -u origin main
  ```

![1f](../photos/Ex1/1f.png?raw=true)

---

### Task 2 - Implement GitHub Operations using Git

#### a. Cloning a Repository

- Clone the repository of your project from GitHub.

  ```sh
  git clone https://github.com/mukesh-tp/WebTechLab.git
  ```

![2a](../photos/Ex1/2a.png?raw=true)

#### b. Making Changes and Creating a Branch

- Navigate into the cloned repository, make the necessary changes, and check the status of the repository.

  ```sh
  cd WebTechLab
  touch README. md
  echo "# This is the README file for WebTechLab" > README. md
  git status
  ```

![2b](../photos/Ex1/2b.png?raw=true)

#### c. Pushing Changes to GitHub

- Add the repository URL to a variable.
- Push the local branch to the repository.

  ```sh
  remote_url="https://github.com/mukesh-tp/WebTechLab.git"
  git add .
  git commit -m "Added README. md"
  git push -u origin main
  ```

![2c](../photos/Ex1/2c.png?raw=true)

#### d. Collaborating through Pull Requests

- Create a pull request on GitHub.
- Choose the base branch and compare it with the new branch.
- Review the changes and merge the pull request.
- Add a title and description for the pull request.
- Assign reviewers.
- Reviewers approve the pull request and merge it into the base branch.

![2d](../photos/Ex1/2d.png?raw=true)

#### e. Syncing Changes

- After the pull request is merged, update your local repository.

  ```sh
  git pull origin main
  ```

![2e](../photos/Ex1/2e.png?raw=true)

---

## Author

- Mukesh T P

## Details

- Last Updated: 2024-07-12
- Registration No. - 21011102064
- Class - IoT B
