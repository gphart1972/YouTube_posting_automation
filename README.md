![PowerShell Automation](https://img.shields.io/badge/PowerShell-Automation-blue)

## 📌 What This Does

This script automatically:

- Checks a YouTube channel for new uploads
- Posts new videos to a Discord channel or to a Slack Channel
- Prevents duplicate posts using a local tracking file

---

## 🚀 Features

- ✅ Detects newest video from a YouTube channel
- ✅ Posts only **once per video** (no duplicates)
- ✅ Saves last video ID locally
- ✅ Discord embed with:
  - Clickable title
  - Thumbnail preview
- ✅ Slack embed with:
  - Bold title
  - clickable link
  - thumbnail image
  - structured layout (Block Kit)
- ✅ Lightweight (no external dependencies)

---

## 📸 Example Output

When a new video is uploaded:

- ✅ Title appears as clickable link
- ✅ Thumbnail is displayed
- ✅ Message is posted automatically to Discord

---

## ⚡ Quick Start

1. Add your API key  
2. Add your Discord webhook  
3. Run the script  

```powershell
powershell.exe -ExecutionPolicy Bypass -File youtube.ps1
```

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
- Scroll to bottom, find the share option, should give two options, one is channel ID
- Use URL or advanced settings
- Example: `UC-Fm2Ezn2Avm97IY3vMpKwA`

---

### 3. Create a Discord Webhook

1. Open Discord, go to the text channel you want the videos posted to.
2. Click on the little gear icon to the right of the channel name, this is settings for that channel, but it says "edit channel".
3. Once you do that on the left find the "Integrations page, select that then "Create Webhook"
4. You can give the Webhook a name other than the random name Discord gives it, then click save at the bottom
5. Copy the webhook URL

---

### 4. Configure the Script
I recommend that you save this script to a location like C:\scripts
I also highly recommend that you create a unique folder for this script if you plan to have more than one.

Edit the script and look for these variables below to make it work for you.

```powershell

$apiKey = "YOUR_API_KEY"
#You got this from Google Cloud Console
$channelId = "YOUR_CHANNEL_ID"
#You got this from the YouTube Channel
$webhookUrl = "YOUR_DISCORD_WEBHOOK"
#You got this from Discord
```

▶️ How to Run
Run manually: powershell.exe -ExecutionPolicy Bypass -File youtube.ps1

🔁 Automate (Recommended)
Use Windows Task Scheduler:

Run every 5–10 minutes
Set:

Program/script: powershell.exe
Arguments: -ExecutionPolicy Bypass -File C:\Path\youtube.ps1
Start in: script folder

📁 How It Works

Fetch latest uploaded video via YouTube API
Compare with last stored video ID (last_video.txt)
If new:

Send Discord message
Update stored ID

If same:
Do nothing

🗂️ File Storage
The script creates:
---
last_video.txt
---
This file stores the last posted video ID to prevent duplicates.

✅ Script
```powershell
$apiKey = "Your_Google_API_goes_here"
$channelId = "YouTube_Channel_ID_goes_here"

$webhookUrl = "Your_Discord_Web_Hook_goes_here"

$lastFile = Join-Path $PSScriptRoot "last_video.txt"

if (Test-Path $lastFile) {
    $lastVideo = (Get-Content $lastFile -Raw).Trim()
} else {
    $lastVideo = ""
}

$url = "https://www.googleapis.com/youtube/v3/search?key=$apiKey&channelId=$channelId&part=snippet,id&order=date&maxResults=1"

$response = Invoke-RestMethod -Uri $url

$videoId = $response.items[0].id.videoId
$title   = $response.items[0].snippet.title
$link    = "https://www.youtube.com/watch?v=$videoId"
$thumb   = $response.items[0].snippet.thumbnails.high.url

if ($lastVideo -eq "") {
    Set-Content -Path $lastFile -Value $videoId -NoNewline
}
elseif ($videoId -ne $lastVideo) {

    $payload = @{
        username = "Your Bot Name"
        embeds = @(
            @{
                title = $title
                url   = $link
                image = @{
                    url = $thumb
                }
            }
        )
    } | ConvertTo-Json -Depth 5

    Invoke-RestMethod -Uri $webhookUrl -Method POST -Body $payload -ContentType "application/json"

    Set-Content -Path $lastFile -Value $videoId -NoNewline
}
```

⚠️ Notes
First run will initialize only (no posting)
Make sure API quota is sufficient
Ensure webhook URL is valid
