# Slack + GitHub PR Comment Notifications — Setup Guide

## 1. Create the Slack App

1. Go to [https://api.slack.com/apps](https://api.slack.com/apps)
2. Click **Create New App** → **From scratch**
3. Name it something like `GitHub PR Notifications` and select your workspace
4. Click **Create App**

## 2. Enable Incoming Webhooks

1. In the app settings sidebar, click **Incoming Webhooks**
2. Toggle **Activate Incoming Webhooks** to **On**
3. Click **Add New Webhook to Workspace**
4. Select the channel where you want notifications (e.g. `#pr-reviews`)
5. Click **Allow**
6. Copy the **Webhook URL** — it looks like `https://hooks.slack.com/services/T.../B.../xxx`

## 3. Add the Webhook to GitHub

1. Go to your GitHub repository → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Name: `SLACK_WEBHOOK_URL`
4. Value: paste the webhook URL from step 2
5. Click **Add secret**

## 4. Add the Workflow

Copy the `.github/workflows/pr-comment-slack-notify.yml` file into your repository.

Push to your default branch and you're done! Any new comment on a PR will trigger a Slack notification.

## What triggers a notification?

- **General PR comments** (the main conversation tab)
- **Review comments** (inline code comments during a review)

Only new comments trigger notifications (not edits or deletions).

## Troubleshooting

- **Notifications not appearing?** Check that the `SLACK_WEBHOOK_URL` secret is set correctly and the webhook is active in your Slack app settings.
- **Only seeing some comments?** The workflow covers both general PR comments and inline review comments. Draft PR comments are also included.
- **Want to filter by repo or user?** You can add `if` conditions to the workflow to skip notifications from bots or specific users.
