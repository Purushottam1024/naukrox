<div align="center">

# 🚀 Naukrox

### Agentic AI Job Automation — Find. Analyze. Apply. Automatically.

<br/>

[![Python](https://img.shields.io/badge/Python-3.11+-blue?style=for-the-badge&logo=python)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-3.0-black?style=for-the-badge&logo=flask)](https://flask.palletsprojects.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-7.0-green?style=for-the-badge&logo=mongodb)](https://mongodb.com)
[![Docker](https://img.shields.io/badge/Docker-Compose-blue?style=for-the-badge&logo=docker)](https://docker.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-orange?style=for-the-badge&logo=openai)](https://openai.com)
[![License](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)](CONTRIBUTING.md)
[![Stars](https://img.shields.io/github/stars/Purushottam1024/naukrox?style=for-the-badge)](https://github.com/Purushottam1024/naukrox/stargazers)

<br/>

**Naukrox** is a fully open-source Agentic AI system that automates your entire job search pipeline —
from discovering jobs to tailoring your resume and tracking applications — powered by GPT-4o, Selenium, Flask, and MongoDB.

[Features](#-features) · [Demo](#-demo) · [Quick Start](#-quick-start) · [Architecture](#-architecture) · [Contributing](#-contributing) · [Roadmap](#-roadmap)

</div>

---

## 🎯 What is Naukrox?

Most job seekers spend **5–10 hours per week** manually searching, copy-pasting, and rewriting resumes for each job. Naukrox eliminates all of that using a multi-agent AI pipeline:

```
You type your role + skills
        ↓
🤖 Query Builder    → Generates a Boolean search query with GPT-4o
🌐 Job Fetcher      → Scrapes live jobs via Selenium (LinkedIn, etc.)
🧠 JD Analyzer      → Extracts skills, keywords & responsibilities
📄 Resume Tailor    → Rewrites your resume to match each job (ATS-optimised)
✉️  Cover Letter     → Auto-generates a personalised cover letter
📊 Tracker          → Logs all applications in MongoDB
```

All of this happens in **one click**.

---

## ✨ Features

- 🔍 **Smart Boolean Query Builder** — GPT-4o generates the best search query from your input
- 🌐 **Live Job Scraper** — Selenium fetches real jobs from LinkedIn (with mock fallback)
- 🧠 **Deep JD Analysis** — Extracts required skills, ATS keywords, experience level, job type
- 📄 **ATS-Optimised Resume Tailoring** — GPT-4o rewrites your resume per job description
- ✉️ **Auto Cover Letter** — Personalised cover letter generated per application
- 📊 **Application Tracker** — Full MongoDB-backed tracker with status management
- 🐳 **One-command Docker setup** — Three containers, zero manual config
- 🌙 **Dark UI** — Clean, modern Flask + Jinja2 interface

---

## 🖥️ Demo

> Screenshots / GIF coming soon — contributors welcome to add one!

| Dashboard | Jobs View | Job Detail |
|-----------|-----------|------------|
| Search form + stats | All analyzed jobs | Resume + Cover Letter |

---

## ⚡ Quick Start

### Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running
- An [OpenAI API Key](https://platform.openai.com/api-keys)

### 1. Clone the repo

```bash
git clone https://github.com/Purushottam1024/naukrox.git
cd naukrox
```

### 2. Add your API key

```bash
cp .env.example .env
# Open .env and add your OPENAI_API_KEY
```

### 3. Run

```bash
docker-compose up --build
```

### 4. Open

```
http://localhost:5000
```

That's it. 🎉

---

## 🏗️ Architecture

```
naukrox/
├── docker-compose.yml          # Orchestrates 3 containers
├── Dockerfile                  # Flask app container
├── requirements.txt
├── run.py                      # Entry point
└── app/
    ├── __init__.py             # Flask app factory
    ├── routes.py               # All routes
    ├── agents/
    │   ├── orchestrator.py     # Coordinates the pipeline
    │   ├── query_builder.py    # GPT-4o Boolean query generation
    │   ├── job_fetcher.py      # Selenium scraper
    │   ├── jd_analyzer.py      # GPT-4o JD parser
    │   ├── resume_tailor.py    # GPT-4o resume customiser
    │   └── apply_assistant.py  # Cover letter generator
    ├── models/
    │   └── database.py         # All MongoDB operations
    ├── utils/
    │   ├── openai_client.py    # OpenAI wrapper
    │   └── selenium_driver.py  # Remote Chrome driver
    └── templates/              # Jinja2 HTML templates
```

### Docker Services

| Service | Image | Port |
|---------|-------|------|
| `web` | Python 3.11 + Flask | 5000 |
| `mongo` | mongo:7 | 27017 |
| `selenium` | selenium/standalone-chrome | 4444 |

### MongoDB Collections

| Collection | Purpose |
|------------|---------|
| `jobs` | Fetched + analyzed jobs |
| `resumes` | Tailored resumes per job |
| `tracker` | Application history |

---

## ⚙️ Configuration

All config lives in `.env`:

```env
OPENAI_API_KEY=sk-...          # Required — your OpenAI key
MONGO_URI=mongodb://mongo:27017/  # Auto-configured for Docker
FLASK_SECRET_KEY=your-secret   # Change in production
```

---

## 📌 Project Status

- **Current release:** `v1.0.0` (initial open-source release)
- **Stage:** Active early development
- **Primary focus:** Stabilising the core job automation pipeline and expanding job source coverage
- **CI:** GitHub Actions validates the repository with linting and Docker build checks

For release history, see [CHANGELOG.md](CHANGELOG.md).

---

## 📚 Project Documentation

The repository already includes the main operational and community documents:

- [README.md](README.md) — product overview and setup
- [CONTRIBUTING.md](CONTRIBUTING.md) — local setup, branch strategy, PR process
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) — community participation standards
- [SECURITY.md](SECURITY.md) — vulnerability reporting and deployment guidance
- [CHANGELOG.md](CHANGELOG.md) — release notes and planned work

If you are contributing code, start with `CONTRIBUTING.md` before opening a pull request.

---

## 🧪 Development Workflow

Naukrox follows a lightweight open-source workflow intended to keep contributions predictable:

1. Branch from `develop`
2. Follow Conventional Commits
3. Test changes locally with Docker
4. Update docs when behaviour changes
5. Open a PR against `develop`

Recommended branch naming:

- `feature/your-feature-name`
- `fix/bug-description`
- `docs/topic-name`

Example commit messages:

```text
feat(agents): add Indeed job scraper
fix(fetcher): handle LinkedIn rate limiting
docs(readme): expand setup and project docs
```

Full contribution details live in [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 🔐 Security

If you discover a security issue, **do not open a public issue**. Report it privately through a GitHub Security Advisory instead.

Deployment basics:

- Never commit `.env`
- Use a strong production `FLASK_SECRET_KEY`
- Do not expose MongoDB publicly
- Put the app behind HTTPS in production

See [SECURITY.md](SECURITY.md) for the full policy.

---

## 🛣️ Roadmap

We are actively looking for contributors to help build these features:

- [ ] **Multi-platform scraping** — Indeed, Naukri.com, Glassdoor, Internshala
- [ ] **Email notifications** — Alert when new matching jobs found
- [ ] **Resume PDF upload** — Parse uploaded PDF as base resume
- [ ] **User authentication** — Multi-user support with login
- [ ] **Scheduled auto-search** — Cron-based daily pipeline runs
- [ ] **Interview prep agent** — GPT-4o generates likely interview questions per JD
- [ ] **Salary estimator** — Predict salary range from JD using AI
- [ ] **Chrome extension** — One-click apply on any job board
- [ ] **REST API** — Expose pipeline as an API for third-party integrations
- [ ] **Mobile app** — React Native frontend

See [open issues](https://github.com/Purushottam1024/naukrox/issues) for the full list.

---

## 🤝 Contributing

Naukrox is **open to all contributors** — developers, designers, testers, and writers.

### How to contribute

```bash
# 1. Fork the repo
# 2. Create your branch
git checkout -b feature/your-feature-name

# 3. Make changes and commit
git commit -m "feat: add your feature"

# 4. Push and open a Pull Request
git push origin feature/your-feature-name
```

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for full guidelines.

### Good first issues

Look for issues labelled [`good first issue`](https://github.com/Purushottam1024/naukrox/issues?q=label%3A%22good+first+issue%22) — these are beginner-friendly and well-scoped.

---

## 🧱 Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python 3.11, Flask 3.0 |
| AI | OpenAI GPT-4o |
| Scraping | Selenium 4, Chrome |
| Database | MongoDB 7 |
| Frontend | Jinja2, HTML/CSS/JS |
| Containerisation | Docker, Docker Compose |

---

## 📄 License

Naukrox is released under the **MIT License** — free to use, modify, and distribute.
See [LICENSE](LICENSE) for full text.

---

## 🌟 Show your support

If Naukrox helped you, please **⭐ star the repo** — it helps others find the project.

[![Star History Chart](https://api.star-history.com/svg?repos=Purushottam1024/naukrox&type=Date)](https://star-history.com/#Purushottam1024/naukrox&Date)

---

## 👨‍💻 Author

Built with ❤️ by the open-source community.

Want to be listed as a contributor? Open a PR!

</div>
