# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| latest (main) | ✅ |
| older branches | ❌ |

## Reporting a Vulnerability

If you discover a security vulnerability in Naukrox, please **do not** open a public GitHub issue.

Instead, please report it privately by:

1. Opening a [GitHub Security Advisory](https://github.com/yourusername/naukrox/security/advisories/new)
2. Or emailing the maintainer directly (add your email here)

Please include:
- A description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

We will acknowledge receipt within **48 hours** and aim to release a patch within **7 days** for critical issues.

## Security Best Practices for Deployment

- Never commit your `.env` file — it contains your API keys
- Use a strong, random `FLASK_SECRET_KEY` in production
- Keep Docker images updated regularly
- Do not expose MongoDB port 27017 publicly
- Use HTTPS in production (via a reverse proxy like Nginx)
