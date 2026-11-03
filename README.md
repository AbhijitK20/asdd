# ASDD Practicals — Experiments 1 to 8

Step-by-step practical guides, full lab file and revision guide for
**Advanced Software Development and DevOps (ASDD)**.

## Start here

| # | Practical | Guide |
|---|---|---|
| 0 | Before you go — accounts, tokens, PC checks | [practicals/00-before-you-go.md](practicals/00-before-you-go.md) |
| 1 | Agile lifecycle using Jira | [practicals/01-jira-agile.md](practicals/01-jira-agile.md) |
| 2 | Version control with Git & GitHub | [practicals/02-git-version-control.md](practicals/02-git-version-control.md) |
| 3 | Install Jenkins + Hello World build | [practicals/03-install-jenkins.md](practicals/03-install-jenkins.md) |
| 4 | Jenkins + GitHub CI/CD pipeline | [practicals/04-jenkins-github-cicd.md](practicals/04-jenkins-github-cicd.md) |
| 5 | Kubernetes — deploy, expose, scale | [practicals/05-kubernetes.md](practicals/05-kubernetes.md) |
| 6 | Docker — develop with containers | [practicals/06-docker.md](practicals/06-docker.md) |
| 7 | Monitoring with Grafana | [practicals/07-grafana.md](practicals/07-grafana.md) |
| 8 | Serverless with AWS Lambda | [practicals/08-aws-lambda.md](practicals/08-aws-lambda.md) |

Each guide follows the same shape:

```
Aim → Prerequisites → Steps (commands + clicks) → What to verify/screenshot
    → Troubleshooting → Viva questions → Result
```

## Repository layout

```
asdd/
├── practicals/            Step-by-step guides (00 checklist + 8 practicals)
├── lab-file/              Full lab file (DOCX + PDF)
├── revision-guide/        Revision guide with viva Q&A (DOCX + PDF)
└── screenshots/
    ├── exp8/              AWS Lambda screenshots (6)
    └── lab-manual/        Handwritten lab-manual pages (2)
```

## Contents

| Folder | File | What it is |
|---|---|---|
| `practicals/` | `00`–`08` | Printable step-by-step procedure, verification points, fixes and viva Q&A |
| `lab-file/` | `ASDD_Experiments_1_to_8.docx` / `.pdf` | Experiment 1–8 with aims, procedure, commands and output |
| `revision-guide/` | `ASDD_Practical_Revision_Guide.docx` / `.pdf` | What to do, what to verify, viva Q&A, commands, 90-minute plan |
| `screenshots/exp8/` | `01`–`06` | Lambda home, getting started, EventBridge trigger, monitor metrics, function overview, code source |
| `screenshots/lab-manual/` | `page-1`, `page-2` | Handwritten lab-manual pages |

## Experiments

1. Agile software project lifecycle using Jira with DevOps pipeline integration
2. Version control operations using Git and collaboration workflows
3. Installation of Jenkins and sample "Hello World" build
4. Integrate Jenkins with GitHub and simulate a CI/CD pipeline
5. Kubernetes — deploy, expose and scale an application
6. Docker — develop with containers
7. Monitoring using Grafana
8. Serverless function using AWS Lambda

## Quick commands

```bash
# Git
git init && git add . && git commit -m "msg"
git branch -M main
git remote add origin <url>
git push -u origin main

# Jenkins — WAR
java -jar jenkins.war --httpPort=8080

# Jenkins — Docker (no install)
docker run -d --name jenkins --restart unless-stopped \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk21

# Kubernetes
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --type=NodePort --port=80
kubectl scale deployment nginx --replicas=3

# Docker
docker compose watch
docker build -t welcome .
docker run -d -p 3000:3000 welcome
```

## Notes

- **Ports:** Jenkins `8080`, Grafana `3000`, app `3000` (use `3001` if busy).
- **Jenkins is local:** the admin account lives on the machine where Jenkins
  runs. GitHub/Jira accounts are portable; Jenkins is not.
- **Keep me signed in:** tick it on the Jenkins `/login` page and on the
  Atlassian login page so a lab session survives restarts.
