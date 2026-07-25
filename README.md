# Latest Rails + Docker + PostgreSQL Starter

Generate a new Rails application without installing Ruby, Rails, Node.js, or
PostgreSQL on the host.

The starter currently pins:

| Tool | Version |
| --- | --- |
| Ruby | 4.0.6 |
| Rails | 8.1.3 |
| Bundler | 4.0.17 |
| Node.js | 24 LTS |
| PostgreSQL | 18.4 |

The Ruby, Rails, Bundler, and PostgreSQL patch releases are exact so a rebuild is
repeatable. Node.js follows the supported Node 24 LTS patch line.

## Prerequisites

- Docker Desktop, or Docker Engine with Docker Compose v2
- Git

No host Ruby or Node.js installation is required.

## Quick start

From the repository root:

```bash
# Build the development image.
docker compose build

# Start PostgreSQL and wait for its health check.
docker compose up -d db

# Generate the default full-stack Rails app in this directory.
# --skip-docker keeps this starter's development Docker setup.
docker compose run --rm app \
  rails new . --force --skip-docker --database=postgresql

# Prepare the development and test databases.
docker compose run --rm app bin/rails db:prepare

# Start Rails and PostgreSQL.
docker compose up
```

Open <http://localhost:3000>.

`rails new` replaces this README with the generated application README.
Ongoing Docker commands remain available in [DOCKER.md](DOCKER.md).

## Choose an application type

Run one of these commands instead of the default `rails new` command above.

### Default Rails stack

Hotwire, importmap, Propshaft, and the current Rails defaults:

```bash
docker compose run --rm app \
  rails new . --force --skip-docker --database=postgresql
```

### API-only Rails app

```bash
docker compose run --rm app \
  rails new . --force --skip-docker --database=postgresql --api
```

### Tailwind CSS

```bash
docker compose run --rm app \
  rails new . --force --skip-docker --database=postgresql --css=tailwind
```

### esbuild

```bash
docker compose run --rm app \
  rails new . --force --skip-docker --database=postgresql --javascript=esbuild
```

### Tailwind CSS and esbuild

```bash
docker compose run --rm app \
  rails new . --force --skip-docker --database=postgresql \
  --css=tailwind --javascript=esbuild
```

See every option supported by this pinned Rails release:

```bash
docker compose run --rm app rails new --help
```

## Verify the toolchain

```bash
docker compose run --rm app bash -c \
  'ruby --version; rails --version; bundle --version; node --version; psql --version'
```

Expected major versions are Ruby 4.0, Rails 8.1, Bundler 4.0, Node 24, and
PostgreSQL client 18.

## How it works

- `Dockerfile.starter` provides the Rails generator and development toolchain.
- `docker-compose.yml` mounts the repository at `/work`.
- The `bundle` volume caches installed gems.
- The `pgdata` volume preserves PostgreSQL data.
- The container runs as an unprivileged `app` user.
- Full-stack apps start with `bin/dev`; API-only apps fall back to
  `bin/rails server`.

After generation, use [DOCKER.md](DOCKER.md) for common development, database,
test, and container commands.
