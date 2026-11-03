# Practical 1 — Agile Project Lifecycle using Jira

**Aim:** To study and implement the Agile software project lifecycle using Jira
with DevOps pipeline integration.

**Prerequisite:** Browser + a working Atlassian/Jira login.

---

## Part A — Create the project

1. Open https://www.atlassian.com → **Log in** (Google login works).
2. Go to https://start.atlassian.com → **Create project**.
3. Choose **Scrum** → **Use template** → **Team-managed**.
4. Name: `DevOpsLab` — Key: `DOL` → **Create**.

> Team-managed is simpler for a lab: no admin approval needed and the board is
> ready immediately.

## Part B — Create the Epic and Stories

1. Open the project → **Backlog**.
2. Click **Create** (top-right).
3. Change the issue type from **Task** to **Epic** (click the type chip).
4. Summary: `DevOps Pipeline Setup` → **Create**.
5. Click **Create** again → type **Story** → summary `Set up Jira board`.
6. While the dialog is open, click the **Sprint** chip and pick the sprint (or
   leave it in the backlog to drag later).
7. Tick **Create another** to keep the dialog open and add:
   - `Configure Git repository`
   - `Build CI/CD pipeline`
8. Close the dialog.

## Part C — Create and start the sprint

1. On **Backlog**, click **Create sprint** if no sprint exists.
2. Drag the three stories into the sprint section (or tick them → **Move to
   sprint**).
3. Click **Start sprint** → set:
   - Sprint name: `SCRUM Sprint 1`
   - Duration: `2 weeks`
   - Sprint goal: `Deliver a working CI/CD pipeline for the Partner Portal app`
4. **Start**.

## Part D — Move work across the board

1. Open **Board** (top nav). You should see the four columns:
   **To Do → In Progress → In Review → Done**.
2. **Drag** `Set up Jira board` to **Done**.
3. Drag `Build CI/CD pipeline` to **In Progress**.
4. Leave `Configure Git repository` in **To Do**.

> If a status pill does not open when clicked, drag the card — that always
> works with a real mouse.

## Part E — Show the other views

1. **Backlog** — shows the sprint goal, items and statuses. Screenshot.
2. **Timeline** — shows the Epic across the sprint dates. Screenshot.
3. **Board** — shows cards in different columns. Screenshot.

## Part F — Add a collaborator

1. Project settings → **Access** (or **People**) → **Add people**.
2. Enter a classmate's email → role **Member** → **Add**.
3. Open one story → **Assignee** → pick that person.
4. Screenshot the assignee on the card.

## Part G — DevOps pipeline integration (GitHub for Jira)

1. Top nav **Apps** → **Explore more apps** → search **GitHub for Jira** →
   **Get app**.
2. **Connect GitHub** → authorise → choose your repository
   (e.g. `jenkins-demo`).
3. In a local repo, commit using the issue key in the message:

```bash
git add .
git commit -m "DOL-1 set up the Jira board"
git push
```

4. Open the Jira issue → **Development** panel → the commit and branch appear.
   Screenshot.

## Part H — Complete the sprint and show the report

1. **Backlog** → on the sprint header click **Complete sprint**.
2. Jira reports *X completed / Y open work items*; choose where open items go
   (**Backlog** or **New sprint**) → **Complete sprint**.
3. Open **Reports → Sprint report** (or the link in the confirmation) and
   screenshot planned vs completed.

## What to verify / screenshot

- [ ] Backlog with the Epic, sprint goal and three stories
- [ ] Board with cards in at least two columns
- [ ] Timeline view
- [ ] Collaborator assigned to an issue
- [ ] Sprint report after completion

## Troubleshooting

| Problem | Fix |
|---|---|
| No **Create sprint** button | You are in a company-managed project; use **Backlog → ... → Create sprint**, or make a team-managed project |
| Story not in the sprint | Drag it into the sprint section, or tick it → **Move to sprint** |
| Status dropdown will not open | Drag the card between columns |
| Cannot complete sprint | The sprint must be started first |
| GitHub app not visible | Apps → Explore more apps; the free plan includes it |

## Viva

- **What is a sprint?** A fixed time box (1–4 weeks) in which a set of stories is completed.
- **Story vs Epic?** Story = small deliverable; Epic = large body of work split into stories.
- **Scrum vs Kanban?** Scrum = fixed sprints and roles; Kanban = continuous flow with WIP limits.
- **What is the backlog?** The prioritised list of all work not yet in a sprint.
- **What does the sprint report show?** Planned vs completed work and scope changes.

**Result:** The Agile lifecycle (Summary, Backlog, Board, Timeline, collaborators)
was implemented in Jira and integrated with GitHub.
