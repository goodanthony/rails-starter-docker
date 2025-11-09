# Rails + Docker + Postgres Starter (2025‑11)

This starter uses **Ruby 3.4 (Debian bookworm slim)**, **Rails 8.1**, **Node 24 LTS (Corepack)**, and **PostgreSQL 18**.

## Quick Start
```bash
# Build images
docker compose build

# Start Postgres first
docker compose up -d db

# Generate your Rails app (choose one option below)
docker compose run --rm app rails new . --force --database=postgresql

# Start the app
docker compose up
```

Then visit http://localhost:3000

---

## Rails App Generation Options

Choose the setup that fits your needs:
```bash
# Minimal setup (API mode)
docker compose run --rm app rails new . --force --database=postgresql

# With Tailwind CSS
docker compose run --rm app rails new . --force --database=postgresql --css=tailwind

# With importmap (no build step)
docker compose run --rm app rails new . --force --database=postgresql --javascript=importmap

# Full-stack with Tailwind + importmap
docker compose run --rm app rails new . --force --database=postgresql --css=tailwind --javascript=importmap

# With esbuild (modern JS bundling)
docker compose run --rm app rails new . --force --database=postgresql --javascript=esbuild
```

---

## Common Commands

### Database Operations
```bash
# Create databases
docker compose run --rm app bin/rails db:create

# Run migrations
docker compose run --rm app bin/rails db:migrate

# Rollback last migration
docker compose run --rm app bin/rails db:rollback

# Load schema
docker compose run --rm app bin/rails db:schema:load

# Seed database
docker compose run --rm app bin/rails db:seed

# Reset database (drop, create, migrate, seed)
docker compose run --rm app bin/rails db:reset
```

### Generators
```bash
# Generate a scaffold
docker compose run --rm app bin/rails g scaffold Post title:string body:text published:boolean

# Generate a model
docker compose run --rm app bin/rails g model User email:string name:string

# Generate a controller
docker compose run --rm app bin/rails g controller Pages home about contact

# Generate a migration
docker compose run --rm app bin/rails g migration AddSlugToPosts slug:string:index
```

### Development Tools
```bash
# Rails console
docker compose run --rm app bin/rails console

# Run tests
docker compose run --rm app bin/rails test

# Run RSpec (if installed)
docker compose run --rm app bin/rspec

# Rails routes
docker compose run --rm app bin/rails routes

# Rails stats
docker compose run --rm app bin/rails stats
```

### Credentials & Secrets
```bash
# Edit credentials (uses $EDITOR, default: vi)
docker compose run --rm app bin/rails credentials:edit

# Show credentials
docker compose run --rm app bin/rails credentials:show
```

### Bundle & Dependencies
```bash
# Install gems
docker compose run --rm app bundle install

# Update a specific gem
docker compose run --rm app bundle update rails

# Add a gem (edit Gemfile first, then:)
docker compose run --rm app bundle install

# Install JS dependencies (if using npm/yarn)
docker compose run --rm app yarn install
```

### Container Management
```bash
# View logs
docker compose logs -f app

# Restart services