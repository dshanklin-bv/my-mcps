# My MCP Servers

Documentation of Model Context Protocol (MCP) servers I use with Claude and other AI assistants.

## Table of Contents

- [Google Workspace MCP](#google-workspace-mcp)

---

## Google Workspace MCP

**Repository:** https://github.com/taylorwilsdon/google_workspace_mcp

### Description

A production-ready MCP server providing natural language control over Google Workspace services. Integrates Gmail, Google Calendar, Docs, Sheets, Slides, Chat, Forms, Tasks, Search, and Drive with AI assistants.

### Features

- **Gmail** - Complete email management
- **Calendar** - Full calendar management with advanced features
- **Drive** - File operations with Office format support
- **Docs** - Document creation, editing, and comments
- **Sheets** - Spreadsheet operations
- **Slides** - Presentation operations
- **Forms** - Form creation and response management
- **Chat** - Space management and messaging
- **Tasks** - Task and task list management with hierarchy
- **Search** - Programmable Search Engine integration

### Technical Highlights

- OAuth 2.0 and OAuth 2.1 support
- Automatic token refresh and session management
- Multi-user bearer token authentication
- Three progressive tool tiers (core, extended, complete)

### Prerequisites

- Python 3.10+
- `uvx` or `uv`
- Google Cloud Project with OAuth 2.0 credentials

### Environment Variables

```bash
GOOGLE_OAUTH_CLIENT_ID=your_client_id
GOOGLE_OAUTH_CLIENT_SECRET=your_client_secret
OAUTHLIB_INSECURE_TRANSPORT=1  # development only
```

### Optional Variables

- `USER_GOOGLE_EMAIL` - Default email for single-user auth
- `GOOGLE_PSE_API_KEY` & `GOOGLE_PSE_ENGINE_ID` - Custom Search setup
- `MCP_ENABLE_OAUTH21=true` - OAuth 2.1 support

### Google Cloud Setup

Enable the following APIs in your Google Cloud Project:
- Calendar API
- Drive API
- Gmail API
- Docs API
- Sheets API
- Slides API
- Forms API
- Tasks API
- Chat API
- Custom Search API

Create OAuth 2.0 Desktop Application credentials.

### Launch

```bash
uv run main.py --tool-tier core
```

### Installation (Claude Desktop)

1. Download the latest `google_workspace_mcp.dxt` from releases
2. Double-click to install
3. Configure credentials in Claude Desktop settings under Extensions
