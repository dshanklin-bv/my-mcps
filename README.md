# My MCP Servers

Documentation of Model Context Protocol (MCP) servers I use with Claude and other AI assistants.

## MCP Servers

| MCP | Description | Setup |
|-----|-------------|-------|
| [Google Workspace](./google-workspace-mcp/) | Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks, Chat, Search | [SETUP.md](./google-workspace-mcp/SETUP.md) |

---

## Google Workspace MCP

**Repository:** https://github.com/taylorwilsdon/google_workspace_mcp

A production-ready MCP server providing natural language control over Google Workspace services.

### Services

- **Gmail** - Email management
- **Calendar** - Event management
- **Drive** - File operations
- **Docs** - Document editing
- **Sheets** - Spreadsheet operations
- **Slides** - Presentation management
- **Forms** - Form creation & responses
- **Tasks** - Task management
- **Chat** - Space messaging
- **Search** - Custom search

### Quick Start

```bash
uvx workspace-mcp --tool-tier core
```

**[Full Setup Guide →](./google-workspace-mcp/SETUP.md)**
