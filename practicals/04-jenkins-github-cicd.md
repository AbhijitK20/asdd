# Practical 4 — Integrate Jenkins with GitHub (CI/CD Pipeline)

**Aim:** To integrate Jenkins with GitHub and simulate a CI/CD pipeline for
automated building and testing of a software project.

**Prerequisite:** Practical 3 done (Jenkins running at http://localhost:8080)
and a GitHub login. JDK for compiling Java is optional — a shell-only pipeline
also satisfies the aim.

---

## Part A — Put a small project on GitHub

1. GitHub → **New repository** → name `jenkins-demo` → **Public** → do **not**
   add a README → **Create**.
2. Locally:

```bash
mkdir jenkins-demo
cd jenkins-demo
```

3. Create `Hello.java`:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello from Jenkins CI/CD");
    }
}
```

4. Create `Jenkinsfile` (pipeline as code):

```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { echo 'Code checked out from GitHub' }
        }
        stage('Build') {
            steps { echo 'Building...' }
        }
        stage('Test') {
            steps { echo 'Running tests...' }
        }
        stage('Deploy') {
            steps { echo 'Simulated deployment...' }
        }
    }
}
```

5. Create `.gitignore` and push:

```bash
echo "*.class" > .gitignore
git init
git add .
git commit -m "Add Hello.java and Jenkinsfile"
git branch -M main
git remote add origin https://github.com/<username>/jenkins-demo.git
git push -u origin main
```

## Part B — Give Jenkins access to GitHub

1. GitHub → **Settings** → **Developer settings** → **Personal access tokens**
   → **Tokens (classic)** → **Generate new token** → tick `repo` → generate.
2. Copy the token (it is shown once).
3. Jenkins → **Manage Jenkins** → **Credentials** → **System** → **Global
   credentials** → **Add Credentials**:
   - Kind: **Username with password**
   - Username: your GitHub username
   - Password: the token
   - ID: `github-token` → **Create**.

## Part C — Create the pipeline job

1. Jenkins → **New Item** → name `CI-CD-Pipeline` → **Pipeline** → **OK**.
2. **Pipeline** section:
   - Definition: **Pipeline script from SCM**
   - SCM: **Git**
   - Repository URL: `https://github.com/<username>/jenkins-demo.git`
   - Credentials: `github-token`
   - Branch Specifier: `*/main` (not `*/master`)
   - Script Path: `Jenkinsfile`
3. **Build Triggers** → tick **Poll SCM** → Schedule: `H/2 * * * *`
   (every ~2 minutes; the orange warning is fine).
4. **Save** → **Build Now**.
5. Open build **#1** → **Console Output** → all four stages run and the build
   ends with `Finished: SUCCESS`.
6. Open the **Stage View** / **Blue Ocean** to show the stage graph.

## Part D — Prove the automation

1. Edit a file locally and push:

```bash
# change a message or add a comment
git add .
git commit -m "Update pipeline demo"
git push
```

2. Wait for the poll interval (≤2 minutes).
3. A new build starts **by itself** — the console says `Started by an SCM
   change`.
4. Open the build → **Changes** → your commit is listed. Screenshot.
5. Optional: in a real network, replace polling with a GitHub webhook
   (`http://<jenkins-host>/github-webhook/`). A laptop needs a tunnel such as
   ngrok for GitHub to reach it.

## What to verify / screenshot

- [ ] GitHub repository with `Hello.java` + `Jenkinsfile`
- [ ] Jenkins credentials page (token hidden)
- [ ] Pipeline job configuration
- [ ] First successful build + stage view
- [ ] Auto-triggered second build with `Started by an SCM change`
- [ ] Console output / Changes tab

## Troubleshooting

| Problem | Fix |
|---|---|
| `Couldn't find any revision to build` | Branch specifier must be `*/main` |
| Authentication failed | Re-check the PAT and the credential ID |
| `javac: not found` | Use the echo-based pipeline, or install a JDK inside the container |
| Build does not trigger | Poll SCM syntax must be `H/2 * * * *` (5 fields); wait 2 minutes |
| Webhook not firing | Jenkins must be publicly reachable — use ngrok or keep polling |
| Pipeline syntax error | Groovy braces must match; keep the sample file unchanged first |

## Viva

- **CI vs CD?** CI = automatically build and test every change; CD = automatically deliver/deploy it.
- **What is a Jenkinsfile?** A text file in the repo that defines the pipeline as code.
- **Webhook vs polling?** Webhook = GitHub notifies Jenkins immediately; polling = Jenkins checks on a schedule.
- **Why a personal access token?** So Jenkins can authenticate to GitHub without the account password.
- **What does `Started by an SCM change` prove?** The pipeline ran automatically from a Git change, not a manual click.

**Result:** Jenkins was integrated with GitHub and every push automatically
built and tested the project — the CI/CD pipeline was simulated successfully.
