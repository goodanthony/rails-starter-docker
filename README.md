## Rails get started with Docker and Postgres

This is a blank project to get started with Rails, Docker and Postgres. Once you get the Rails app going please change the Dockerfile and docker-compose.yml to suit your needs.

## To build

```bash
docker compose build
docker compose up
```

Then go to docker desktop
Find the container and open a shell and type

# create a new rails app with postgres

```bash
rails new . --force --database=postgresql
```
