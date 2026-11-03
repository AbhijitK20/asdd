# Practical 6 — Docker: Develop with Containers

**Aim:** To develop and run an application using Docker containers.

**Prerequisite:** Docker installed, or a browser for Play with Docker.

---

## Option A — Local Docker

1. Verify Docker:

```bash
docker --version
docker ps
```

If `docker ps` fails, start Docker Desktop (Windows/macOS) or the Docker
service (Linux: `sudo systemctl start docker`).

2. Clone the sample project:

```bash
git clone https://github.com/docker/getting-started-todo-app
cd getting-started-todo-app
```

3. Start the development environment:

```bash
docker compose watch
```

The app starts and is reachable at http://localhost:3000. `watch` rebuilds and
syncs files as you edit them.

4. In a second terminal, build an image from the provided Dockerfile:

```bash
docker build -t welcome .
docker images
```

5. Run a container from the image:

```bash
docker run -d -p 3000:3000 --name welcome-app welcome
docker ps
```

6. Open http://localhost:3000 and use the app (add/complete a todo).
7. Stop and remove:

```bash
docker stop welcome-app
docker rm welcome-app
```

## Option B — Play with Docker (browser only)

1. Open https://labs.play-with-docker.com and log in with Docker Hub.
2. **Start** a new instance.
3. Run the same `git clone`, `cd` and `docker compose watch` commands in the
   browser terminal.
4. Click the exposed **3000** port link to open the app.

## What to verify / screenshot

- [ ] `docker --version`
- [ ] `docker compose watch` output showing containers started
- [ ] App open in the browser at localhost:3000
- [ ] `docker ps` showing the running container
- [ ] `docker images` showing the `welcome` image

## Troubleshooting

| Problem | Fix |
|---|---|
| `Cannot connect to the Docker daemon` | Start Docker Desktop / `sudo systemctl start docker` |
| Port 3000 already in use | Use `-p 3001:3000` and open http://localhost:3001 |
| `docker compose` not found | Old Docker: use `docker-compose up` |
| Build fails on `.` | Run `docker build` from the folder containing the Dockerfile |
| `git clone` fails | Download the repo as ZIP from GitHub and extract it |

## Viva

- **Image vs container?** An image is the packaged template; a container is a running instance of it.
- **What is a Dockerfile?** A recipe that defines how to build an image.
- **What is Docker Compose?** A tool to define and run multi-container applications from a YAML file.
- **What does `-p 3000:3000` do?** Maps host port 3000 to container port 3000.
- **Why containers?** Consistent environment, isolation, fast startup and reproducible builds.

**Result:** An application was cloned, started with Docker Compose, built into
an image and run as a container successfully.
