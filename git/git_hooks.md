# Using Git Hooks in Flutter Projects

## What are Git Hooks?

Git hooks are scripts that Git automatically executes before or after specific events (like commit, push, etc.). They help enforce rules or automate workflows in your codebase.

## Why Use Git Hooks in Flutter Projects?

Using Git hooks in a Flutter project can:

* Ensure code quality (e.g., format and lint before committing)
* Prevent committing debug prints or unwanted files
* Enforce commit message conventions
* Help junior developers follow team coding standards

## Common Hooks You Can Use

* `pre-commit`: Runs before a commit is made. Great for linting and formatting code.
* `commit-msg`: Validates commit messages.
* `pre-push`: Checks tests or ensures code builds before pushing.

---

## Step-by-Step Guide to Implement Git Hooks in Flutter

### Step 1: Create a `.git/hooks` Script

1. Navigate to your project folder.
2. Go to the `.git/hooks` directory.
3. Create or modify the hook file, e.g., `pre-commit`, and make it executable:

```bash
cd .git/hooks
touch pre-commit
chmod +x pre-commit
```

### Step 2: Add Your Script

Here's an example `pre-commit` script to check formatting and linting:

```bash
#!/bin/sh

echo "Running Flutter format check..."
flutter format --set-exit-if-changed .

if [ $? -ne 0 ]; then
  echo "Formatting issues found. Please run flutter format."
  exit 1
fi

echo "Running Flutter analyze..."
flutter analyze

if [ $? -ne 0 ]; then
  echo "Analysis failed. Fix the issues before committing."
  exit 1
fi

exit 0
```

This prevents commits if the code is not formatted or has analysis issues.

---

### Step 3: Share Hooks with Team

Git doesn’t track `.git/hooks` by default. To share hooks with your team:

1. Create a `hooks/` folder in the root of your project.
2. Add your hook scripts there (e.g., `hooks/pre-commit`).
3. Create a setup script to install them:

```bash
#!/bin/sh
cp hooks/* .git/hooks/
chmod +x .git/hooks/*
echo "Hooks installed!"
```

4. Ask juniors to run this setup script once:

```bash
sh setup_hooks.sh
```

---

## How This Helps Junior Developers

* Ensures they write clean, formatted, and error-free code.
* Reduces need for code review comments on basics.
* Automates tedious checks.
* Reinforces discipline in workflow (e.g., writing good commit messages).

---

## Tips

* You can use packages like `lefthook` or `husky` (via Node.js) for better management.
* Integrate testing (`flutter test`) in `pre-push` hook.
* Educate juniors on what each script does.

---

## Conclusion

Git hooks are a powerful way to automate and enforce best practices in your Flutter projects. Set them up once and enjoy cleaner, safer code — especially helpful when working with junior developers.