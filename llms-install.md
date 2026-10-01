# Installing the Switchboard Finance MCP server

This is a hosted remote server. Nothing to install, no API key, no sign-in.

- Transport: Streamable HTTP
- URL: `https://api.switchboardfinance.com.au/mcp`

Add it to the MCP settings file as a remote server:

```json
{
  "mcpServers": {
    "switchboard-finance": {
      "type": "streamableHttp",
      "url": "https://api.switchboardfinance.com.au/mcp"
    }
  }
}
```

(For clients that use `"type": "http"`, use that instead.)

Check it works by calling `list_products` with no arguments: it returns 11 Australian business finance types.

`request_callback` sends a real enquiry to a licensed broker. Only call it when the user has agreed to be contacted and given their own name and mobile. For testing, use a name starting with "Test" so no emails are sent.
