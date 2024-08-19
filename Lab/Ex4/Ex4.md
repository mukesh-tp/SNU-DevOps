# DevOps Lab - Mukesh T P

## Exercise 4

## Exploring Git Commands through Collaborative Coding – Advanced Git Commands

### a. Use Interactive Rebase to Combine Multiple Commits into One

#### Use `git rebase -i` to Modify the Commit History

1. Check the commit history to identify the range of commits to rebase:

   ```bash
   git log --oneline
   ```

   ![a-1](../photos/Ex4/a-1.png?raw=true)

2. Start an interactive rebase for the last N commits (replace N with the number of commits):

   ```bash
   git rebase -i HEAD~N
   ```

   ![a-2](../photos/Ex4/a-2.png?raw=true)
   ![a-3](../photos/Ex4/a-3.png?raw=true)

3. In the interactive rebase interface, change `pick` to `edit` or `squash` as needed to edit messages or combine commits.
   - `edit`: Modify the commit message or contents.
   - `squash`: Combine the commit with the previous one.

   ![a-4](../photos/Ex4/a-4.png?raw=true)

#### Rebase onto Another Branch

1. Create a new branch from an earlier point in your commit history:

   ```bash
   git checkout -b new-branch <commit_hash>
   ```

   ![a-5](../photos/Ex4/a-5.png?raw=true)

2. Rebase the `main` branch onto this new branch:

   ```bash
   git rebase main
   ```

   ![a-6](../photos/Ex4/a-6.png?raw=true)

### b. Stash Changes

1. Make some changes in your working directory.
   ![b-1](../photos/Ex4/b-1.png?raw=true)

2. Stash those changes:

   ```bash
   git stash
   ```

   ![b-2](../photos/Ex4/b-2.png?raw=true)

3. Apply the stash:

   ```bash
   git stash apply
   ```

   ![b-3](../photos/Ex4/b-3.png?raw=true)

### c. Revert and Reset

1. Create a new commit:

   ```bash
   echo "New change" >> file.txt
   git add file.txt
   git commit -m "New change"
   ```

   ![c-1](../photos/Ex4/c-1.png?raw=true)

2. Revert the commit:

   ```bash
   git revert <commit_hash>
   ```

   ![c-2](../photos/Ex4/c-2.png?raw=true)
   ![c-3](../photos/Ex4/c-3.png?raw=true)

3. Experiment with `git reset` to understand the differences:
   - `--soft`: Resets the commit history but keeps the changes staged.

     ```bash
     git reset --soft <commit_hash>
     ```

   ![c-4](../photos/Ex4/c-4.png?raw=true)

   - `--mixed`: Resets the commit history and unstages the changes.

     ```bash
     git reset --mixed <commit_hash>
     ```

   ![c-5](../photos/Ex4/c-5.png?raw=true)

   - `--hard`: Resets the commit history and discards the changes.

     ```bash
     git reset --hard <commit_hash>
     ```

   ![c-6](../photos/Ex4/c-6.png?raw=true)

### d. Cherry-Pick a Commit

1. Cherry-pick a commit from another branch:

   ```bash
   git cherry-pick <commit_hash>
   ```

2. Resolve conflicts if any occur during cherry-picking:
   - Edit the conflicting files.
   - Stage the resolved files:

     ```bash
     git add <resolved_file>
     ```

   - Continue the cherry-pick:

     ```bash
     git cherry-pick --continue
     ```

### e. Working with Submodules

1. In your repository, add another repository as a submodule:

   ```bash
   git submodule add <repository_url> <path>
   ```

2. Clone a repository with submodules:

   ```bash
   git clone --recurse-submodules <repository_url>
   ```

3. Update and synchronize submodules:

   ```bash
   git submodule update --remote --merge
   ```

### f. Git Hooks

#### Create a Pre-Commit Hook that Prevents Commits with “TODO” Comments

1. Create a file named `pre-commit` in the `.git/hooks` directory with the following script:

   ```sh
   #!/bin/sh
   if grep -r "TODO" .; then
       echo "Commit rejected: please remove TODO comments."
       exit 1
   fi
   ```

2. Make the script executable:

   ```bash
   chmod +x .git/hooks/pre-commit
   ```

3. Try committing a file with a TODO comment to see the hook in action.

#### Explore Other Types of Hooks

1. Create simple scripts for other hooks like post-merge, pre-push, or post-checkout:
   - For a `pre-push` hook, create a file named `pre-push` in the `.git/hooks` directory with the following script:

     ```sh
     #!/bin/sh
     echo "This is a pre-push hook"
     ```

   - Make the script executable:

     ```bash
     chmod +x .git/hooks/pre-push
     ```
