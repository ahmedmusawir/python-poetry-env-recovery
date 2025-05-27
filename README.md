# Poetry Virtual Environment Reset Guide

When your Poetry virtual environment gets corrupted or isn't working properly, follow these steps for a complete clean reset.

## 🚨 When to Use This Guide

Use this process when you encounter:
- Virtual environment activation issues
- Python path problems with Poetry
- Dependency conflicts that won't resolve
- "Environment not found" errors
- Mixed virtual environments causing confusion

## 🧹 Complete Environment Reset Process

### Step 1: Exit Current Environment
```bash
# Exit any active shell/environment
exit
```

### Step 2: Remove Poetry Environment
```bash
# Remove all virtual environments for the current project
poetry env remove --all

# Clear Poetry's package cache
poetry cache clear --all pypi
```

### Step 3: Manual Cleanup (if needed)
```bash
# List all Poetry environments to see what's left
poetry env list --full-path

# If any environments remain, manually remove them
# Replace the path with your actual environment path
rm -rf /home/username/.cache/pypoetry/virtualenvs/your-project-name-xxxxx-py3.xx
```

### Step 4: Fresh Environment Creation
```bash
# Navigate to your project directory
cd ~/path/to/your/project

# Create fresh virtual environment and install dependencies
poetry install --no-root

# Activate the new environment
poetry shell
```

### Step 5: Verify Everything Works
```bash
# Check Python path (should point to Poetry's virtual environment)
which python

# Verify environment details
poetry env info

# Test your application
python -m your_module.main  # or whatever your entry point is
```

## ✅ Success Indicators

After following these steps, you should see:

1. **Correct Python Path**: `which python` should show a path like:
   ```
   /home/username/.cache/pypoetry/virtualenvs/project-name-xxxxx-py3.xx/bin/python
   ```

2. **Valid Environment Info**: `poetry env info` should show:
   ```
   Virtualenv
   Python:         3.xx.x
   Implementation: CPython
   Path:           /home/username/.cache/pypoetry/virtualenvs/project-name-xxxxx-py3.xx
   Executable:     /home/username/.cache/pypoetry/virtualenvs/project-name-xxxxx-py3.xx/bin/python
   Valid:          True
   ```

3. **Working Application**: Your Python modules should import and run correctly.

## 🔧 Common Variations

### For Specific Python Version
```bash
# If you need a specific Python version
poetry env use python3.12
poetry install --no-root
```

### For Development Dependencies
```bash
# Include development dependencies
poetry install --with dev
```

### Skip Lock File Update
```bash
# If you don't want to update poetry.lock
poetry install --no-root --no-update
```

## 💡 Prevention Tips

- Always use `poetry shell` to activate environments rather than manual activation
- Don't mix `pip` and `poetry` for package management in the same project
- Use `poetry run python your_script.py` for one-off commands instead of activating the shell
- Keep your `pyproject.toml` and `poetry.lock` files in version control

## 🆘 Still Having Issues?

If this process doesn't resolve your issues:

1. Check your Poetry version: `poetry --version`
2. Update Poetry: `curl -sSL https://install.python-poetry.org | python3 -`
3. Verify your Python installation: `python --version`
4. Check for system-level Python conflicts
5. Consider using a Python version manager like `pyenv` for better isolation

---

*This guide is based on resolving Poetry virtual environment corruption issues. Keep this handy for future troubleshooting!*
