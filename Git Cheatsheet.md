## Setup and Configurations
```bash
# Set user name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Check configuration
git config --list

# Set default editor
git config --global core.editor "vim"
```

## Creating and Cloning Repositories
```bash
# Initialize a new Git repository
git init

# Clone a repository
git clone <repository_url>

# Clone a repository with a specific branch
git clone -b <branch_name> <repository_url>
```

## Basic Commands
```bash
# Check repository status
git status

# Add files to staging area
git add <file_name>

# Add all files to staging area
git add .

# Commit changes
git commit -m "Commit message"

# View commit history
git log

# View a concise log
git log --oneline
```

## Branching and Merging
```bash
# Create a new branch
git branch <branch_name>

# Switch to a branch
git checkout <branch_name>

# Create and switch to a new branch
git checkout -b <branch_name>

# Create and switch to a new branch
git switch -c <branch_name>

# Merge a branch into the current branch
git merge <branch_name>

# Delete a branch
git branch -d <branch_name>
```

## Remote Repositories
```bash
# Add a remote repository
git remote add origin <repository_url>

# View remote repositories
git remote -v

# Push changes to a remote repository
git push origin <branch_name>

# Pull changes from a remote repository
git pull origin <branch_name>

# Fetch changes from a remote repository
git fetch origin
```

## Stashing Changes
```bash
# Stash current changes
git stash

# List stashes
git stash list

# Apply the most recent stash
git stash apply

# Apply and drop the most recent stash
git stash pop

# Drop a specific stash
git stash drop stash@{index}
```

## Undoing Changes
```bash
# Unstage a file
git reset <file_name>

# Unstage all files
git reset

# Revert to a previous commit
git revert <commit_hash>

# Reset to a previous commit (destructive)
git reset --hard <commit_hash>

# Discard changes in a file
git checkout -- <file_name>
```

## Tagging
```bash
# Create a lightweight tag
git tag <tag_name>

# Create an annotated tag
git tag -a <tag_name> -m "Tag message"

# List all tags
git tag

# Push tags to remote
git push origin <tag_name>

# Push all tags to remote
git push origin --tags
```

## Useful Logs and Diffs
```bash
# Show changes in working directory
git diff

# Show changes between commits
git diff <commit1_hash> <commit2_hash>

# Show commit history for a file
git log -- <file_name>

# View a specific commit
git show <commit_hash>
```

## Miscellaneous
```bash
# Clean untracked files
git clean -f

# Clean untracked files and directories
git clean -fd

# View a file from a specific commit
git show <commit_hash>:<file_path>

# Alias for a frequently used command
git config --global alias.<alias_name> '<command>'

# Example: Create an alias for `git log --oneline`
git config --global alias.lg 'log --oneline'
