# Django Project Setup Workflow

**Stack:** `uv` · Django · Git · GitHub · pre-commit · Ruff

## 1. Create project & environment

```bash
uv init [project-name]
cd [project-name]
dir

uv python pin 3.13
uv sync
uv add django

uv run python --version
uv run django-admin --version
```

## 2. Create Django project

```bash
uv run django-admin startproject config .
uv run python manage.py check
uv run python manage.py migrate
uv run python manage.py runserver
```

## 3. Configure Git

Create `.gitignore` in the project root:

```gitignore
__pycache__/
*.py[cod]
.venv/
venv/
.env
.env.*
!.env.example
db.sqlite3
db.sqlite3-journal
media/
staticfiles/
.pytest_cache/
.ruff_cache/
.mypy_cache/
.coverage
htmlcov/
.vscode/
.idea/
.DS_Store
Thumbs.db
```

Initialize Git:

```bash
git init
git branch -M main
git status
```

## 4. Configure pre-commit & Ruff

```bash
uv add --dev pre-commit ruff
```

Create `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: local
    hooks:
      - id: ruff-check
        name: Ruff lint
        entry: uv run ruff check --fix
        language: system
        types: [python]

      - id: ruff-format
        name: Ruff format
        entry: uv run ruff format
        language: system
        types: [python]
```

Install and run hooks:

```bash
uv run pre-commit install
uv run pre-commit run --all-files
```

## 5. Initial commit

```bash
git add .
git status
git commit -m "chore: initialize Django project"
```

## 6. Connect to GitHub

Create a new GitHub repository with the same project name, **without** a README, `.gitignore`, or license.

```bash
git remote add origin https://github.com/morecoldbrewplease/YOUR_MF_REPOSITORY.git
git remote -v
git push -u origin main
```

## 7. Daily workflow

```bash
# Update dependencies
uv sync

# Check Django & run tests
uv run python manage.py check
uv run python manage.py test

# After changing models
uv run python manage.py makemigrations
uv run python manage.py migrate

# Review, commit & push
git status
git diff
git add .
git commit -m "feat: describe your change"
git push
```
