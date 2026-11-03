# Docker setup files

Reproducible containers for Practicals 3, 4 and 7. No Dockerfile is needed for
Jenkins or Grafana — both run from official images. (Practical 6's sample app
already includes its own `Dockerfile` inside
[`docker/getting-started-todo-app`](https://github.com/docker/getting-started-todo-app).)

## Start Jenkins (Practical 3 / 4)

```bash
cd docker
docker compose up -d jenkins
```

Get the initial admin password:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Open http://localhost:8080 and finish the wizard (install suggested plugins →
create admin user). The `jenkins_home` volume keeps jobs, plugins and users
across restarts.

## Start Grafana (Practical 7)

```bash
cd docker
docker compose up -d grafana
```

Open http://localhost:3000 — login `admin` / `admin`, then change the password.

## Both at once

```bash
docker compose up -d
docker compose ps
```

## Stop / clean up

```bash
docker compose stop          # stop containers, keep data
docker compose down          # remove containers, keep volumes
docker compose down -v       # remove containers AND data (fresh start)
```

> `down -v` deletes the Jenkins admin user and all jobs — only use it when you
> want a clean Jenkins for a new demo.

## Ports

| Service | URL |
|---|---|
| Jenkins | http://localhost:8080 |
| Grafana | http://localhost:3000 |

If a port is busy, change the left side of the mapping, e.g.
`"8081:8080"` for Jenkins or `"3001:3000"` for Grafana.
