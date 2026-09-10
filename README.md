# Hacker News RSS to Discord Automated Notifier

An automated n8n workflow designed to fetch live news feeds, eliminate duplicate posts using an internal database, and deliver high-value industry updates directly to your Discord community.

---

## 🌟 Overview

Keeping team members or community channels informed with real-time news usually requires manual browsing and repetitive sharing. This workflow automates content curation by monitoring the **Hacker News RSS feed**, filtering out previously shared articles, and instantly broadcasting fresh updates to a designated Discord channel.

### Key Business Benefits
* **Zero Manual Effort:** Runs automatically on a background schedule without human intervention.
* **Smart Deduplication:** Tracks sent links in a database to prevent posting the same article twice.
* **Noise Reduction:** Limits updates to the top 5 newest items every cycle to avoid cluttering channels.
* **Workspace Integration:** Keeps your team informed directly inside Discord.

---

## ⚙️ How It Works

1. **Trigger:** Fires automatically every 15 minutes.
2. **Fetch Feed:** Pulls the latest front-page articles via RSS.
3. **Deduplicate:** Cross-checks article URLs against an n8n Data Table to skip previously logged posts.
4. **Throttle:** Filters the remaining new items to the top 5 updates.
5. **Format & Post:** Generates formatted messages and posts them to Discord via Webhook.
6. **Log Data:** Saves newly posted article links to the Data Table for future deduplication.

---

## 🚀 Setup & Installation

### Prerequisites
* An active **n8n** instance (Self-hosted or Cloud).
* A **Discord Server** with administrator rights to create a Webhook.

---

### Step 1: Create a Discord Webhook
1. Open your Discord server and go to **Channel Settings** (gear icon) for your target channel.
2. Navigate to **Integrations** ➔ **Webhooks** ➔ **New Webhook**.
3. Copy the **Webhook URL**.

---

### Step 2: Set Up the Data Table in n8n
1. In your n8n dashboard, go to **Data Tables** on the left menu.
2. Create a new Data Table named: `RSS Discord Bot - Posted Items`.
3. Add two string columns:
   * `link` (Text)
   * `title` (Text)

---

### Step 3: Import & Configure Workflow
1. Copy the contents of [`workflow.json`](./workflow.json) from this repository.
2. Open n8n, click **New Workflow**, and paste the JSON directly onto the canvas (or select **Import from File**).
3. Open the **`Post to Discord`** HTTP Request node:
   * Replace `YOUR_DISCORD_WEBHOOK_URL_HERE` with your actual Discord Webhook URL.
4. Open both **`Skip Already-Posted Items`** and **`Log Posted Item`** nodes:
   * Select your newly created Data Table from the dropdown menu.
5. Save and **Activate** the workflow.

---

## 🛡️ Security Note

Never share workflow JSON files that contain live Webhook URLs or API credentials. Always replace sensitive endpoints with placeholder variables prior to committing code publicly.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
