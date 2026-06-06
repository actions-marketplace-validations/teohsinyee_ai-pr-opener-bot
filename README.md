# AI PR Opener Bot

Open pull requests with a GitHub App so the human maintainer can stay in the review and approval path.

This is a self-hosted GitHub Action.
You bring your own GitHub App.
You keep full control of the workflow.

App page:

- [github.com/apps/ai-pr-opener-bot](https://github.com/apps/ai-pr-opener-bot)

## Why Use It

If AI helps write code, a solo developer can end up with an awkward review flow:

- your personal account opens the PR
- your personal account is also supposed to review and approve it

AI PR Opener Bot separates those roles.

The bot opens the pull request.
You keep your personal account for review, approval, and merge.

## Quick Start

1. Create or reuse your own GitHub App.
2. Add your GitHub App credentials as repository secrets.
3. Add a workflow that calls this action.
4. Customize reviewer, PR title, draft setting, and branch logic for your repo.

You do not install a hosted shared bot from this repository.
This action is designed for developers who want to keep their own GitHub App identity and customize the workflow.

Minimal example:

```yaml
name: Create PR via AI PR Opener Bot

on:
  workflow_dispatch:
    inputs:
      branch:
        description: Source branch
        required: true
        type: string
      title:
        description: Pull request title
        required: true
        type: string
      reviewer:
        description: Optional reviewer username
        required: false
        default: ""
        type: string

permissions:
  contents: read

jobs:
  create-pr:
    runs-on: ubuntu-latest
    steps:
      - name: Open pull request
        uses: teohsinyee/ai-pr-opener-bot@main
        with:
          app_id: ${{ secrets.PR_APP_ID }}
          private_key: ${{ secrets.PR_APP_PRIVATE_KEY }}
          branch: ${{ github.event.inputs.branch }}
          base: main
          title: ${{ github.event.inputs.title }}
          draft: true
          reviewer: ${{ github.event.inputs.reviewer || github.actor }}
```

Full example:

- [examples/workflow-dispatch.yml](./examples/workflow-dispatch.yml)

If you want a custom PR body, you can still pass the optional `body` input from your own workflow.

In the example workflow, `reviewer` is optional.
If the user leaves it blank, the action requests review from the person who triggered the workflow.

## What You Need

- your own GitHub App
- a repository secret for the App ID
- a repository secret for the App private key
- a workflow in your repo that calls this action

## Inputs

- `app_id`: GitHub App ID
- `private_key`: GitHub App private key in PEM format
- `branch`: source branch
- `base`: target branch, default `main`
- `title`: pull request title
- `body`: optional pull request body in Markdown
- `draft`: `true` or `false`, default `true`
- `reviewer`: optional GitHub username to request for review

## Outputs

- `pr-number`: created pull request number
- `pr-url`: created pull request URL

## What It Does

- opens a pull request from a source branch to a base branch
- supports draft pull requests
- requests a reviewer automatically
- keeps PR opening separate from human approval

## Required Permissions

Your GitHub App should have:

- `Contents`: `Read and write`
- `Pull requests`: `Read and write`
- `Metadata`: `Read`

## Typical Flow

1. Push a branch with your changes.
2. Trigger your GitHub Actions workflow that uses this action.
3. The app opens the PR.
4. Review is requested automatically.
5. You review, approve, and merge with your personal account.

## Best For

- solo developers using AI-assisted coding
- repos that want PR opening separated from human approval
- teams that prefer bring-your-own-app workflows
- developers who want to customize their own GitHub Actions logic

## Current Status

This project is intentionally simple and focused on one job:

- open PRs cleanly
- keep the review path human
