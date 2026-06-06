# AI PR Opener Bot

Open pull requests with a GitHub App so the human maintainer can stay in the review and approval path.

App page:

- [github.com/apps/ai-pr-opener-bot](https://github.com/apps/ai-pr-opener-bot)

## Why Use It

If AI helps write code, a solo developer can end up with an awkward review flow:

- your personal account opens the PR
- your personal account is also supposed to review and approve it

AI PR Opener Bot separates those roles.

The bot opens the pull request.
You keep your personal account for review, approval, and merge.

## What It Does

- opens a pull request from a source branch to a base branch
- supports draft pull requests
- requests a reviewer automatically
- keeps PR opening separate from human approval

## Install

1. Open the app page:
   [github.com/apps/ai-pr-opener-bot](https://github.com/apps/ai-pr-opener-bot)
2. Click `Install`.
3. Choose your personal account or organization.
4. Select the repository or repositories where you want to use it.

## Required Permissions

The current workflow uses:

- `Contents`: `Read and write`
- `Pull requests`: `Read and write`
- `Metadata`: `Read`

## Typical Flow

1. Push a branch with your changes.
2. Trigger your GitHub Actions workflow that uses this GitHub App.
3. The app opens the PR.
4. Review is requested automatically.
5. You review, approve, and merge with your personal account.

## Best For

- solo developers using AI-assisted coding
- repos that want PR opening separated from human approval
- lightweight GitHub App based PR workflows

## Current Status

This project is intentionally simple and focused on one job:

- open PRs cleanly
- keep the review path human
