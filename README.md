# 🧮 Python Addition Project with GitHub Actions

## 📘 Project Overview
This project demonstrates a simple **Python addition function** with automated testing using **GitHub Actions**.  
Whenever you push code or create a pull request, the workflow automatically runs tests to ensure everything works properly across multiple Python versions.

---

## 🧩 Folder Structure
```
my-python-project/
│
├── add.py                 # Python function for addition
├── test_add.py            # Test cases using pytest
├── requirements.txt       # Project dependencies
└── .github/
    └── workflows/
        └── main.yml       # GitHub Actions workflow file
```

---

## ⚙️ GitHub Actions Workflow

### 📍 File Location
`.github/workflows/main.yml`

### 🧠 Workflow Explanation
```yaml
name: Python Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version: ['3.10', '3.11']

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run pytest
        run: pytest -v --maxfail=1 --disable-warnings
```

### 🧾 Step-by-Step Workflow

1. **Trigger** – The workflow runs when you push to the `main` branch, open a pull request, or manually trigger it from the Actions tab.  
2. **Environment Setup** – GitHub Actions creates a fresh Ubuntu environment and installs Python versions 3.10 and 3.11.  
3. **Dependency Installation** – Installs all packages from `requirements.txt` (like `pytest`).  
4. **Run Tests** – Executes all test cases automatically.  
5. **Result** – Displays the outcome in the **Actions tab** and marks the commit or PR as passed ✅ or failed ❌.

---

## 🧪 Example Code

**`add.py`**
```python
def add(a, b):
    return a + b
```

**`test_add.py`**
```python
from add import add

def test_add_positive_numbers():
    assert add(2, 3) == 5

def test_add_negative_numbers():
    assert add(-2, -3) == -5

def test_add_mixed_numbers():
    assert add(-2, 3) == 1
```

---

## ✅ Run Tests Locally
Before pushing to GitHub, you can test locally:

```bash
pip install -r requirements.txt
pytest -v
```

Expected output:
```
================== test session starts ==================
collected 3 items

test_add.py ...                                          [100%]

=================== 3 passed in 0.01s ===================
```

---

## 🟢 GitHub Actions Status Badge
Add this badge to the top of your README to show your workflow status:

```markdown
![Python Tests](https://github.com/<YOUR_USERNAME>/<YOUR_REPO_NAME>/actions/workflows/main.yml/badge.svg)
```
Replace `<YOUR_USERNAME>` and `<YOUR_REPO_NAME>` with your actual GitHub username and repository name.

---

## 🏁 Summary

✅ Automatically runs tests for every push or pull request  
✅ Ensures compatibility across Python 3.10 and 3.11  
✅ Verifies code quality and correctness using pytest  
✅ Implements Continuous Integration (CI) best practices  

With this setup, your repository automatically tests your code, ensuring every change remains reliable and bug-free! 🎉
