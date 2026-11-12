# Eversports Studio Manager MCP server for ChatGPT and Claude

Connect Eversports Studio Manager to ChatGPT, Claude and other AI agents through Cotlet. Work with studio activities, participants, memberships and invoices in your own signed-in account. Cotlet is independent and not affiliated with Eversports Studio Manager. If Eversports Studio Manager offers an official API for your needs, we recommend it.

## What you can ask

> Show today’s studio activities and their sign-in lists.

> Pause the membership I name for the dates I provide. Ask me before saving.

> Email the invoice I select to its customer. Ask me before sending.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev. Follow the steps in your Cotlet console.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Eversports Studio Manager tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"eversports-studio-manager": {"command": "python3", "args": ["/absolute/path/to/eversports-studio-manager-mcp/eversports_studio_manager_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t eversports-studio-manager-mcp .
docker run -i --rm -e COTLET_API_KEY eversports-studio-manager-mcp
```

Tools: `eversports_studio_manager_guide`, `eversports_studio_manager_status`, `eversports_studio_manager_open`, `eversports_studio_manager_read`, `eversports_studio_manager_click`, `eversports_studio_manager_type`, `eversports_studio_manager_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 eversports_studio_manager_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 eversports_studio_manager_agent.py status    # is Eversports Studio Manager ready in your Cotlet.dev account
python3 eversports_studio_manager_agent.py guide     # Eversports Studio Manager screens and sign-in link
python3 eversports_studio_manager_agent.py read      # open Eversports Studio Manager, read the page, close the browser
python3 eversports_studio_manager_agent.py tools     # list Cotlet.dev tools
python3 eversports_studio_manager_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Eversports Studio Manager users

**How do I connect Eversports Studio Manager to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to Eversports Studio Manager once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your Eversports Studio Manager account through Cotlet, in their phone apps too.

**Can ChatGPT sign in participants in Eversports Studio Manager?**

ChatGPT opens the activity's Sign-in and signs in the customers you list after you approve it, so the booking is deducted from their card or membership.

**Can ChatGPT pause a membership in Eversports Studio Manager?**

ChatGPT adds or removes the membership rest period you give it on the customer's membership after you approve the change.

**Can ChatGPT email an invoice in Eversports Studio Manager?**

ChatGPT opens the class or membership invoice in Financials and emails it to the customer after you approve the send.

**Is Cotlet affiliated with Eversports Studio Manager?**

No. Cotlet is independent and not affiliated with Eversports Studio Manager.

## Find it on

- [Eversports Studio Manager on Cotlet](https://cotlet.dev/integrations/eversports-studio-manager-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/eversports-studio-manager-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=eversports-studio-manager

Request access: https://cotlet.dev/signup?app=eversports-studio-manager&utm_source=github&utm_medium=readme&utm_campaign=eversports-studio-manager
