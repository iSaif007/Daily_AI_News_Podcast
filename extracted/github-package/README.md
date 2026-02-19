# 🎙️ Daily AI News Podcast Generator

An automated n8n workflow that generates a personalized daily AI news podcast in German, covering the latest developments in artificial intelligence, machine learning, and AI software engineering.

## 🌟 Features

- **Automated Daily Execution**: Runs every morning at 8:05 AM
- **Multi-Source News Gathering**: 
  - YouTube AI videos
  - RSS feeds (AI News, VentureBeat, Heise.de)
  - X/Twitter discussions
  - Web search (DuckDuckGo)
  - Direct web scraping (TechCrunch, AI News, etc.)
- **AI-Powered Script Generation**: Uses Anthropic Claude to create engaging, personalized podcast scripts
- **Text-to-Speech**: Converts scripts to audio using OpenAI TTS
- **Automatic Distribution**: 
  - Uploads to Google Drive
  - Sends email notification with link
  - Sends Telegram message with link
- **Personalized Content**: Tailored for Software Engineers and AI Project Managers

## 📋 Prerequisites

### Required Accounts & API Keys

1. **n8n Account** (cloud or self-hosted)
2. **Anthropic API Key** (for Claude)
   - Get it at: https://console.anthropic.com/
3. **OpenAI API Key** (for Text-to-Speech)
   - Get it at: https://platform.openai.com/api-keys
4. **Google Cloud Project** (for Google Drive)
   - Enable Google Drive API
   - Create OAuth 2.0 credentials
5. **Gmail Account** (for sending emails)
6. **Telegram Bot** (for notifications)
   - Create bot via @BotFather
   - Get your Chat ID via @userinfobot
7. **Optional: SerpAPI Key** (for enhanced search, has free tier)
   - Get it at: https://serpapi.com/

## 🚀 Setup Instructions

### 1. Import Workflow

1. Download `Daily_AI_News_Podcast_CLEANED.json`
2. In n8n: Click on workflow menu → Import from File
3. Select the downloaded file

### 2. Configure Credentials

#### Anthropic API
1. Click on "Anthropic Chat Model" nodes
2. Click "Create New Credential"
3. Enter your Anthropic API key

#### OpenAI API
1. Click on "Generate Podcast Audio" node
2. In Authentication, select "Generic Credential Type"
3. Choose "OpenAI Api"
4. Enter your OpenAI API key

#### Google Drive
1. Click on "Upload file" node
2. Click "Create New Credential"
3. Follow OAuth 2.0 setup:
   - Go to Google Cloud Console
   - Create OAuth credentials
   - Add authorized redirect URI: `https://your-n8n-instance.com/rest/oauth2-credential/callback`
   - Enter Client ID and Client Secret
   - Connect your account

#### Gmail
1. Click on "Send Gmail" node
2. Click "Create New Credential"
3. Follow Gmail OAuth setup (similar to Google Drive)

#### Telegram
1. Click on "Send Telegram Message" node
2. Click "Create New Credential"
3. Enter your Bot Token
4. Update `chatId` parameter with your Chat ID

### 3. Configure Parameters

#### Workflow Configuration Node
- Set `podcastDurationMinutes` to desired length (default: 19)
- Search query is auto-generated based on current date

#### Get News Node (Direct Search)
- Optional: Add or remove news sources
- Adjust number of articles per source (currently 2 per source)

#### Podcast Script Generator
- **Personalization**: Change "Saif" to your name in:
  - System Message (line with "Morgen Saif!")
  - User Message greeting
- **Language & Tone**: Adjust formality level if desired
- **Topics**: Modify focus areas (currently: 40% AI Tech, 40% Software Engineering, 20% Project Management)

#### Send Gmail Node
- Update recipient email address
- Customize email subject/body if desired

### 4. Activate Workflow

1. Toggle the "Active" switch in the top-right corner
2. The workflow will now run automatically every day at 8:05 AM

## 🏗️ Workflow Architecture

```
Daily Trigger (8:05 AM)
    ↓
Workflow Configuration (sets date, duration)
    ↓
Direct Search (multi-source news gathering)
    ↓
AI Research Agent (optional: uses memory + tools)
    ↓
Podcast Script Generator (Claude creates German script)
    ↓
Generate Podcast Audio (OpenAI TTS)
    ↓
Upload to Google Drive
    ↓
Process Audio Response (extract link)
    ↓
Send Email + Telegram Notification
```

## 🎯 Customization Guide

### Change Voice
In "Generate Podcast Audio" node, modify `voice` parameter:
- `nova` - Female, warm (default)
- `alloy` - Neutral
- `echo` - Male
- `shimmer` - Female, clear

### Change Podcast Length
In "Workflow Configuration" node:
- Adjust `podcastDurationMinutes`
- Update word count in Podcast Script Generator (currently 2500-3000 words ≈ 20 min)

### Add News Sources
In "Direct Search" node, add to the `sources` array:
```javascript
{
  url: 'https://your-news-site.com',
  name: 'Site Name',
  titleRegex: /<your-regex>/g
}
```

### Change Language
- Update all prompts in "Podcast Script Generator" to your language
- Update `toLocaleDateString` locale parameter
- Update OpenAI TTS voice to match language

## 📊 Cost Estimation

Approximate costs per podcast (20 minutes):

- **Anthropic Claude API**: ~$0.15 (for script generation)
- **OpenAI TTS**: ~$0.30 (for 3000 words)
- **SerpAPI**: Free tier available (100 searches/month)
- **Google Drive/Gmail**: Free
- **Telegram**: Free

**Total: ~$0.45 per podcast or ~$13.50/month for daily podcasts**

## 🐛 Troubleshooting

### Workflow doesn't trigger automatically
- Check if workflow is "Active" (green toggle)
- Verify timezone in "Daily Trigger" node
- Check n8n execution logs

### Audio generation fails
- Verify OpenAI API key is valid
- Check if you have sufficient OpenAI credits
- Reduce text length if hitting limits

### No news found
- Check internet connectivity of n8n instance
- Verify news site structures haven't changed (update regex patterns)
- Check console logs in "Direct Search" node

### Wrong date in podcast
- Verify timezone in "Workflow Configuration"
- Check `$now` expressions use correct timezone
- Ensure server time is accurate

## 🔒 Security Notes

- Never commit API keys to public repositories
- Use n8n's credential system (encrypted storage)
- Restrict Google OAuth scopes to minimum required
- Regularly rotate API keys
- Review n8n instance security settings

## 📝 License

MIT License - feel free to modify and use for your own projects!

## 🤝 Contributing

Contributions welcome! Areas for improvement:
- Additional news sources
- Better deduplication logic
- Multi-language support
- Enhanced error handling
- Alternative TTS providers
- RSS feed optimization

## 📧 Support

For issues or questions:
- Open an issue on GitHub
- Check n8n community forums
- Review n8n documentation

## 🎉 Acknowledgments

- Built with [n8n](https://n8n.io/)
- Powered by [Anthropic Claude](https://www.anthropic.com/)
- Audio by [OpenAI TTS](https://platform.openai.com/docs/guides/text-to-speech)

---

**Happy podcasting!** 🎙️🚀
