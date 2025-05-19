# GitHub Commands Guide (Beginner to Advanced)

This guide explains **37 essential Git commands** in simple, easy-to-understand language with use cases and examples.

---

## Basic Git Commands

### 1. `git init`

* **Use**: To initialize a new Git repository in your project folder.
* **Example**:

  ```bash
  git init
  ```

### 2. `git clone`

* **Use**: To copy (clone) an existing repository from GitHub to your local system.
* **Example**:

  ```bash
  git clone https://github.com/user/repo.git
  ```

### 3. `git status`

* **Use**: To check the current status of your repository (changes, staged files, etc).
* **Example**:

  ```bash
  git status
  ```

### 4. `git add`

* **Use**: To stage files before committing.
* **Examples**:

  ```bash
  git add filename.txt       # Single file
  git add .                  # All files
  ```

### 5. `git commit`

* **Use**: To save staged changes with a message.
* **Example**:

  ```bash
  git commit -m "Added login feature"
  ```

### 6. `git log`

* **Use**: To see commit history.
* **Example**:

  ```bash
  git log
  ```

### 7. `git diff`

* **Use**: To view file differences (unstaged or between commits).
* **Example**:

  ```bash
  git diff
  ```

### 8. `git checkout`

* **Use**: To switch branches or revert files.
* **Examples**:

  ```bash
  git checkout main          # Switch to main branch
  git checkout filename.txt  # Discard file changes
  ```

### 9. `git branch`

* **Use**: To view, create or delete branches.
* **Examples**:

  ```bash
  git branch                 # View branches
  git branch new-feature     # Create new branch
  ```

### 10. `git merge`

* **Use**: To merge changes from one branch into another.
* **Example**:

  ```bash
  git merge new-feature
  ```

### 11. `git remote`

* **Use**: To manage remote repository links.
* **Example**:

  ```bash
  git remote add origin https://github.com/user/repo.git
  ```

### 12. `git push`

* **Use**: To upload your changes to GitHub.
* **Example**:

  ```bash
  git push origin main
  ```

### 13. `git pull`

* **Use**: To fetch and merge changes from GitHub.
* **Example**:

  ```bash
  git pull origin main
  ```

### 14. `git fetch`

* **Use**: To download changes from remote without merging.
* **Example**:

  ```bash
  git fetch
  ```

### 15. `git reset`

* **Use**: To unstage changes or reset commits.
* **Examples**:

  ```bash
  git reset filename.txt       # Unstage file
  git reset --hard HEAD~1      # Delete last commit
  ```

### 16. `git revert`

* **Use**: To undo a commit by creating a new one.
* **Example**:

  ```bash
  git revert abc123
  ```

  > Use when you want to keep history clean and not delete commit.

### 17. `git stash`

* **Use**: Temporarily save changes without committing.
* **Example**:

  ```bash
  git stash
  git stash pop
  ```

### 18. `git tag`

* **Use**: To mark specific commits (like a release).
* **Example**:

  ```bash
  git tag v1.0
  git push origin v1.0
  ```

---

## Intermediate Git Commands

### 19. `git cherry-pick`

* **Use**: To copy a specific commit from one branch to another.
* **Example**:

  ```bash
  git cherry-pick abc123
  ```

### 20. `git rebase`

* **Use**: To move or combine commits.
* **Example**:

  ```bash
  git rebase main
  ```

### 21. `git reflog`

* **Use**: To view history of HEAD and restore lost commits.
* **Example**:

  ```bash
  git reflog
  ```

### 22. `git clean`

* **Use**: To delete untracked files.
* **Example**:

  ```bash
  git clean -f
  ```

### 23. `git describe`

* **Use**: To describe a commit using the nearest tag.
* **Example**:

  ```bash
  git describe
  ```

### 24. `git shortlog`

* **Use**: To see summary of commits by author.
* **Example**:

  ```bash
  git shortlog
  ```

### 25. `git bisect`

* **Use**: To find the commit that introduced a bug.
* **Example**:

  ```bash
  git bisect start
  git bisect bad
  git bisect good abc123
  ```

---

## Advanced Git Commands

### 26. `git archive`

* **Use**: To create zip/tar of your repository.
* **Example**:

  ```bash
  git archive --format=zip --output=code.zip main
  ```

### 27. `git worktree`

* **Use**: Work on multiple branches at once in separate folders.
* **Example**:

  ```bash
  git worktree add ../new-folder new-feature
  ```

### 28. `git submodule`

* **Use**: To add another repository inside your project.
* **Example**:

  ```bash
  git submodule add https://github.com/example/repo libs/repo
  ```

### 29. `git fsck`

* **Use**: To check repository for corruption.
* **Example**:

  ```bash
  git fsck
  ```

### 30. `git bundle`

* **Use**: Share a repo as a single file without remote.
* **Example**:

  ```bash
  git bundle create repo.bundle --all
  git clone repo.bundle new-folder -b main
  ```

### 31. `git blame --show-email`

* **Use**: See who wrote each line of a file (with email).
* **Example**:

  ```bash
  git blame --show-email filename.txt
  ```

### 32. `git diff --word-diff`

* **Use**: View changes word-by-word instead of line-by-line.
* **Example**:

  ```bash
  git diff --word-diff
  ```

### 33. `git log --graph`

* **Use**: Visual representation of commits and branches.
* **Example**:

  ```bash
  git log --graph --oneline --all
  ```

### 34. `git notes`

* **Use**: Add notes to a commit without changing it.
* **Example**:

  ```bash
  git notes add -m "Related to bug #101"
  git notes show
  ```

### 35. `git rerere`

* **Use**: Auto-resolve previously resolved merge conflicts.
* **Enable**:

  ```bash
  git config rerere.enabled true
  ```

### 36. `git gc`

* **Use**: Clean up unnecessary files to optimize repo.
* **Example**:

  ```bash
  git gc --aggressive
  ```

### 37. `git config`

* **Use**: Customize Git settings.
* **Examples**:

  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "email@example.com"
  git config --global alias.st status
  git st
  ```

---

✅ **Pro Tip**: Use `git help <command>` anytime to get documentation for any Git command.

---

> This markdown file is made for deep understanding of Git from beginner to advanced level. You can use it as a reference for your day-to-day Git tasks.