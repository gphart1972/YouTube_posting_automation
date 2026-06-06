📺 YouTube → Discord Automation (PowerShell, RSS‑Based, No API Key)

![PowerShell Automation](https://img.shields.io/badge/PowerShell-Automation-blue)

📌 What This Script Does
This PowerShell script automatically:

Monitors multiple YouTube channels for new uploads

Uses the official YouTube RSS feed (no API key, no quotas, no cost)

Skips livestreams and upcoming streams

Posts new uploads to Discord via webhook

Prevents duplicate posts using per‑channel tracking files

This is a lightweight, zero‑dependency, zero‑cost YouTube → Discord automation.

🚀 Features
✅ No API key required (RSS feed only)

✅ Monitors multiple channels

✅ Skips livestreams using title‑based filtering

✅ Posts only once per upload

✅ Clean Discord embed formatting

✅ Per‑channel tracking files

✅ No quotas, no authentication, no billing

✅ Works on PowerShell 5.1 and 7+

📸 Example Output
When a new upload is detected:

Title appears as a clickable link

Thumbnail is displayed

Message is posted automatically to Discord

Livestreams are ignored

Example console output:

Code
ENTRY: videoId=3Z9zZdLRV3E  title='Dont cross the Stream(S)'
  -> Skipping livestream based on TITLE
ENTRY: videoId=GD3IdR-bTLU  title='Mummy Bread'
  -> Using this entry
New upload from Habitual Linecrosser: Mummy Bread
Posted to Discord
⚡ Quick Start
Clone this repository

Edit the script to add your YouTube channels

Add your Discord webhook URL

Run the script manually or via Task Scheduler

Example:

powershell
powershell.exe -ExecutionPolicy Bypass -File General_Topic_YT_mcms.ps1
⚙️ Requirements
Windows PowerShell or PowerShell Core

A Discord webhook URL

Internet access

No API key required

🔗 Discord Webhook Setup
Open your Discord server

Go to Channel Settings → Integrations → Webhooks

Click Create Webhook

Copy the webhook URL

Paste it into the script

🧩 Configuration
1. Add your channels
Inside the script:

powershell
$Channels = @{
    "CHANNEL_ID_1" = "Friendly Name 1"
    "CHANNEL_ID_2" = "Friendly Name 2"
}
Example:

powershell
$Channels = @{
    "UC6ysC3YUZbjScBKZlNLrmtQ" = "Habitual Linecrosser"
    "UC_T3Zsw2257Ke-g3F20ZCRA" = "The Fat Electrician"
}
2. Add your Discord webhook
powershell
$webhookUrl = "https://discord.com/api/webhooks/XXXX/XXXX"
🗂️ How It Works
Script fetches the RSS feed for each channel

It loops through entries and skips livestreams

It selects the newest real upload

Compares it to the per‑channel tracking file

If new:

Posts to Discord

Saves the video ID

If same:

Does nothing

Tracking files look like:

Code
last_video_<channelId>.txt
▶️ Running the Script
Manual run:

powershell
powershell.exe -ExecutionPolicy Bypass -File General_Topic_YT_mcms.ps1
🔁 Automate with Task Scheduler
Program:

Code
powershell.exe
Arguments:

Code
-ExecutionPolicy Bypass -File C:\Path\General_Topic_YT_mcms.ps1
Start in:

Code
C:\Path\
Set it to run every 5–15 minutes.

📁 Script (RSS‑Based, Livestream‑Skipping)
Your repo should include the full script file, but here is the high‑level summary:

Uses YouTube RSS feed

Skips livestreams by filtering titles containing “live” or “stream”

Posts real uploads to Discord

Maintains per‑channel tracking files

⚠️ Notes
First run initializes tracking files (no posting)

Livestreams are skipped automatically

If you want to force a repost, delete the tracking file

Works with any number of channels
