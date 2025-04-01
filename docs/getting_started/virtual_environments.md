# Comparison
For fresh projects you have two options in 2025, `venv` or `Poetry`. What to use depends on the project you are going for as `Poetry` can do a lot more than `venv` does.

Both aim to solve **Python environment isolation**, but Poetry is a **higher-level tool** (1) that also handles **package management, dependency resolution, and publishing** whereas `venv` only handles the Python environment.
{ .annotate }

1. Higher-level tool refers to how much functionality is abstracted away or automated for the user.

---

## What Is `venv`?
The purpose of `venv` is to create isolated Python environments. Which have the following benefits:
- Prevents dependency conflicts between projects
- Allows you to have multiple Python versions or library sets side-by-side

However, it doesn't handle dependency resolution — you still use `pip` + `requirements.txt`

### Typical Usage
```bash
python -m venv .venv
source .venv/bin/activate
pip install requests
pip install black
```

You manage packages manually and freeze (lock their versions) with:
```bash
pip freeze > requirements.txt
```

---

## What Is `poetry`?
The purpose of `poetry` is also to create isolated Python environments, but it does a bunch more than just this - it's basically an End-to-end Python project management tool, which accomplishes the following:

- **Creates virtual environments** (like `venv`)
- **Manages dependencies** via `pyproject.toml` (instead of `requirements.txt`)
- **Resolves dependency trees** (like `pip-tools`, but built-in)
- **Can build and publish packages** to PyPI or private registries
- **Better reproducibility** with `poetry.lock`

### Typical Usage:
```bash
poetry new myproject
cd myproject
poetry add requests
poetry add black --group dev
poetry run python script.py
```

It automatically creates and uses its own **isolated virtual environment** (unless you tell it not to).

---

## Key Differences

| Feature | `venv`                  | `poetry` |
|--------|-------------------------|---------|
| **Creates virtual environments** | ✅                       | ✅ |
| **Manages dependencies** | ❌ (you use pip manually) | ✅ |
| **Resolves dependency versions** | ❌                       | ✅ |
| **Generates lock file** | ❌                       | ✅ (`poetry.lock`) |
| **Package publishing** | ❌                       | ✅ |
| **Uses `pyproject.toml`** | ❌                       | ✅ |
| **Dev dependencies separation** | ❌ (not built-in)        | ✅ (`--group dev`) |
| **Reproducible builds** | ❌                       | ✅ |
| **Interactive CLI commands** | ❌                       | ✅ (like `poetry shell`, `poetry run`) |

---

## So, Are They Similar?
Yes, but with a big distinction:

> `venv` is only about isolation and is built into Python - you don't need to install anything.  
> `Poetry` is a full **project toolchain manager** (including isolation) and has to bee installed seperately from Python.

---

## When to use either?

| Situation                                          | Use This         |
|----------------------------------------------------|------------------|
| Simple script or project, or ad hoc work           | `venv`           |
| Building an application, library, or internal tool | `poetry`         |
| Need lock files, dev dependencies, publishing      | `poetry`         |


