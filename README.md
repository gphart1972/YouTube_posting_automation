# 📺 YouTube → Discord / Slack / Teams Automation (PowerShell)

![PowerShell Automation](https://img.shields.io/badge/PowerShell-Automation-blue)

## 📌 What This Does

This script automatically:

- Checks a YouTube channel for new uploads
- Posts new videos to:
  - ✅ Discord
  - ✅ Slack
  - ✅ Microsoft Teams
- Prevents duplicate posts using a local tracking file

## 🚀 Features

- ✅ Detects newest video from a YouTube channel
- ✅ Posts only **once per video** (no duplicates)
- ✅ Saves last video ID locally
- ✅ Multi-platform support:

### 💬 Discord
- Clickable title  
- Thumbnail preview  
- Rich embed formatting  

### 💼 Slack
- Bold title  
- Clickable link  
- Thumbnail image  
- Structured layout (Block Kit)  

### 🏢 Microsoft Teams
- Card-based messages  
- Title + link  
- Thumbnail image  
- Clean structured layout  

- ✅ Lightweight (no external dependencies)

## 📸 Example Output

When a new video is uploaded:

- ✅ Title appears as clickable link  
- ✅ Thumbnail is displayed  
- ✅ Message is posted automatically to your platform of choice  

## ⚡ Quick Start

1. Add your API key  
2. Add your webhook URL (Discord / Slack / Teams)  
3. Run the script  

powershell.exe -ExecutionPolicy Bypass -File youtube.ps1

## ⚙️ Requirements

- Windows PowerShell (or PowerShell Core)  
- YouTube Data API v3 key  
- Webhook URL for:
  - Discord OR
  - Slack OR
  - Microsoft Teams  

## 🔑 Setup Instructions

### 1. Get a YouTube API Key

1. Go to the Google Cloud Console  
2. Create a new project  
3. Enable YouTube Data API v3  
4. Create API credentials → copy your API key  

### 2. Get YouTube Channel ID

- Go to the channel page  
- Open the About section  
- Find the channel ID  

Example:  
UC-Fm2Ezn2Avm97IY3vMpKwA

## 🔗 Webhook Setup

### 💬 Discord

1. Open Discord channel settings  
2. Go to Integrations → Webhooks  
3. Click Create Webhook  
4. Copy the webhook URL  

### 💼 Slack

1. Go to https://api.slack.com/apps  
2. Create a new app  
3. Enable Incoming Webhooks  
4. Add webhook to a channel  
5. Copy the webhook URL  

### 🏢 Microsoft Teams

1. Open your Teams channel  
2. Click ... → Connectors / Workflows  
3. Add Incoming Webhook  
4. Copy the webhook URL

## 🔧 Configure the Script

Recommended folder:
```
C:\scripts\youtube_bot\
```
Edit variables:
```powershell
$apiKey = "YOUR_API_KEY"  
$channelId = "YOUR_CHANNEL_ID"  
$webhookUrl = "YOUR_WEBHOOK_URL"  
```
## ▶️ Running the Script
```powershell
powershell.exe -ExecutionPolicy Bypass -File youtube.ps1  
```
## 🔁 Automate (Recommended)

Use Windows Task Scheduler:

Program:  
powershell.exe  

Arguments:  
-ExecutionPolicy Bypass -File C:\Path\youtube.ps1  

Start in:  
C:\Path\To\Script  

## 📁 How It Works

1. Fetch latest video via YouTube API  
2. Compare with last stored ID (last_video.txt)  
3. If new:
   - Send message  
   - Save ID  
4. If same:
   - Do nothing  

---

## 🗂️ File Storage

Creates:

last_video.txt

Stores last video ID to prevent duplicates.

---

## ✅ Script
```powershell
$apiKey = "Your_Google_API_goes_here"
$channelId = "YouTube_Channel_ID_goes_here"

$webhookUrl = "Your_Webhook_goes_here"

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
    Invoke-RestMethod -Uri $webhookUrl -Method POST
}
```
## ⚠️ Notes

- First run will initialize only (no posting)  
- Ensure API quota is sufficient  
- Make sure webhook URL is valid  
- Teams and Slack formatting differ from Discord  
