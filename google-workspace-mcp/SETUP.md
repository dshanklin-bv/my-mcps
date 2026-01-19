# Google Workspace MCP - Setup Guide

**Repository:** https://github.com/taylorwilsdon/google_workspace_mcp

## Overview

MCP server providing natural language control over Google Workspace services: Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks, Chat, and Search.

---

## Setup Steps

### Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select existing)
3. Note your project name

### Step 2: Create OAuth 2.0 Credentials

1. Navigate to **APIs & Services → Credentials**
2. Click **Create Credentials → OAuth Client ID**
3. Choose **Desktop Application** as the application type
4. Download credentials and note:
   - Client ID
   - Client Secret

### Step 3: Enable Required APIs

Enable each API in **APIs & Services → Library**, or use these quick links:

- [Google Calendar API](https://console.cloud.google.com/flows/enableapi?apiid=calendar-json.googleapis.com)
- [Google Drive API](https://console.cloud.google.com/flows/enableapi?apiid=drive.googleapis.com)
- [Gmail API](https://console.cloud.google.com/flows/enableapi?apiid=gmail.googleapis.com)
- [Google Docs API](https://console.cloud.google.com/flows/enableapi?apiid=docs.googleapis.com)
- [Google Sheets API](https://console.cloud.google.com/flows/enableapi?apiid=sheets.googleapis.com)
- [Google Slides API](https://console.cloud.google.com/flows/enableapi?apiid=slides.googleapis.com)
- [Google Forms API](https://console.cloud.google.com/flows/enableapi?apiid=forms.googleapis.com)
- [Google Tasks API](https://console.cloud.google.com/flows/enableapi?apiid=tasks.googleapis.com)
- [Google Chat API](https://console.cloud.google.com/flows/enableapi?apiid=chat.googleapis.com)
- [Custom Search API](https://console.cloud.google.com/flows/enableapi?apiid=customsearch.googleapis.com)

### Step 4: Configure Environment Variables

```bash
export GOOGLE_OAUTH_CLIENT_ID="your-client-id"
export GOOGLE_OAUTH_CLIENT_SECRET="your-client-secret"
export OAUTHLIB_INSECURE_TRANSPORT=1  # Development only
```

**Optional variables:**
```bash
export USER_GOOGLE_EMAIL="your.email@gmail.com"  # Default email for single-user auth
export GOOGLE_PSE_API_KEY="xxx"                   # For Custom Search
export GOOGLE_PSE_ENGINE_ID="yyy"                 # For Custom Search
export MCP_ENABLE_OAUTH21="true"                  # OAuth 2.1 support
```

### Step 5: Install & Run

**Option A: Quick Start with uvx (Recommended)**
```bash
uvx workspace-mcp --tool-tier core
```

**Option B: Claude Desktop DXT Extension**
1. Download `google_workspace_mcp.dxt` from [Releases](https://github.com/taylorwilsdon/google_workspace_mcp/releases)
2. Double-click to install
3. Configure credentials in Claude Desktop → Settings → Extensions → Google Workspace MCP

**Option C: Manual Claude Desktop Config**

Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "google_workspace": {
      "command": "uvx",
      "args": ["workspace-mcp"],
      "env": {
        "GOOGLE_OAUTH_CLIENT_ID": "your-client-id",
        "GOOGLE_OAUTH_CLIENT_SECRET": "your-secret",
        "OAUTHLIB_INSECURE_TRANSPORT": "1"
      }
    }
  }
}
```

**Option D: Claude Code**
```bash
claude mcp add --transport http workspace-mcp http://localhost:8000/mcp
```

---

## Tool Tiers

| Tier | Description | Use Case |
|------|-------------|----------|
| `core` | Essential tools only | Light usage, minimal API quotas |
| `extended` | Core + management tools | Regular usage |
| `complete` | All available tools | Power users |

```bash
uvx workspace-mcp --tool-tier core      # Start small
uvx workspace-mcp --tool-tier extended  # More features
uvx workspace-mcp --tool-tier complete  # Everything
```

---

## First-Time Authentication

1. Call any tool
2. Server returns authorization URL
3. Open URL in browser and authorize
4. Google provides authorization code
5. Paste code when prompted (or handled automatically)
6. Server completes authentication

---

## Available Services & Tools

### Gmail
- `search_gmail_messages` - Search with Gmail operators
- `get_gmail_message_content` - Retrieve message content
- `send_gmail_message` - Send emails
- `draft_gmail_message` - Create drafts
- `modify_gmail_message_labels` - Modify labels

### Calendar
- `list_calendars` - List accessible calendars
- `get_events` - Retrieve events with time filtering
- `create_event` - Create events with attachments & reminders
- `modify_event` - Update events
- `delete_event` - Remove events

### Drive
- `search_drive_files` - Search files
- `get_drive_file_content` - Read file content
- `create_drive_file` - Create files
- `share_drive_file` - Share with users/groups

### Docs
- `get_doc_content` - Extract document text
- `create_doc` - Create new documents
- `modify_doc_text` - Modify document text
- `find_and_replace_doc` - Find and replace

### Sheets
- `read_sheet_values` - Read cell ranges
- `modify_sheet_values` - Write/update cells
- `create_spreadsheet` - Create new spreadsheets

### Slides
- `create_presentation` - Create presentations
- `get_presentation` - Retrieve details
- `batch_update_presentation` - Apply updates

### Forms
- `create_form` - Create new forms
- `get_form` - Retrieve form details
- `list_form_responses` - List responses

### Tasks
- `list_tasks` - List tasks with filtering
- `create_task` - Create tasks with hierarchy
- `update_task` - Modify task properties

### Chat
- `list_spaces` - List chat spaces
- `get_messages` - Retrieve messages
- `send_message` - Send messages

### Search
- `search_custom` - Perform web searches (requires PSE setup)

---

## Custom Search Setup (Optional)

1. Create Search Engine at [Programmable Search Engine](https://programmablesearchengine.google.com/controlpanel/create)
2. Get API Key from [Google Developers Console](https://console.cloud.google.com/)
3. Set environment variables:
   ```bash
   export GOOGLE_PSE_API_KEY="your-api-key"
   export GOOGLE_PSE_ENGINE_ID="your-engine-id"
   ```

---

## Troubleshooting

**Authentication issues:**
- Ensure `OAUTHLIB_INSECURE_TRANSPORT=1` is set for local development
- Check that all required APIs are enabled in Google Cloud Console
- Verify OAuth credentials are correct

**API quota exceeded:**
- Use `--tool-tier core` to reduce API usage
- Check Google Cloud Console for quota limits

---

## Links

- [GitHub Repository](https://github.com/taylorwilsdon/google_workspace_mcp)
- [PyPI Package](https://pypi.org/project/workspace-mcp/)
- [Google Cloud Console](https://console.cloud.google.com/)
- [OAuth Documentation](https://developers.google.com/workspace/guides/auth-overview)
