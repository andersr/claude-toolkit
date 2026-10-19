---
description: Start a new task from a Linear ticket
argument-hint: [ticket-id]
allowed-tools: Bash(git:*), mcp__linear__get_issue, AskUserQuestion, EnterPlanMode
---

You are helping the user start a new development task based on a Linear ticket.

## Step 1: Get the Ticket ID

The user may have provided a ticket ID: $ARGUMENTS

If the ticket ID is empty or not provided, use the AskUserQuestion tool to ask the user for the Linear ticket ID before proceeding.

## Step 2: Fetch the Linear Ticket

Once you have the ticket ID, use the Linear MCP to fetch the full ticket details including:

- Title
- Description
- Status
- Labels
- Assignee
- Any other relevant context

## Step 3: Create a Git Branch, if needed

Based on the ticket ID, if we are not already on this branch, create a new git branch using the ticket ID as the branch name.

Before creating the branch:

1. Check the current git status to ensure the working directory is clean
2. Ensure you're on the main/master branch (or ask the user which base branch to use if unclear)
3. Pull the latest changes from the remote
4. Create and checkout the new branch

## Step 4: Enter Planning Mode

Once you have the ticket details and the branch is created, use the EnterPlanMode tool to help the user plan the implementation.

When entering planning mode, provide context including:

- The ticket title and description
- Any acceptance criteria or requirements from the ticket
- Relevant labels or metadata
- The goal: create an implementation plan for this task

## Error Handling

- If the Linear ticket is not found, inform the user and ask them to verify the ticket ID
- If there are uncommitted changes, ask the user how they want to handle them (stash, commit, or cancel)
- If the branch already exists, ask the user if they want to switch to it or create a new one with a different name

## Example Usage

When the user runs: `/start-task ABC-123`

You will:

1. Fetch Linear ticket ABC-123
2. Create branch `ABC-123`
3. Enter planning mode with the ticket context
