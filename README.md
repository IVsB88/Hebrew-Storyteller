# Hebrew Storyteller - n8n Workflow

AI-powered personalized Hebrew storytelling for children ages 3-5. Creates custom stories, converts them to speech, and delivers interactive HTML audio players via email.

## Features

- Personalized Hebrew stories based on child's name, age, and theme
- Text-to-speech conversion using Google TTS with Hebrew voice
- Interactive HTML audio player with intro/story/outro sequence
- Automated email delivery to parents
- Input validation for data quality

## How It Works

1. Webhook receives child details (name, age, theme, parent email)
2. Validates input data (age 3-5, valid email, required fields)
3. AI generates personalized Hebrew bedtime story using OpenAI
4. Converts story to Hebrew speech using Google Text-to-Speech
5. Creates HTML player with embedded audio and Hebrew RTL interface
6. Uploads to Google Drive and emails download link to parents

## Prerequisites

- n8n instance (cloud or self-hosted)
- OpenAI API key
- Google Cloud account with Text-to-Speech API enabled
- Google Service Account with Drive and Gmail access
- Gmail account for sending emails

## Setup

### Import Workflow
Download `workflow.json` and import it into your n8n instance via Settings → Import from File.

### Configure Credentials
Set up these credentials in n8n:
- **OpenAI API** - Your OpenAI API key
- **Google Service Account** - JSON key file with TTS, Drive, and Gmail permissions
- **Gmail OAuth2** - OAuth credentials for sending emails

### Configure Audio Files
1. Convert intro and outro music files to base64:
   ```bash
   base64 -i intro.mp3 > intro_base64.txt
   base64 -i outro.mp3 > outro_base64.txt
   ```
2. Paste the base64 strings into the "Edit Fields" node

### Set Up Google Services
1. **Google Drive**: Create a folder and copy its ID from the URL
2. **Text-to-Speech API**: Enable the API and get your API key
3. Update the workflow nodes with your folder ID and API key

### Test the Workflow
Send a POST request to your webhook URL:

```json
{
  "child_name": "יעל",
  "age": 4,
  "story_theme": "חיות הג'ונגל",
  "parent_email": "parent@example.com"
}
```

## API Reference

**Endpoint**: `POST /webhook/hebrew-story`

**Request Body**:
```json
{
  "child_name": "string (Hebrew name)",
  "age": "number (3-5)",
  "story_theme": "string (story topic)",
  "parent_email": "string (valid email)"
}
```

**Output**: Personalized story audio player sent via email

## Customization

### Story Content
Modify the OpenAI prompt in the "Message a model" node to adjust:
- Story length and complexity
- Writing style and themes
- Character types and scenarios

### Audio Settings
Configure Google TTS parameters in the "HTTP Request" node:
- Voice type (he-IL-Standard-A/B/C/D)
- Speaking rate (0.25-4.0)
- Pitch adjustment (-20 to 20)

### Email Template
Customize the HTML email design in the "Send a message" node.

## Troubleshooting

**Audio processing errors**: Check Google TTS API configuration and service account permissions

**Missing audio data**: Ensure intro/outro base64 audio is properly added to "Edit Fields" node

**Email delivery issues**: Verify Gmail OAuth2 credentials and API permissions

**Workflow execution fails**: Enable debug mode in "Prepare Audio Data" node for detailed logging
