# YouTube_posting_automation
This repo will provide a PowerShell script that can be used to automate posting of YouTube videos to apps like Discord.
# 📺 YouTube to Discord Notifier (PowerShell)

A simple PowerShell script that monitors a YouTube channel and automatically posts new uploads to a Discord channel using a webhook — with rich embed previews.

---

## 🚀 Features

- ✅ Detects newest video from a YouTube channel
- ✅ Posts only **once per video** (no duplicates)
- ✅ Saves last video ID locally
- ✅ Discord embed with:
  - Clickable title
  - Thumbnail preview
- ✅ Lightweight (no external dependencies)

---

## 📸 Example Output

When a new video is uploaded:

- ✅ Title appears as clickable link
- ✅ Thumbnail is displayed
- ✅ Message is posted automatically to Discord

---

## ⚙️ Requirements

- Windows PowerShell (or PowerShell Core)
- YouTube Data API v3 key
- Discord webhook URL

---

## 🔑 Setup Instructions

### 1. Get a YouTube API Key

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable **YouTube Data API v3**
4. Create API credentials → copy your API key

---

### 2. Get YouTube Channel ID

- Go to the channel page
- In the bio section, click on more (should open a pop-up)
- scroll to bottom, find the share option, should give two options, one is channel ID
- Use URL or advanced settings
- Example: `UC-Fm2Ezn2Avm97IY3vMpKwA`

---

### 3. Create a Discord Webhook

1. Open Discord, go to the text channel you want the videos posted to.
2. Click on the little gear icon to the right of the channel name, this is settings for that channel, but it says edit channel
3. once you do that on the left find the "Integrations page, select that then "Create Webhook"
4. You can give the Webhook a name other than the random name Discord gives it, then click save at the bottom
5. Copy the webhook URL

---

### 4. Configure the Script
I recommend that you save this script to a location like C:\scripts
I also highly recommend that you create a unique folder for this script if you plan to have more than one.

Edit the script and look for these variables below to make it work for you.

$apiKey = "YOUR_API_KEY"
#You got this from Google Cloud Console
$channelId = "YOUR_CHANNEL_ID"
#You got this from the YouTube Channel
$webhookUrl = "YOUR_DISCORD_WEBHOOK"
#You got this from Discord
