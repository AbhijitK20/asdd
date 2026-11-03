# Practical 2 — Version Control with Git and GitHub

**Aim:** To perform version control operations using Git and apply collaboration
workflows for software development.

**Prerequisite:** Git installed + a GitHub account.

---

## Part A — Configure Git

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```

> Use the email tied to your GitHub account so commits are attributed to you.

## Part B — Create a local repository

```bash
mkdir GitProject
cd GitProject
git init
git status
```

Create the first file and commit it:

```bash
echo "# GitProject" > README.md
git add README.md
git commit -m "Initial Commit"
```

> On Windows PowerShell, `echo "# GitProject" > README.md` works; in CMD use
> `echo # GitProject> README.md`.

## Part C — Push to GitHub

1. GitHub → **New repository** → name `GitProject` → **Public** → do **not**
   add a README → **Create**.
2. Copy the repository URL, then:

```bash
git branch -M main
git remote add origin https://github.com/<username>/GitProject.git
git push -u origin main
```

If Git asks for a password, paste a **Personal Access Token** (classic, `repo`
scope) — not your GitHub password.

## Part D — Collaboration workflow (branch → PR → merge)

```bash
git checkout -b feature-branch
# create or edit a file, e.g. feature.txt
git add .
git commit -m "Add feature"
git push origin feature-branch
```

Then on GitHub:

1. Open the repository → **Compare & pull request**.
2. Add a title and description → **Create pull request**.
3. **Review** the changes → **Merge pull request** → **Confirm merge**.
4. Locally, update main:

```bash
git checkout main
git pull origin main
```

## What to verify / screenshot

- [ ] `git status` before and after committing
- [ ] `git log --oneline` showing the commits
- [ ] GitHub repo with `README.md` and two branches
- [ ] The merged pull request
- [ ] `git remote -v` showing `origin`

## Troubleshooting

| Problem | Fix |
|---|---|
| `Author identity unknown` | Set `user.name` and `user.email` (Part A) |
| `remote origin already exists` | `git remote set-url origin <url>` |
| `Authentication failed` | Use a Personal Access Token, not the password |
| `Updates were rejected` | `git pull --rebase origin main` then push again |
| Wrong branch name | `git branch -M main` renames the current branch |
| `src refspec main does not match any` | Make a commit first, then push |

## Viva

- **Git vs GitHub?** Git is the local version-control tool; GitHub is the remote hosting/collaboration service.
- **Commit vs push?** Commit saves a snapshot locally; push uploads commits to the remote.
- **What is a branch?** An independent line of development that can later be merged.
- **Pull vs fetch?** Fetch downloads changes; pull fetches and merges them.
- **What is a merge conflict?** Two branches changed the same lines; Git cannot merge automatically and asks you to resolve.

**Result:** Version control operations were performed and the collaboration
workflow (branch → pull request → review → merge) was applied successfully.
