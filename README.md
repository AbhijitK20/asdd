# ASDD Practicals — Experiments 1 to 8

Practical file and revision guide for **Advanced Software Development and DevOps (ASDD)**.

## Contents

| File | What it is |
|---|---|
| `ASDD_Experiments_1_to_8.docx` / `.pdf` | Full lab file: Experiment 1–8 with aims, procedure, commands and output |
| `ASDD_Practical_Revision_Guide.docx` / `.pdf` | Revision guide: what to do, what to verify, viva Q&A, commands, 90-minute plan |
| `pics/` | Experiment 8 screenshots (6), plus the two handwritten lab-manual pages |

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

# Jenkins
java -jar jenkins.war --httpPort=8080

# Kubernetes
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --type=NodePort --port=80
kubectl scale deployment nginx --replicas=3

# Docker
docker compose watch
docker build -t welcome .
docker run -d -p 3000:3000 welcome
```
