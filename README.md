all these steps are after create a new vault and cd to it
create a vault
uv init [vault's name]

change directory
cd [directory]

check generated files
dir

add python version
uv python 3.13 [py ver]

create synchronizes .venv-uv.lock
uv sync

add Django
uv add Django

verify installation
uv run python --version
uv run django-admin --version

create Django prj with config vault
uv run django-admin startproject config .

check if everything correct
uv run python manage.py check
uv run python manage.py migrate
uv run python manage.py runserver

reate a .gitignore file in the project root before committing

initialize Git
git init
git branch -m main
git status

install and config pre-commit
uv add --dev pre-commit ruff

create .pre-commit-config.yaml in the root directory

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

install git hook
uv run pre-commit install

run all config check
uv run pre-commit run --all-files
git 
make init commit
git add .
git status
git commit -m ""

On GitHub, create a new repository with the same project name, wo readme, ignore
git remote add origin https://github.com/morecoldbrewplease/kafi.git
git remote -v
git push -u origin main
