---
title: GitHub Integration
type: feature
status: draft
sources: [raw/docs/devrev-agent-dump-integrations.md]
related: ["features/airdrop"]
last_updated: 2026-04-12
---

# GitHub Integration

## What it does
The GitHub integration connects DevRev with GitHub repositories, enabling automatic linking of PRs/branches/commits to DevRev issues, automatic stage transitions based on GitHub events, PR review task tracking, and bidirectional GitHub Issues sync via AirSync.

## Why it exists
Development teams use GitHub for code management. This integration closes the loop between code activity and issue tracking, automatically updating DevRev issue stages as code moves through the development lifecycle without manual status updates.

## Setup flow (step-by-step)

1. Go to the DevRev Marketplace and find **GitHub Integration**.
2. Click **Install** and follow the guided setup to connect your GitHub account.
3. The snap-in automatically registers a webhook for your GitHub organization. If auto-registration fails, manual webhook setup is available via **Settings -> Webhooks** in GitHub.
4. Select the events to subscribe to: branch/tag creation, pushes, pull requests, PR review comments, PR review threads, PR reviews.
5. Each developer who wants automatic work detection must link their GitHub account: **Settings -> Account -> External Identities -> Link GitHub Account**.

## How PRs auto-link to issues

Link GitHub activity to DevRev issues by mentioning issue IDs in:

- **Branch names** -- e.g. `mavis/iss-123/teaches-typing`. All commits in the branch are automatically associated with the issue.
- **Commit messages** -- e.g. `Fix: paging issue (issue:123)` or including the full DON.
- **PR titles** -- e.g. `iss-123 Fixes paging issue`.
- **PR body** -- using `/towards` or `/close` magic commands (see below).

Accepted ID formats (all case-insensitive): full DON (`<don:core:dvrv-us-1:devo/0:issue/123>`), `iss-123`, `issue:123`, `ISSUE:123`.

## Auto stage transitions

| GitHub event | Default DevRev stage |
|---|---|
| New branch created | In Development |
| Draft PR opened | In Development |
| PR opened | In Review |
| PR merged | In Development |
| PR closed | In Development |

Organizations can configure which stage each event maps to, or set **None** to disable stage updates for a specific event.

## Magic commands (in PR body)

- `/towards <issue-refs>` -- associates the PR with issues; stage automations apply as if IDs were in the title.
- `/close <issue-refs>` -- associates and closes the listed issues when the PR merges.
- `/close #work` -- closes all issues already associated with the PR.

## What data syncs

- **Code change objects:** Every PR generates a code change object capturing status, author, reviewers, approvals, commit history, timestamps, lines changed, and files modified. These link directly to DevRev issues.
- **PR review tasks:** A task is created for each requested reviewer in the linked DevRev issue. Tasks auto-complete when the reviewer approves, denies, or the PR closes.
- **PR inactivity reminders:** Configurable -- reminders are posted on linked DevRev issues when a PR has been inactive for a set number of days.
- **Autonomous issues:** If a branch or PR is created without an explicit issue link, DevRev auto-creates an issue and populates it with PR details.

### GitHub Issues AirSync (separate from the snap-in)

Supports bidirectional sync of GitHub issues, comments, and labels:

| GitHub object | DevRev object | Sync to DevRev | Sync to GitHub |
|---|---|---|---|
| Issue | Issue | Yes | Yes |
| Comment on Issue | Comment on Issue | Yes | Yes |
| Label on Issue | Tag on Issue | Yes | Yes |
| User | DevUser | Yes | No |
| Markdown File | Article | Yes | No |

## Key behaviors
- Webhook-based event detection (auto-registered or manual).
- Case-insensitive issue ID matching in branches, commits, PR titles, and PR bodies.
- Configurable stage transition mapping per GitHub event.
- Auto-creation of DevRev issues for unlinked branches/PRs.
- PR review tasks auto-complete on reviewer action.

## Entry points
- **Marketplace:** Settings -> Snap-ins -> Explore Marketplace -> search "GitHub"
- **Developer linking:** Settings -> Account -> External Identities -> Link GitHub Account
- **GitHub side:** Branch names, commit messages, PR titles/bodies with issue references

## Related flows
- [gap] GitHub PR to DevRev issue linking flow
- [gap] Auto stage transition flow

## Related scenarios
- [gap] Scenarios to be created

## Open questions
- [gap] What happens when a PR references issues across multiple DevRev organizations?
- [gap] How does the autonomous issue creation interact with existing issues?
- [gap] What is the exact behavior when webhook auto-registration fails?
