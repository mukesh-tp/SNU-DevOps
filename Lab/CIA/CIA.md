# CIA

### 1. **Getting Started with Git**

- **Initialize a Repository:**
  - `git init`: Initializes a new Git repository in the current directory. This creates a `.git` directory where all the Git-related data is stored.

- **Clone a Repository:**
  - `git clone <repository-url>`: Clones an existing Git repository from a URL (like GitHub) to your local machine.

### 2. **Basic Commands**

- **Check Status:**
  - `git status`: Shows the status of your working directory and staging area. It tells you what changes have been staged, which haven’t, and files that aren't being tracked by Git.

- **Add Files:**
  - `git add <file>`: Adds the specified file to the staging area.
  - `git add .`: Adds all modified and new files in the current directory to the staging area.

- **Commit Changes:**
  - `git commit -m "commit message"`: Commits the staged changes with a descriptive message.

### 3. **Working with Branches**

- **Create a New Branch:**
  - `git branch <branch-name>`: Creates a new branch with the given name.
  - `git checkout -b <branch-name>`: Creates and switches to a new branch.

- **Switch Branches:**
  - `git checkout <branch-name>`: Switches to the specified branch.

- **Merge Branches:**
  - `git merge <branch-name>`: Merges the specified branch into the current branch.

### 4. **Viewing History**

- **Log History:**
  - `git log`: Shows the commit history for the repository.
  - `git log --oneline`: Displays the commit history in a condensed, single-line format per commit.

- **Show Differences:**
  - `git diff`: Shows the differences between your working directory and the staging area.
  - `git diff <branch1> <branch2>`: Shows the differences between two branches.

### 5. **Undoing Changes**

- **Unstage a File:**
  - `git reset <file>`: Removes the specified file from the staging area but keeps the changes in the working directory.

- **Revert to a Previous Commit:**
  - `git revert <commit>`: Creates a new commit that undoes the changes from the specified commit.

- **Reset a Branch:**
  - `git reset --hard <commit>`: Resets the current branch to the specified commit and discards all changes after that commit.

### 6. **Remote Repositories**

- **View Remotes:**
  - `git remote -v`: Lists the remote repositories linked to your local repository.

- **Push Changes:**
  - `git push origin <branch-name>`: Pushes changes from your local branch to the remote repository.

- **Pull Changes:**
  - `git pull`: Fetches and merges changes from the remote repository into your current branch.

### 7. **Stashing Changes**

- **Stash Changes:**
  - `git stash`: Temporarily saves your changes and cleans your working directory.
  - `git stash apply`: Applies the stashed changes back to your working directory.

### 8. **Tagging**

- **Create a Tag:**
  - `git tag <tagname>`: Creates a tag at the current commit.
  - `git tag -a <tagname> -m "message"`: Creates an annotated tag with a message.

### Quick Tips:

- Always write meaningful commit messages.
- Regularly check your `git status` to stay on top of changes.
- Make sure to pull the latest changes before starting new work on a project.

### Levels of Git Configuration

Git configurations can be set at three different levels:

1. **System Level (`--system`)**:
   - Applies to all users on the system. Typically set by a system administrator.
   - Configuration file: `/etc/gitconfig` or in Git's installation directory on Windows.

2. **Global Level (`--global`)**:
   - Applies to all repositories for a single user.
   - Configuration file: `~/.gitconfig` or `~/.config/git/config` on Linux/macOS, or `C:\Users\YourName\.gitconfig` on Windows.

3. **Local Level (`--local`)**:
   - Applies only to the specific repository where the configuration is set.
   - Configuration file: `.git/config` inside the repository directory.

### Common Configuration Settings

Here are some commonly used Git configurations:

1. **Set Your Username:**
   - `git config --global user.name "Your Name"`
   - This sets the name that will be associated with your commits. It’s a good idea to set this globally.

2. **Set Your Email:**
   - `git config --global user.email "you@example.com"`
   - This sets the email address associated with your commits. Like the username, it's typically set globally.

3. **Set the Default Text Editor:**
   - `git config --global core.editor "editor"`
   - Sets the default text editor for Git (e.g., Vim, Nano, VS Code). Example: `git config --global core.editor "code --wait"` to use VS Code.

4. **Set the Default Merge Tool:**
   - `git config --global merge.tool "tool"`
   - Specifies the tool Git should use for resolving merge conflicts.

5. **Coloring Git Output:**
   - `git config --global color.ui auto`
   - Enables color coding in Git command output to improve readability.

6. **Viewing the Configuration:**
   - `git config --list`: Displays all the current configuration settings.
   - `git config <key>`: Displays the value for a specific configuration key.

7. **Alias Commands:**
   - `git config --global alias.st status`: Creates a shorthand alias so you can use `git st` instead of `git status`.
   - You can create aliases for any Git command.

### Example Configuration

Here’s an example of what a global configuration might look like:

```ini
[user]
    name = Mukesh T P
    email = mukeshtp2004@gmail.com
[core]
    editor = nano
[alias]
    co = checkout
    br = branch
    ci = commit
    st = status
[color]
    ui = auto
```

### Editing the Configuration Files Directly

You can manually edit the configuration files if needed:

- For global settings, open `~/.gitconfig` in your favorite text editor.
- For local settings, open `.git/config` in the repository directory.

### Resetting Configuration

If you want to unset or remove a configuration:

- `git config --global --unset <key>`: Unsets a global configuration.
- `git config --global --remove-section <section>`: Removes an entire section from the configuration.

### Practical Tips:

- Make sure your `user.name` and `user.email` are set before you start committing changes.
- Use aliases to speed up common Git commands.
- Configurations like `core.autocrlf` can help with line ending issues across different operating systems.
