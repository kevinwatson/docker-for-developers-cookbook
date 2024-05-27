### Chapter 4 - Databases

## Introduction

If containers are ephemeral, why would anyone run a database (a persistent data store) in a container? There are multiple answers to this question. Perhaps you need the data to persist (use a volume), or you just need to test out a feature and you don't need to persist the data. In this chapter we'll provide examples for both.

## MySQL

## PostgreSQL

### Ephemeral (non-persistent) Data

```bash
mkdir -p ~/projects/postgres
cd ~/projects/postgres
touch docker-compose.yml
```

```yaml
# docker-compose.yml
# usage: docker-compose up

version: "3"
services:
  db:
    environment:
      POSTGRES_PASSWORD: secret
    image: "postgres:16.1"
    container_name: "pg"
    ports:
      - "5432:5432"
```

### Persistent (non-ephemeral) Data

```bash
mkdir -p ~/projects/postgres/data
cd ~/projects/postgres
touch docker-compose.yml
```

```yaml
# docker-compose.yml
# usage: docker-compose up

version: "3"
services:
  db:
    environment:
      POSTGRES_PASSWORD: secret
    image: "postgres:16.1"
    container_name: "pg"
    ports:
      - "5432:5432"
    volumes:
      - ./data:/var/lib/postgresql/data
```

## Resources

* https://www.postgresql.org
* https://hub.docker.com/_/postgres

[Next >>](050-chapter-05.md)
