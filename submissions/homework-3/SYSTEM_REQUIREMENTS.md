# Homework 3 — System Requirements and Verification

## Approved UN/UR Baseline

### Stakeholder Needs

| ID | Stakeholder Need |
|:---|:---|
| UN-GIT-01 | A student developer needs a way to start tracking a local project because it has no recorded history. |
| UN-GIT-02 | A student developer needs to know which project files have changed because they may forget what they edited before recording a checkpoint. |
| UN-GIT-03 | A student developer needs to inspect changed content before recording it because a file may contain unintended edits. |
| UN-GIT-04 | A student developer needs to choose the file content to include in the next checkpoint because some current changes may still be unfinished. |
| UN-GIT-05 | A student developer needs to record a meaningful checkpoint because they want to record an important project version and provide a descriptive label. |
| UN-GIT-06 | A student developer needs to review earlier checkpoints because they want to understand how the project reached its current state. |
| UN-GIT-07 | A student developer needs invalid commands to explain why they failed while preserving existing project files and recorded checkpoints. |

### User Requirements

| ID | User-Visible Capability | Need |
|:---|:---|:---|
| UR-GIT-01 | A student developer shall be able to initialize tracking in the current local project folder without removing existing project files. | UN-GIT-01, UN-GIT-07 |
| UR-GIT-02 | A student developer shall be able to see whether project files are untracked, staged, changed after staging, modified, deleted, or clean. | UN-GIT-02 |
| UR-GIT-03 | A student developer shall be able to view differences between current working file content and the content selected for the next checkpoint. | UN-GIT-03 |
| UR-GIT-04 | A student developer shall be able to view differences between content selected for the next checkpoint and the latest recorded checkpoint. | UN-GIT-03 |
| UR-GIT-05 | A student developer shall be able to select the current content of one existing project file for the next checkpoint without selecting unrelated files. | UN-GIT-04 |
| UR-GIT-06 | A student developer shall be able to create a checkpoint of selected content with a nonempty explanation while leaving later unselected edits in the working files. | UN-GIT-05, UN-GIT-04 |
| UR-GIT-07 | A student developer shall be able to view recorded checkpoints from newest to oldest, including their identifier and explanation. | UN-GIT-06 |
| UR-GIT-08 | A student developer shall receive a useful error when a command is invalid, a requested file is unavailable, or a path is outside the allowed project files. | UN-GIT-07 |
| UR-GIT-09 | A student developer shall be able to retry an operation after a failure without losing ordinary project files or an already recorded checkpoint. | UN-GIT-07 |

## UR-to-UN Mapping

| User Requirement | Source Need |
|:---|:---|
| UR-GIT-01 | UN-GIT-01, UN-GIT-07 |
| UR-GIT-02 | UN-GIT-02 |
| UR-GIT-03 | UN-GIT-03 |
| UR-GIT-04 | UN-GIT-03 |
| UR-GIT-05 | UN-GIT-04 |
| UR-GIT-06 | UN-GIT-05, UN-GIT-04 |
| UR-GIT-07 | UN-GIT-06 |
| UR-GIT-08 | UN-GIT-07 |
| UR-GIT-09 | UN-GIT-07 |

## Functional System Requirements

### SR-01 — First initialization

**Source:** UR-GIT-01

Given a local project that has not been initialized, when `init` is used, MiniGit shall initialize tracking for the project without changing any existing project files.

**Check:** Confirm that the project is recognized as initialized and that the existing project files are unchanged.

### SR-02 — Repeated initialization

**Source:** UR-GIT-01, UR-GIT-09

Given a project that is already initialized and contains an existing recorded checkpoint, when `init` is used again, MiniGit shall leave the project initialized without changing existing project files or recorded checkpoints.

**Check:** Compare the project files and recorded checkpoint before and after the repeated `init` and confirm that they are unchanged.

### SR-03 — Add one existing file

**Source:** UR-GIT-05

Given an initialized project with `notes.txt` containing `ONE` and `plan.txt` present, when `add notes.txt` is used, MiniGit shall copy the current content `ONE` of `notes.txt` to the stage without staging `plan.txt`.

**Check:** Confirm that staged `notes.txt` contains `ONE` and that `plan.txt` is not staged.

### SR-04 — Add a missing file

**Source:** UR-GIT-08, UR-GIT-09

Given an initialized project with `notes.txt` already staged and an existing recorded checkpoint, but without `missing.txt`, when `add missing.txt` is used, MiniGit shall report that `missing.txt` does not exist and leave the staged content and recorded checkpoints unchanged.

**Check:** Confirm that the error appears, staged `notes.txt` is unchanged, and the existing checkpoint remains recorded.

### SR-05 — Status for one staged file

**Source:** UR-GIT-02

Given an initialized project with `notes.txt` staged and no later edits to that file, when `status` is used, MiniGit shall report `notes.txt` as staged.

**Check:** Confirm that `status` reports `notes.txt` as staged.

### SR-06 — Status after editing a staged file

**Source:** UR-GIT-02

Given an initialized project where `notes.txt` containing `ONE` was staged and its working content was later changed to `TWO` without another `add`, when `status` is used, MiniGit shall report `notes.txt` as changed after staging.

**Check:** Confirm that `status` reports `notes.txt` as changed after staging while the staged content remains `ONE`.

### SR-07 — Status for a deleted tracked file

**Source:** UR-GIT-02

Given an initialized project with a tracked `notes.txt` that has been deleted from the working project, when `status` is used, MiniGit shall report `notes.txt` as deleted.

**Check:** Confirm that `status` reports `notes.txt` as deleted.

### SR-08 — Working-to-stage diff

**Source:** UR-GIT-03

Given an initialized project where staged `notes.txt` contains `ONE` and working `notes.txt` contains `TWO`, when `diff` is used, MiniGit shall display a whole-file BEFORE/AFTER comparison showing `ONE` as BEFORE and `TWO` as AFTER.

**Check:** Confirm that the output shows BEFORE as `ONE` and AFTER as `TWO`.

### SR-09 — Stage-to-checkpoint diff

**Source:** UR-GIT-04

Given an initialized project whose latest checkpoint contains `notes.txt` with `OLD` and whose staged copy contains `NEW`, when `diff --staged` is used, MiniGit shall display a whole-file BEFORE/AFTER comparison showing `OLD` as BEFORE and `NEW` as AFTER.

**Check:** Confirm that the output shows BEFORE as `OLD` and AFTER as `NEW`.

### SR-10 — Create a checkpoint

**Source:** UR-GIT-06

Given an initialized project with `notes.txt` staged as `ONE` and a later unstaged working edit changing it to `TWO`, when `commit -m "Save notes"` is used, MiniGit shall create a new numbered checkpoint containing staged content `ONE` with explanation `Save notes` while leaving working `notes.txt` containing `TWO`.

**Check:** Confirm that the new numbered checkpoint contains `ONE` and explanation `Save notes`, while working `notes.txt` still contains `TWO`.

### SR-11 — View checkpoint history

**Source:** UR-GIT-07

Given an initialized project containing multiple recorded checkpoints, when `log` is used, MiniGit shall display the checkpoints from newest to oldest and include each checkpoint's identifier and explanation.

**Check:** Confirm that `log` lists all checkpoints newest to oldest with their identifiers and explanations.

### SR-12 — Invalid command preserves project state

**Source:** UR-GIT-08, UR-GIT-09

Given an initialized project containing ordinary project files and an existing recorded checkpoint, when an unsupported command is used, MiniGit shall display a useful error identifying the command as invalid and leave the project files and recorded checkpoints unchanged.

**Check:** Confirm that the error appears and that the ordinary project files and existing checkpoint remain unchanged.

## Acceptance Tests

| Test | Covers | Given | When | Expected Result |
|:---|:---|:---|:---|:---|
| AT-01 | SR-01 | Uninitialized project containing `notes.txt` with `ONE` | `init` | Project becomes initialized and `notes.txt` remains `ONE`. |
| AT-02 | SR-02 | Initialized project with an existing checkpoint | `init` | Project remains initialized; files and checkpoint remain unchanged. |
| AT-03 | SR-03 | `notes.txt` contains `ONE`; `plan.txt` exists; neither is staged | `add notes.txt` | `notes.txt` containing `ONE` is staged and `plan.txt` is not staged. |
| AT-04 | SR-04 | `notes.txt` is staged, a checkpoint exists, and `missing.txt` does not exist | `add missing.txt` | Missing-file error appears; stage and checkpoint remain unchanged. |
| AT-05 | SR-05 | `notes.txt` is staged with no later edit | `status` | `notes.txt` is reported as staged. |
| AT-06 | SR-06 | `notes.txt` was staged as `ONE` and then edited to `TWO` | `status` | `notes.txt` is reported as changed after staging. |
| AT-07 | SR-07 | Tracked `notes.txt` has been deleted | `status` | `notes.txt` is reported as deleted. |
| AT-08 | SR-08 | Staged `notes.txt` is `ONE`; working version is `TWO` | `diff` | BEFORE is `ONE`; AFTER is `TWO`. |
| AT-09 | SR-09 | Checkpoint `notes.txt` is `OLD`; staged version is `NEW` | `diff --staged` | BEFORE is `OLD`; AFTER is `NEW`. |
| AT-10 | SR-10 | Staged `notes.txt` is `ONE`; working version is `TWO` | `commit -m "Save notes"` | Numbered checkpoint contains `ONE` and explanation `Save notes`; working file remains `TWO`. |
| AT-11 | SR-11 | Multiple checkpoints exist | `log` | Checkpoints appear newest to oldest with identifiers and explanations. |
| AT-12 | SR-12 | Initialized project with files and a checkpoint | Unsupported command | Useful error appears; files and checkpoint remain unchanged. |

## Verification Methods

| SR | Verification Method |
|:---|:---|
| SR-01 | Test `init` and inspect initialization state and existing files. |
| SR-02 | Test repeated `init` and compare files and checkpoints before and after. |
| SR-03 | Test `add notes.txt` and inspect staged and unrelated files. |
| SR-04 | Test `add missing.txt` and inspect the error, stage, and checkpoints. |
| SR-05 | Test `status` and inspect the staged-file output. |
| SR-06 | Test `status` after editing a staged file and inspect the output and staged content. |
| SR-07 | Test `status` after deleting a tracked file and inspect the output. |
| SR-08 | Test `diff` and inspect the whole-file BEFORE/AFTER output. |
| SR-09 | Test `diff --staged` and inspect the whole-file BEFORE/AFTER output. |
| SR-10 | Test `commit -m "Save notes"` and inspect the checkpoint, explanation, snapshot, and working file. |
| SR-11 | Test `log` and inspect checkpoint order, identifiers, and explanations. |
| SR-12 | Test an unsupported command and compare files and checkpoints before and after. |

## Traceability Matrix

| System Requirement | User Requirement(s) | Acceptance Test |
|:---|:---|:---|
| SR-01 | UR-GIT-01 | AT-01 |
| SR-02 | UR-GIT-01, UR-GIT-09 | AT-02 |
| SR-03 | UR-GIT-05 | AT-03 |
| SR-04 | UR-GIT-08, UR-GIT-09 | AT-04 |
| SR-05 | UR-GIT-02 | AT-05 |
| SR-06 | UR-GIT-02 | AT-06 |
| SR-07 | UR-GIT-02 | AT-07 |
| SR-08 | UR-GIT-03 | AT-08 |
| SR-09 | UR-GIT-04 | AT-09 |
| SR-10 | UR-GIT-06 | AT-10 |
| SR-11 | UR-GIT-07 | AT-11 |
| SR-12 | UR-GIT-08, UR-GIT-09 | AT-12 |