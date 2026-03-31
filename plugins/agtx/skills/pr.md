---
name: agtx-pr
description: Prepare branch and create a GitHub PR. Resolve conflicts, clean commits, create PR with intent-focused description, write .agtx/pr.md.
---

# PR Phase

You are in the **PR phase** of an agtx-managed task. Your goal is to prepare the branch and open a GitHub Pull Request.

## Instructions

### 1. Check for merge conflicts

Run `git fetch origin` then check for conflicts with the default branch. If conflicts exist, resolve them before proceeding (same approach as the merge-conflicts skill).

### 2. Review and clean commits

Run `git log main..HEAD --oneline`. Ensure all commits have descriptive messages. Squash or amend any "WIP", "fixup", or vague commits. The commit history should tell a clear story.

### 3. Verify no scratch files are committed

Check that `.agtx/` scratch files (research.md, plan.md, execute.md, review.md) are not tracked in the commit. They should be gitignored — if any were accidentally staged, unstage and remove them from the commit history.

### 4. Create the Pull Request

Run `gh pr create` with a title and description. The PR description must:

- **Explain the intent and motivation** — why this change was made, what problem it solves, what decision was made and why
- **Not summarize the code** — reviewers can read the diff and commit messages for that; the PR description adds context they cannot get from the code alone
- **Only call out surprising or non-obvious API/behavioral changes** explicitly — anything that would surprise a reviewer who wasn't involved in the task
- Keep it concise: a few focused sentences are better than a long summary

**Example of a bad description:** "Added a new `PR` status to the TaskStatus enum and updated all match arms. Modified app.rs to add transition_to_pr function and remove ReviewConfirmPopup struct..."

**Example of a good description:** "Splits the Review step into two phases so self-review and PR creation are decoupled. This lets the agent finish reviewing and annotating commits before the PR is opened, rather than creating the PR immediately when moving out of Running."

### 5. Write the artifact

Write `.agtx/pr.md` with the PR URL:

```
# PR Created

{PR URL here}
```

## CRITICAL: Stop After Writing

After writing `.agtx/pr.md`:
- Say: "PR created. Details in `.agtx/pr.md`."
- Wait for further instructions
