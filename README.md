🎭 Hebrew Storyteller - n8n Workflow

AI-powered personalized Hebrew storytelling for children ages 3-5. Creates custom stories, converts them to speech, and delivers interactive HTML audio players via email.

✨ Features

🎯 Personalized Stories - Custom Hebrew stories based on child's name, age, and theme
🗣️ Text-to-Speech - Converts stories to Hebrew audio using Google TTS
🎵 Complete Audio Experience - Intro music + story + outro music
📱 Interactive HTML Player - Beautiful Hebrew RTL interface with progress tracking
📧 Automated Delivery - Emails parents a shareable HTML audio player
✅ Input Validation - Ensures proper data before processing

🔧 How It Works

Webhook receives child details (name, age, theme, parent email)
Validates input (age 3-5, valid email, required fields)
AI generates personalized Hebrew bedtime story using OpenAI
Converts to speech using Google Text-to-Speech (Hebrew voice)
Creates HTML player with embedded audio and Hebrew interface
Uploads to Google Drive and sends download link via Gmail

🚀 Quick Start
Prerequisites

n8n instance (cloud or self-hosted)
OpenAI API key
Google Cloud account with TTS API enabled
Google Service Account with Drive & Gmail access
Gmail account for sending emails

Setup

Import the workflow:


Configure credentials in n8n:

OpenAI API credentials
Google Service Account credentials
Gmail OAuth2 credentials


Update placeholders:

Add your intro/outro music as base64 in "Edit Fields" node
Set your Google Drive folder ID
Configure your Google TTS API key


Test the webhook:
json{
  "child_name": "יעל",
  "age": 4,
  "story_theme": "חיות הג'ונגל",
  "parent_email": "parent@example.com"
}


📋 API Reference
Webhook Endpoint
POST /webhook/hebrew-story
Request Body
json{
  "child_name": "string (required) - Child's name in Hebrew",
  "age": "number (required) - Age between 3-5",
  "story_theme": "string (required) - Story theme/topic",
  "parent_email": "string (required) - Valid email address"
}
Response

Creates personalized story
Sends HTML audio player via email
Returns success/error status

🎨 Sample Output
The workflow generates:

Hebrew bedtime story (300-400 words)
Interactive HTML player with Hebrew RTL layout
Email with embedded player sent to parents
Google Drive hosted file for easy sharing

🔧 Customization
Story Templates
Modify the OpenAI prompt in "Message a model" node to change:

Story length
Writing style
Educational themes
Character types

Audio Settings
Configure Google TTS parameters:

Voice type (male/female)
Speaking rate
Pitch
Audio quality

Email Design
Customize the HTML email template in "Send a message" node.
📱 Mobile Support
The generated HTML player is fully responsive and works great on:

iOS Safari
Android Chrome
Mobile browsers with audio support

🛠️ Troubleshooting
Common Issues
"Could not find story audio"

Check Google TTS API configuration
Verify service account permissions

"Missing audio data"

Ensure intro/outro base64 audio is added to "Edit Fields" node

Email not sending

Verify Gmail OAuth2 credentials
Check Gmail API permissions

Debug Mode
Enable debug logging in the "Prepare Audio Data" node to troubleshoot audio processing.
