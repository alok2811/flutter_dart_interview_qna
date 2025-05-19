# Using Git Hooks in Flutter Projects (Without Third-Party Libraries)

Git hooks are scripts that run automatically at certain points in the Git lifecycle (e.g., before committing, after merging, etc.). They're useful for enforcing coding standards, formatting code, or preventing bad commits—especially helpful when working with junior developers.

---

## ✅ Benefits of Using Git Hooks with Junior Developers

* Enforces coding and formatting standards.
* Prevents bad code from being committed.
* Helps automate repetitive tasks (e.g., running tests, linting).
* Acts as a safety net before code goes into the repository.

---

## 🛠 Step-by-Step: Implement Git Hooks in Flutter

### Step 1: Navigate to the `.git/hooks` directory

In your Flutter project root, navigate to:

```bash
cd .git/hooks
```

This folder contains sample hook scripts like `pre-commit.sample`, `pre-push.sample`, etc.

### Step 2: Create or Modify Hook Files

Rename or create a new hook script. For example:

```bash
mv pre-commit.sample pre-commit
```

Make it executable:

```bash
chmod +x pre-commit
```

### Step 3: Add Your Flutter-Specific Script

Edit the `pre-commit` file:

```bash
nano pre-commit
```

Example content:

```bash
#!/bin/sh

# Format Dart code before commit
echo "Running flutter format..."
flutter format .

# Run analyzer to catch errors
echo "Running flutter analyze..."
flutter analyze

# If the analyzer fails, reject the commit
if [ $? -ne 0 ]; then
  echo "Code analysis failed. Please fix the issues before committing."
  exit 1
fi

echo "Pre-commit checks passed."
exit 0
```

### Step 4: Try a Commit

Try committing some changes:

```bash
git add .
git commit -m "Test commit with hooks"
```

You’ll see the script automatically formats and analyzes your code.

---

## 🔧 Commonly Used Git Hooks and Their Use Cases

| Hook                 | Trigger Point                      | Common Use Cases                                           |
| -------------------- | ---------------------------------- | ---------------------------------------------------------- |
| `pre-commit`         | Before `git commit`                | Format, lint, run tests, prevent bad code                  |
| `prepare-commit-msg` | Before commit message editor opens | Auto-fill commit messages with ticket ID                   |
| `commit-msg`         | After commit message entered       | Enforce message formats (e.g., Conventional Commits)       |
| `pre-push`           | Before `git push`                  | Run tests, ensure no debug prints, prevent pushing to main |
| `post-merge`         | After `git merge`                  | Auto-install packages, show success message                |
| `post-checkout`      | After switching branches           | Show branch-specific info, sync dependencies               |

---

## 👨‍💻 Best Practices for Flutter Teams

* **Share hooks via template:** Store your custom hooks in a shared directory like `.githooks` and configure Git to use them:

```bash
git config core.hooksPath .githooks
```

* **Always commit executable scripts**
* **Use hooks to enforce team-wide quality** (lint rules, tests, code format)
* **Avoid third-party libraries** unless necessary for larger teams

---

## 🧪 Sample `pre-push` Hook

```bash
#!/bin/sh

# Run flutter test before push
echo "Running tests before push..."
flutter test

if [ $? -ne 0 ]; then
  echo "Tests failed. Push rejected."
  exit 1
fi

echo "All tests passed. Proceeding with push."
exit 0
```

---

## ✅ Summary

Git hooks are powerful automation tools for maintaining code quality and helping junior developers stay within best practices without extra tools. You can:

* Format and analyze code before commit.
* Prevent pushes with failing tests.
* Standardize commit messages.

All without needing any extra libraries.