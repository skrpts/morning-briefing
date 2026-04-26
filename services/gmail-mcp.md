---
type: service
id: gmail-mcp
title: Gmail MCP
description: "Gmail MCP server for reading emails, searching inbox, and managing labels"
tags: [Production, Email]
connections: []
metadata:
  provider: gmail
  protocol: mcp
  auth_type: oauth
  env_var: GMAIL_OAUTH_CREDENTIALS
  required_scopes: [gmail.readonly]
---

## Service Description

Provides access to Gmail via the Model Context Protocol (MCP). This service is used to search and read emails for the morning briefing — fetching recent messages, reading their content, and identifying which need replies.

## Configuration

### Authentication

Requires OAuth 2.0 credentials for Google. Set the `GMAIL_OAUTH_CREDENTIALS` environment variable to the path of your OAuth credentials JSON file.

**Steps to set up:**
1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a project (or use an existing one)
3. Enable the Gmail API
4. Create OAuth 2.0 credentials (Desktop application type)
5. Download the credentials JSON file
6. Set `GMAIL_OAUTH_CREDENTIALS` to the file path

On first run, the MCP server will open a browser window for you to authorise access to your Gmail account.

### MCP Server Setup

```json
{
  "mcpServers": {
    "gmail": {
      "command": "npx",
      "args": ["-y", "gmail-mcp-server"],
      "env": {
        "GMAIL_OAUTH_CREDENTIALS": "{GMAIL_OAUTH_CREDENTIALS}"
      }
    }
  }
}
```

## Capabilities Used

### Reading

- `search_emails` — search emails using Gmail query syntax (e.g. `newer_than:12h`, `in:inbox is:unread`, `from:jane@example.com`). Parameters: `query` (string), `maxResults` (number).
- `read_email` — retrieve the full content of a specific email by message ID. Parameters: `messageId` (string).
- `list_email_labels` — list all available Gmail labels for filtering.

### Not Used by This Skrpt

- `draft_email` — this is a read-only briefing; no drafts are created
- `send_email` — not used
- `modify_email` — not used

## Rate Limiting

Gmail API allows 250 quota units per user per second. `search_emails` costs 5 units, `read_email` costs 5 units. A typical morning briefing consumes 50–150 units depending on email volume.

## Privacy Considerations

Email content, sender names, and subject lines are sent to your configured LLM provider for categorisation and summarisation. Emails may contain PII, confidential information, and sensitive attachments. The `data_handling: pii` declaration in the manifest makes this explicit during import. Ensure your organisation's policies permit sending email content to third-party AI services.
