# Slack + GitHub PR Comment Notifications — Setup Guide

## 1. Create the Slack App

1. Go to [https://api.slack.com/apps](https://api.slack.com/apps)
2. Click **Create New App** → **From an app manifest**
3. Select your workspace
4. Paste the contents of `slack-app-manifest.json` from this repo
5. Click **Create**

## 2. Install the App and Get the Bot Token

1. In the app settings sidebar, click **Install App**
2. Click **Install to Workspace** and authorize
3. Copy the **Bot User OAuth Token** (`xoxb-...`)

## 3. Get Your Slack Channel ID

1. In Slack, right-click the channel you want notifications in (e.g. `#pr-reviews`)
2. Click **View channel details**
3. At the bottom of the popup, copy the **Channel ID** (e.g. `C0123456789`)

## 4. Add Secrets to GitHub

1. Go to your GitHub repository → **Settings** → **Secrets and variables** → **Actions**
2. Add two repository secrets:
   - `SLACK_BOT_TOKEN` — the `xoxb-...` token from step 2
   - `SLACK_CHANNEL_ID` — the channel ID from step 3

## 5. Add the Workflow

Copy the `.github/workflows/pr-comment-slack-notify.yml` file into your repository.

Push to your default branch and you're done! Any new comment on a PR will trigger a Slack notification with the commenter's GitHub avatar and username.

## What triggers a notification?

- **General PR comments** (the main conversation tab)
- **Review comments** (inline code comments during a review)

Only new comments trigger notifications (not edits or deletions).

## Troubleshooting

- **Notifications not appearing?** Check that the `SLACK_BOT_TOKEN` and `SLACK_CHANNEL_ID` secrets are set correctly.
- **Avatar not showing?** The `chat:write.customize` scope is required. Reinstall the app if you added it after the initial install.
- **"not_in_channel" error?** The bot auto-joins public channels. For private channels, you need to manually invite it with `/invite @GitHub Comments`.
