# Contributing to Naukrox 🚀

First off — **thank you** for taking the time to contribute! Naukrox is built by the community, for the community.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Branching Strategy](#branching-strategy)
- [Commit Message Format](#commit-message-format)
- [Pull Request Process](#pull-request-process)
- [Style Guide](#style-guide)

---

## Code of Conduct

By participating in this project, you agree to be respectful, inclusive, and constructive.
Harassment of any kind will not be tolerated.

---

## How Can I Contribute?

### 🐛 Reporting Bugs

- Check if the issue already exists in [GitHub Issues](https://github.com/yourusername/naukrox/issues)
- If not, open a new issue using the **Bug Report** template
- Include: steps to reproduce, expected vs actual behaviour, OS, Python version

### 💡 Suggesting Features

- Open an issue using the **Feature Request** template
- Explain the use case clearly — why would this help other users?

### 🔧 Contributing Code

1. Look for issues labelled `good first issue` or `help wanted`
2. Comment on the issue to claim it
3. Fork, branch, code, test, and open a PR

### 📖 Improving Docs

- Fix typos, improve clarity, add examples
- Documentation PRs are always welcome and fast to review

### 🧪 Writing Tests

- We currently have no test coverage — adding `pytest` tests is a high-value contribution

---

## Development Setup

### Requirements

- Python 3.11+
- Docker Desktop
- Git

### Local Setup

```bash
# 1. Fork and clone
git clone https://github.com/YOUR_USERNAME/naukrox.git
cd naukrox

# 2. Create virtual environment (optional but recommended for IDE support)
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set up environment
cp .env.example .env
# Add your OPENAI_API_KEY to .env

# 5. Run with Docker
docker-compose up --build
```

### Verify it works

Visit `http://localhost:5000` — you should see the Naukrox dashboard.

---

## Branching Strategy

| Branch | Purpose |
|--------|---------|
| `main` | Stable, production-ready code |
| `develop` | Integration branch for new features |
| `feature/your-feature` | Your new feature |
| `fix/bug-description` | Bug fixes |
| `docs/what-you-changed` | Documentation only |

Always branch off from `develop`, not `main`.

```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name
```

---

## Commit Message Format

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): short description

Examples:
feat(agents): add Indeed job scraper
fix(fetcher): handle LinkedIn rate limiting
docs(readme): update quick start guide
refactor(database): extract query helpers
test(analyzer): add JD parser unit tests
chore(docker): upgrade mongo to 7.1
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `style`

---

## Pull Request Process

1. **Branch** off `develop`
2. **Write clean code** — follow the style guide below
3. **Test your changes** locally with `docker-compose up --build`
4. **Update docs** if you added new features or changed behaviour
5. **Open PR** against `develop` with a clear title and description
6. **Fill in the PR template** completely
7. **Wait for review** — a maintainer will review within 48 hours

### PR Checklist

- [ ] My code follows the project style guide
- [ ] I have tested my changes locally
- [ ] I have updated documentation if needed
- [ ] I have added comments where the code is non-obvious
- [ ] My PR title follows Conventional Commits format

---

## Style Guide

### Python

- Follow **PEP 8**
- Use **type hints** where possible
- Keep functions **small and focused** (one responsibility)
- Add **docstrings** to all classes and public methods
- Use **f-strings** over `.format()` or `%`

```python
# Good
def build_query(user_input: dict) -> str:
    """Generate a Boolean search query from user input."""
    role = user_input.get("role", "")
    skills = user_input.get("skills", "")
    return f'"{role}" AND ({skills})'

# Avoid
def build_query(user_input):
    return '"' + user_input['role'] + '" AND (' + user_input['skills'] + ')'
```

### HTML / Jinja2

- Use semantic HTML5 tags
- Keep templates clean — logic belongs in Python, not templates
- CSS goes in `<style>` blocks within templates or a shared stylesheet

### Naming Conventions

| What | Convention | Example |
|------|-----------|---------|
| Files | `snake_case` | `job_fetcher.py` |
| Classes | `PascalCase` | `JobFetcherAgent` |
| Functions | `snake_case` | `fetch_jobs()` |
| Constants | `UPPER_SNAKE` | `MAX_JOBS = 10` |
| MongoDB collections | `snake_case` | `jobs`, `tracker` |

---

## Adding a New Job Source

One of the most valuable contributions is adding scrapers for new job platforms. Here's the pattern:

```python
# app/agents/job_fetcher.py

def fetch_from_indeed(self, query: str) -> list:
    """Scrape jobs from Indeed."""
    driver = get_driver()
    try:
        driver.get(f"https://indeed.com/jobs?q={query}")
        # ... scraping logic
        return jobs
    finally:
        driver.quit()
```

Then register it in `orchestrator.py` and open a PR — it will be merged fast!

---

## Questions?

Open a [GitHub Discussion](https://github.com/yourusername/naukrox/discussions) or tag `@maintainer` in your issue.

**Happy coding! 🎉**
