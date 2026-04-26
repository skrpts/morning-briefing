---
type: service
id: google-calendar-mcp
title: Google Calendar MCP
description: "Google Calendar MCP server for reading events, checking availability, and viewing schedules"
tags: [Production, Calendar]
connections: []
metadata:
  provider: google-calendar
  protocol: mcp
  auth_type: oauth
  env_var: GOOGLE_OAUTH_CREDENTIALS
  required_scopes: [calendar.readonly]
---

## Service Description

Provides access to Google Calendar via the Model Context Protocol (MCP). This service is used to fetch today's events, check meeting details, and understand the day's schedule for the morning briefing.

## Configuration

### Authentication

Requires OAuth 2.0 credentials for Google. Set the `GOOGLE_OAUTH_CREDENTIALS` environment variable to the path of your OAuth credentials JSON file.

**Steps to set up:**
1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a project (or use the same one as Gmail)
3. Enable the Google Calendar API
4. Create OAuth 2.0 credentials (Desktop application type) or reuse your Gmail credentials
5. Download the credentials JSON file
6. Set `GOOGLE_OAUTH_CREDENTIALS` to the file path

On first run, the MCP server will open a browser window for you to authorise access to your calendar.

### MCP Server Setup

```json
{
  "mcpServers": {
    "google-calendar": {
      "command": "npx",
      "args": ["-y", "google-calendar-mcp"],
      "env": {
        "GOOGLE_OAUTH_CREDENTIALS": "{GOOGLE_OAUTH_CREDENTIALS}"
      }
    }
  }
}
```

## Capabilities Used

### Reading

- `list-events` — list events within a date range. Used to fetch today's schedule.
- `get-event` — get detailed information for a specific event by ID, including attendees, description, and location.
- `get-current-time` — get the current date and time in the calendar's timezone.
- `list-calendars` — list all available calendars (for multi-calendar setups).

### Not Used by This Skrpt

- `create-event` — this is a read-only briefing; no events are created
- `update-event` — not used
- `delete-event` — not used
- `search-events` — not used (list-events with date filtering is sufficient)

## Rate Limiting

Google Calendar API allows 1,000,000 queries per day. The morning briefing typically consumes 5–15 requests. Rate limiting is not a concern for this use case.

## Privacy Considerations

Event titles, attendee names, descriptions, and locations are sent to your configured LLM provider. Calendar data may contain sensitive meeting details. Ensure your organisation's policies permit sending calendar data to third-party AI services.
