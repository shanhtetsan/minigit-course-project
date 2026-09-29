# Homework 2 — Part 2 Submission

Student name: Shan Htet San

GitHub username: shanhtetsan

## 1. Git Command Observations

| Command or workflow | What did you observe? | What was the user trying to accomplish? | What problem or risk did it address? |
| ------------------- | --------------------- | --------------------------------------- | ------------------------------------ |
| 1. `git status` | Git showed which files were modified, staged, or untracked. | The user was trying to understand the current state of the repository. | It reduced the risk of forgetting changed files or committing the wrong files. |
| 2. `git diff` | Git showed the changes made to tracked files that were not staged yet. | The user was trying to review changes before preparing them for a commit. | It reduced the risk of including unintended changes. |
| 3. `git add` and `git diff --staged` | `git add` staged selected changes, and `git diff --staged` showed the changes prepared for the next commit. | The user was trying to select and verify which changes would be included in the next commit. | It reduced the risk of committing unwanted changes or missing intended changes. |
| 4. `git commit` | Git recorded the staged changes as a new version with a commit message. | The user was trying to save a version of the project in the repository history. | It created a history of changes that could be reviewed later. |

## 2. User Needs

### UN-GIT-01 — Understand repository state

> **UN-GIT-01:** A developer needs a way to understand the current state of project files because they need to know what has changed before recording a new version.

### UN-GIT-02 — Review project changes

> **UN-GIT-02:** A developer needs a way to review changes made to project files because unintended changes should be identified before they are recorded.

### UN-GIT-03 — Control recorded changes

> **UN-GIT-03:** A developer needs a way to control which project changes are included in a new version because not every current change may be ready to be recorded.

## 3. User Requirements

| ID and short title | User requirement | Source user need | Rationale |
| ------------------ | ---------------- | ---------------- | --------- |
| UR-GIT-01 — View repository state | A developer shall be able to view the current state of project files before recording a new version. | UN-GIT-01 | The developer needs to identify files that have changed. |
| UR-GIT-02 — Review file changes | A developer shall be able to review changes made to project files before selecting them for a new version. | UN-GIT-02 | Reviewing changes helps identify unintended modifications. |
| UR-GIT-03 — Select changes | A developer shall be able to select specific project changes to include in the next version. | UN-GIT-03 | Not every current change may be ready to be recorded. |
| UR-GIT-04 — Review selected changes | A developer shall be able to review selected changes before recording a new version. | UN-GIT-03 | Reviewing selected changes helps verify that only intended changes will be recorded. |