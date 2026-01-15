# Security Policy

## Supported Versions

- Security fixes target the latest Docker configuration on `master`.
- Custom images or diverging compose stacks are out of scope unless the issue reproduces with the documented versions below.

## Ecosystem & Compatibility

| Component              | Version(s) / Tooling      | Notes |
| ---------------------- | ------------------------- | ----- |
| OS baseline            | WSL (Ubuntu 24.04.3 LTS)  | Authoring environment referenced in the README. |
| Container runtime      | Docker 29.1.3             | Required for building the image. |
| Database image         | `mysql/mysql-server:8.0.32` | Pulled via `docker-compose.yml`; includes sample schema from `setup.sql`. |
| Client tooling         | `docker-compose`, MySQL CLI | Use `docker-compose exec db mysql -u root` for local testing. |

## Backward Compatibility

- Compose files target the MySQL 8.0.x series. We maintain backward compatibility for patch-level upgrades (8.0.x → 8.0.y). Older major versions (5.7, 5.6) are unsupported.
- Custom schema tweaks are outside the scope of this repo; if you diverge from `setup.sql`, rebase onto the latest version before requesting fixes.

## Reporting a Vulnerability

If you believe you’ve found a security issue in the Docker setup or SQL assets:

1. Open a private GitHub Security Advisory (preferred) via **Security → Report a vulnerability** and include compose logs, schemas, and repro steps.
2. Or email `security@project.org` with details about the container build, configuration, and query samples.

Expect acknowledgement within **3 business days** and progress updates at least every **7 business days** while we investigate.
