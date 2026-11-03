# Practical 3 — Install Jenkins and Trigger a Sample Build

**Aim:** To install Jenkins, launch it on an available port and trigger a sample
build for the built-in "Hello World" program.

**Prerequisite:** Java (JDK 17 or 21) installed. Check:

```bash
java -version
javac -version
```

> Jenkins runs on the JVM, so Java must come first. Jenkins 2.5xx supports
> Java 17 and 21.

---

## Option A — Docker (recommended, nothing to install)

Works on Linux, macOS and Windows with Docker Desktop.

Using the repository's compose file (recommended):

```bash
cd docker
docker compose up -d jenkins
```

Or run the container directly:

```bash
docker pull jenkins/jenkins:lts-jdk21
docker run -d --name jenkins --restart unless-stopped \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts-jdk21
```

Get the initial admin password:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

## Option B — WAR file (no admin rights needed)

```bash
# download from https://www.jenkins.io/download/ (LTS war)
java -jar jenkins.war --httpPort=8080
```

If port 8080 is busy, use `--httpPort=8081`.

The password is printed in the terminal and stored at:

```bash
cat ~/.jenkins/secrets/initialAdminPassword
```

## Option C — Windows installer

1. Download the LTS `.msi` from https://www.jenkins.io/download/.
2. Run it → Next → choose the port (8080) → Install.
3. Open `http://localhost:8080`; the password is at
   `C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword`.

## Unlock and finish setup (all options)

1. Open http://localhost:8080 → **Unlock Jenkins**.
2. Paste the initial admin password → **Continue**.
3. **Install suggested plugins** (includes Git, GitHub and Pipeline).
4. Wait for the plugins to install.
5. **Create First Admin User** — username, password, name, email → **Save and
   Continue**.
6. Instance URL: leave the default → **Save and Finish** → **Start using
   Jenkins**.

> Keep these admin credentials — they are your "Jenkins login" for Practical 4.
> The **Keep me signed in** checkbox appears on `http://localhost:8080/login`
> after you log out.

## Trigger the Hello World build

1. **New Item** → name `HelloWorld` → **Freestyle project** → **OK**.
2. **Build Steps** → **Add build step** → **Execute shell** (Linux/macOS) or
   **Execute Windows batch command** (Windows).
3. Command:

```bash
echo "Hello World from Jenkins"
```

4. **Save** → **Build Now**.
5. Click build **#1** → **Console Output** → verify the message and
   `Finished: SUCCESS`.

## What to verify / screenshot

- [ ] Jenkins dashboard after setup
- [ ] `HelloWorld` job page
- [ ] Build #1 success
- [ ] Console Output showing `Hello World from Jenkins`

## Troubleshooting

| Problem | Fix |
|---|---|
| `java: command not found` | Install JDK 17/21 and reopen the terminal |
| Port 8080 already in use | Start with `--httpPort=8081` (or `-p 8081:8080` for Docker) |
| Unlock password missing | Docker: `docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`; WAR: `~/.jenkins/secrets/initialAdminPassword` |
| `docker: permission denied` | Add your user to the docker group, or use `sudo docker ...` |
| Plugins fail to install | Check internet/proxy; retry from Manage Jenkins → Plugins |
| Forgot admin password | Manage Jenkins → Users → configure, or reset via `config.xml` (lab PC: reinstall is faster) |

## Viva

- **What is Jenkins?** An open-source automation server used to build, test and deploy software.
- **Why does Jenkins need Java?** Jenkins itself runs on the JVM.
- **What is a build job?** A configured task Jenkins executes (compile, test, run a script).
- **Where is the initial password?** `~/.jenkins/secrets/initialAdminPassword` (or printed in the terminal).
- **What are plugins?** Extensions that add SCM, pipeline, notification and deployment capabilities.

**Result:** Jenkins was installed, launched on a free port and a sample
"Hello World" build was triggered successfully.
