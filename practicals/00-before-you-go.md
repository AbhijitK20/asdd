# Before You Go — Practical Checklist

5-minute checklist to do **before** entering the lab. Each practical assumes
only free tools and a browser.

## Accounts to create at home

| Account | URL | Needed for |
|---|---|---|
| Atlassian / Jira | https://www.atlassian.com | Practical 1 |
| GitHub | https://github.com | Practicals 2, 4 |
| AWS (free tier) | https://aws.amazon.com/free | Practical 8 |
| Docker Hub (optional) | https://hub.docker.com | Practical 6 (Play with Docker) |

> AWS needs a card for verification. If your college gives AWS Academy /
> Learner Lab accounts, use those instead — do not add a card on a lab PC.

## Keep ready (phone notes or paper)

- [ ] GitHub username + password
- [ ] A GitHub **Personal Access Token** (Settings → Developer settings →
      Personal access tokens → Tokens (classic) → Generate, tick `repo`).
      Use the token as the password when Git asks.
- [ ] Jira workspace URL (e.g. `https://yourname.atlassian.net`)
- [ ] Jenkins admin username + password (created on the day, Practical 3)

## Check on the college PC

Open a terminal (Git Bash / PowerShell / Linux shell):

```bash
git --version        # Practical 2
java -version        # Practicals 3, 4 (need JDK 17 or 21)
javac -version       # must work (JDK, not just JRE)
docker --version     # Practicals 3, 6
minikube version     # Practical 5 (optional)
```

If something is missing:

- **Git** missing → ask lab staff to install Git, or use GitHub's web upload.
- **Java** missing → install JDK 17/21, or use the Docker route for Jenkins.
- **Docker** missing → use Play with Docker (Practical 6) and Killercoda
  (Practical 5).
- **Nothing installable** → Practicals 5 and 6 can be done entirely in the
  browser; Practical 1 is browser-only.

## On a shared / college PC

- Log in to GitHub, Jira and Jenkins **in the browser** and tick
  **Keep me signed in** where offered.
- Work inside a folder you can write to, e.g. `~/devops` or `D:\devops`.
- At the end: **log out** of GitHub / Jira / AWS and remove saved Git
  credentials (Windows: Credential Manager → Windows Credentials →
  remove `github.com`).
- Never save passwords or tokens in a file that stays on the lab PC.

## Ports used

| Tool | Port |
|---|---|
| Jenkins | 8080 (or 8081 if busy) |
| Grafana | 3000 |
| Docker app | 3000 (or 3001 if busy) |
| Kubernetes NodePort | 30000–32767 (random, read from `kubectl get svc`) |
