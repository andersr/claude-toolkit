---
description: Create a pull request for the current branch
allowed-tools: Bash(git:*), Bash(gh:*), mcp__linear__get_issue, AskUserQuestion
---

Create a pull request for the current branch.

## Step 1: Gather Context

First find the base branch: `gh repo view --json defaultBranchRef --jq .defaultBranchRef.name`. Use it as `<base>` below.

Then run these in parallel:

- `git status` to check for uncommitted changes
- `git log <base>..HEAD --oneline` to see all commits on this branch
- `git diff <base>...HEAD --stat` to see changed files
- Look for a PR template (`.github/pull_request_template.md`, `.github/PULL_REQUEST_TEMPLATE.md`, or `.github/PULL_REQUEST_TEMPLATE/`)

If there are uncommitted changes, ask the user if they want to commit them first.

## Step 2: Determine Linear Ticket

Check the branch name — if it matches a Linear ticket ID pattern (e.g., `ABC-123`), fetch the ticket details using the Linear MCP to get the title and description for the PR.

If the branch name doesn't match a ticket pattern, ask the user if there's a related Linear ticket.

## Step 3: Create the PR

Push the branch if needed, then create the PR against `<base>` using `gh pr create`.

- **Title**: Use the Linear ticket title if available, otherwise derive from commits. Keep under 70 characters.
- **Body**: If the repository has a PR template, fill it in. Otherwise use this format:

```markdown
## Summary
<1-3 bullet points summarizing the changes>

## Linear Ticket
<Link to the Linear ticket if available, otherwise omit this section>

## Test plan
<Bulleted checklist of how to test the changes>

<attribution>
```

For `<attribution>`, use the exact pull request attribution line given in your
environment instructions, if any; otherwise omit it.

## Step 4: Report

Return the PR URL to the user.
