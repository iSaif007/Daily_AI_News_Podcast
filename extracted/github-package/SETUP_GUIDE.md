# 🚀 Quick Setup Guide

Follow these steps to get your AI News Podcast up and running in ~15 minutes.

## Step 1: Get Your API Keys (10 minutes)

### 1.1 Anthropic API Key
1. Go to https://console.anthropic.com/
2. Sign up / Log in
3. Navigate to "API Keys"
4. Click "Create Key"
5. Copy your key (starts with `sk-ant-...`)

### 1.2 OpenAI API Key
1. Go to https://platform.openai.com/
2. Sign up / Log in
3. Navigate to "API Keys"
4. Click "Create new secret key"
5. Copy your key (starts with `sk-...`)
6. **Important**: Add $5-10 credit to your account

### 1.3 Telegram Bot
1. Open Telegram
2. Search for `@BotFather`
3. Send `/newbot`
4. Follow instructions to create bot
5. Copy your bot token

**Get Your Chat ID:**
1. Search for `@userinfobot` in Telegram
2. Start the bot
3. It will show your Chat ID (a number like `1234567890`)

### 1.4 Google Cloud Setup
1. Go to https://console.cloud.google.com/
2. Create a new project (e.g., "AI-Podcast")
3. Enable APIs:
   - Google Drive API
   - Gmail API
4. Go to "Credentials" → "Create Credentials" → "OAuth 2.0 Client ID"
5. Application type: Web application
6. Add authorized redirect URI: `https://YOUR-N8N-INSTANCE/rest/oauth2-credential/callback`
7. Copy Client ID and Client Secret

## Step 2: Import to n8n (2 minutes)

1. Open n8n
2. Click workflow menu (top left)
3. Click "Import from File"
4. Select `Daily_AI_News_Podcast_CLEANED.json`
5. Workflow is imported!

## Step 3: Configure Credentials (3 minutes)

### 3.1 Anthropic Credential
1. Click on any "Anthropic Chat Model" node
2. In "Credentials", click "Create New Credential"
3. Paste your Anthropic API key
4. Click "Save"

### 3.2 OpenAI Credential  
1. Click on "Generate Podcast Audio" node
2. In "Authentication", select "Predefined Credential Type"
3. Choose "OpenAI API"
4. Click "Create New Credential"
5. Paste your OpenAI API key
6. Click "Save"

### 3.3 Google Drive & Gmail
1. Click on "Upload file" node
2. Click "Create New Credential"
3. Select "OAuth2"
4. Enter Client ID and Client Secret from Step 1.4
5. Click "Sign in with Google"
6. Allow access
7. Repeat for "Send Gmail" node

### 3.4 Telegram
1. Click on "Send Telegram Message" node
2. Click "Create New Credential"
3. Paste Bot Token
4. Click "Save"
5. In node parameters, update `chatId` field with your Chat ID

## Step 4: Personalize (1 minute)

### 4.1 Change Name
1. Click on "Podcast Script Generator" node
2. In System Message, change "Saif" to your name
3. In User Message, change "Morgen Saif" to "Morgen [YOUR NAME]"

### 4.2 Update Email
1. Click on "Send Gmail" node
2. Update "To" field with your email address

## Step 5: Test! (2 minutes)

1. Click "Execute Workflow" button (top)
2. Wait 2-3 minutes
3. Check output of each node
4. Look for:
   - ✅ News collected
   - ✅ Script generated
   - ✅ Audio created
   - ✅ Uploaded to Drive
   - ✅ Email/Telegram sent

## Step 6: Activate (30 seconds)

1. Toggle "Active" switch (top right)
2. Workflow will now run automatically every day at 8:05 AM!

---

## ⚠️ Common Issues

### "No news found"
- Wait a few seconds and try again
- Some websites may temporarily block requests
- Check console logs in "Direct Search" node

### "API Key invalid"
- Double-check you copied the entire key
- Verify key is for correct service (OpenAI vs Anthropic)
- Check if API key is active

### "Google authentication failed"
- Make sure redirect URI is exactly correct
- Check if APIs are enabled in Google Cloud
- Try creating new OAuth credentials

### "Audio too short"
- Check if script generation worked
- Increase word count in Podcast Script Generator
- Check OpenAI API credits

---

## 🎉 Success!

You should now have:
- ✅ Automated daily AI news podcast
- ✅ Delivered to email and Telegram
- ✅ Stored in Google Drive
- ✅ Personalized to your interests

**Enjoy your daily AI news!** 🎙️

Need help? Check README.md or open an issue on GitHub.
