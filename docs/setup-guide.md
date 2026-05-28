# Setup Guide

## Prerequisites

- A running n8n instance (self-hosted or [n8n cloud](https://n8n.io))
- A free [Groq account](https://console.groq.com)
- A Telegram account + Bot token
- A Google account with access to Google Sheets
- (Optional) An X Developer account

---

## Step 1 — Import Workflows

1. Open your n8n instance
2. Click **"+ New Workflow"** → **"Import from file"**
3. Import `daily-content-generator.workflow.json`
4. Repeat for `daily-x-publisher.workflow.json`

---

## Step 2 — Connect Groq

1. Go to [console.groq.com](https://console.groq.com) and create a free API key
2. In n8n, open the **Groq Chat Model** node
3. Add a new credential and paste your API key
4. Model: `llama-3.3-70b-versatile`

---

## Step 3 — Connect Telegram

1. Create a bot via [@BotFather](https://t.me/BotFather) on Telegram
2. Copy the bot token
3. Get your chat ID by messaging [@userinfobot](https://t.me/userinfobot)
4. In n8n, open the **Review via Telegram** node
5. Add your bot token as a credential
6. Set your chat ID in the `chatId` field

---

## Step 4 — Connect Google Sheets

1. Create a new Google Sheet with these columns:
   - `tweet_text`
   - `status`
   - `created_date`
   - `posted_date`
2. In n8n, connect your Google account via OAuth2
3. Select your sheet in the **Save to Sheet** and **Read Approved Tweets** nodes

See `sample-data/sample-data.csv` for an example of the expected format.

---

## Step 5 — Set Your RSS Feed

1. Open the **Fetch News** node
2. Replace the URL with your preferred RSS feed
3. Example using Google News proxy:
   ```
   https://news.google.com/rss/search?q=site:YOUR_SITE.com&hl=en-US&gl=US&ceid=US:en
   ```

---

## Step 6 — Activate

1. Activate **Daily Content Generator** — runs at 9:00 AM daily
2. Activate **Daily X Publisher** — runs at 10:00 AM daily

---

## How Approval Works

When a tweet is generated, you receive a Telegram message with two buttons:

- ✅ **Approve** → saved to Google Sheets with status `pending`
- ❌ **Skip** → discarded

You can then manually post from the Sheet, or let Workflow 2 handle it automatically.
