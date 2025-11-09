# Rails + Docker + Postgres Starter (2025‑11)

This starter uses **Ruby 3.4 (Debian bookworm slim)**, **Rails 8.1**, **Node 24 LTS (Corepack)**, and **PostgreSQL 18**.

> TL;DR  
> ```bash
> docker compose build
> docker compose up -d db
> docker compose run --rm app rails new . --force --database=postgresql
> docker compose up
> ```
> Then visit http://localhost:3000

---

or ie:
docker compose run --rm app rails new . --force --database=postgresql --css=tailwind --javascript=importmap


## 1) Build and boot

```bash
# Build images
docker compose build

# Start Postgres first
docker compose up -d db


Good commands
docker compose run --rm app bin/rails db:migrate
docker compose run --rm app bin/rails g scaffold Post title:string

# Console & tests
docker compose run --rm app bin/rails console
docker compose run --rm app bin/rspec 