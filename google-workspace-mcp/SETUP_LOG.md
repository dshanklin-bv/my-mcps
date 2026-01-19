# Google Workspace MCP - Setup Log

**Date:** 2026-01-18
**Assisted by:** Claude Code + Perplexity Comet

---

## What Was Done

### 1. Created Repository
- Created GitHub repo `dshanklin-bv/my-mcps` to document MCP servers
- Cloned locally to `/Users/dshanklinbv/repos-personal/my-mcps`
- Created folder structure: `google-workspace-mcp/`

### 2. Google Cloud Setup (via Perplexity Comet)
- **Project:** rhea-ai-465103
- Created OAuth 2.0 Desktop Application credentials
- Downloaded client secret JSON to Downloads folder

### 3. APIs Enabled
All 10 required APIs enabled in Google Cloud Console:
- ✅ Gmail API (was already enabled)
- ✅ Google Calendar API
- ✅ Google Drive API
- ✅ Google Docs API
- ✅ Google Sheets API
- ✅ Google Slides API
- ✅ Google Forms API
- ✅ Google Tasks API
- ✅ Google Chat API
- ✅ Custom Search API

### 4. Credentials Stored
Created `.env` file at `/Users/dshanklinbv/repos-personal/my-mcps/google-workspace-mcp/.env`:
```
GOOGLE_OAUTH_CLIENT_ID=<stored in .env - git ignored>
GOOGLE_OAUTH_CLIENT_SECRET=<stored in .env - git ignored>
OAUTHLIB_INSECURE_TRANSPORT=1
USER_GOOGLE_EMAIL=daniel@boone.voyage
```

Also copied `client_secret.json` to the folder.

### 5. Added .gitignore
Created `.gitignore` to protect credentials from being committed:
```
.env
*.env
client_secret*.json
.credentials/
```

### 6. Configured Claude Code
Added MCP server via CLI:
```bash
claude mcp add google-workspace \
  -e GOOGLE_OAUTH_CLIENT_ID=... \
  -e GOOGLE_OAUTH_CLIENT_SECRET=... \
  -e OAUTHLIB_INSECURE_TRANSPORT=1 \
  -e USER_GOOGLE_EMAIL=daniel@boone.voyage \
  -- uvx workspace-mcp --tool-tier core
```

Config stored in: `/Users/dshanklinbv/.claude.json`

### 7. Configured Claude Desktop
Added to `~/Library/Application Support/Claude/claude_desktop_config.json`:
```json
"google-workspace": {
  "command": "uvx",
  "args": ["workspace-mcp", "--tool-tier", "core"],
  "env": {
    "GOOGLE_OAUTH_CLIENT_ID": "<your-client-id>",
    "GOOGLE_OAUTH_CLIENT_SECRET": "<your-client-secret>",
    "OAUTHLIB_INSECURE_TRANSPORT": "1",
    "USER_GOOGLE_EMAIL": "daniel@boone.voyage"
  }
}
```

---

## Why

### Why Google Workspace MCP?
- Natural language control over Google Workspace services
- Integrates Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks, Chat, Search
- Works with Claude Code and Claude Desktop
- Production-ready with OAuth 2.0/2.1 support

### Why `--tool-tier core`?
- Minimal API quota usage for initial setup
- Essential tools only (search, read, create, basic modify)
- Can upgrade to `extended` or `complete` later if needed

### Why Desktop OAuth client type?
- Simplified setup - no redirect URIs needed
- Works in both stdio and HTTP modes
- Handles authentication flow automatically

### Why separate .env file?
- Keeps credentials out of git
- Single source of truth for credentials
- Easy to reference or source when needed

---

## Next Steps

1. **Restart Claude Code** - Start new session to activate MCP
2. **Restart Claude Desktop** - Quit and reopen app
3. **First use** - Call any Google tool (e.g., "list my calendars")
4. **OAuth flow** - Authorize when prompted with Google OAuth URL
5. **Optional** - Upgrade to `--tool-tier extended` for more features

---

## File Locations

| File | Path |
|------|------|
| Setup guide | `/Users/dshanklinbv/repos-personal/my-mcps/google-workspace-mcp/SETUP.md` |
| Credentials (.env) | `/Users/dshanklinbv/repos-personal/my-mcps/google-workspace-mcp/.env` |
| Client secret JSON | `/Users/dshanklinbv/repos-personal/my-mcps/google-workspace-mcp/client_secret.json` |
| Claude Code config | `/Users/dshanklinbv/.claude.json` |
| Claude Desktop config | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| This log | `/Users/dshanklinbv/repos-personal/my-mcps/google-workspace-mcp/SETUP_LOG.md` |

---

## References

- **MCP Repository:** https://github.com/taylorwilsdon/google_workspace_mcp
- **PyPI Package:** https://pypi.org/project/workspace-mcp/
- **Google Cloud Console:** https://console.cloud.google.com/
- **Project:** rhea-ai-465103
