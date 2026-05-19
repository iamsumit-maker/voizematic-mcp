# 🎙️ voizematic-mcp

> **World's first and only AI voice agent MCP connector with features all voice ai missing.**  
> Operate your entire Voizematic voice stack directly from Claude — no dashboard, no switching tabs, no friction.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-blue.svg)](https://modelcontextprotocol.io)
[![Powered by Voizematic](https://img.shields.io/badge/Powered%20by-Voizematic.ai-purple.svg)](https://voizematic.ai)

---

## What is this?

`voizematic-mcp` is an [MCP (Model Context Protocol)](https://modelcontextprotocol.io) server that connects [Voizematic.ai](https://voizematic.ai) — a full-stack AI voice agent platform — directly into Claude and any other MCP-compatible AI assistant.

Instead of logging into a dashboard to manage your voice agents, you just **talk to Claude**.

---

## What can you do from Claude?

Once connected, you can have natural conversations with Claude to:

| Action | Example prompt |
|---|---|
| 🤖 Create AI voice agents | *"Create an outbound sales agent with a female English voice"* |
| 📋 List agents & phone numbers | *"Show me all my agents"* |
| 📞 Make outbound calls | *"Call +1XXXXXXXXXX using my sales agent"* |
| 🛡️ Run compliance checks | *"Check if this number is TCPA safe before calling"* |
| 📂 Upload contacts | *"Upload this CSV to my leads list"* |
| 🧠 Add knowledge bases | *"Create a knowledge base from voizematic.ai"* |
| 🚀 Launch bulk campaigns | *"Run a campaign to my Q2 leads list using agent 12"* |
| 📊 Analyse transcripts | *"Fetch the last call transcript and summarise it"* |
| 🗓️ Schedule callbacks | *"Schedule a follow-up call for tomorrow at 1 PM"* |
| 💰 Check wallet balance | *"How many credits do I have left?"* |

Watch live in action : https://www.youtube.com/watch?v=jhTNfISDfWk

---

## Quickstart (5 minutes)

### Prerequisites
- A [Voizematic.ai](https://voizematic.ai) account (free $25 credit for US businesses)
- [Claude Desktop](https://claude.ai/download) or any MCP-compatible client
- Your Voizematic API key → [get it here](https://voizematic.ai/settings/api)

### Step 1 — Add to Claude Desktop

Open your Claude Desktop config file:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`  
**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Add the following:

```json
{
  "mcpServers": {
    "voizematic": {
      "type": "url",
      "url": "https://voizematic.ai/mcp",
      "headers": {
        "X-Client-ID": "YOUR_VOIZEMATIC_CLIENT_ID",
        "X-Client-Secret": "YOUR_VOIZEMATIC_CLIENT_SECRET"
      }
    }
  }
}
```

> **Where to find your credentials:** Log in to [voizematic.ai](https://voizematic.ai) → **Settings → API / MCP** → copy your **Client ID** and **Client Secret**.

### Step 2 — Restart Claude Desktop

Fully quit and reopen Claude Desktop. You should see Voizematic tools available in the tools panel.

### Step 3 — Talk to Claude

```
You: Create a new outbound sales agent with a female English voice 
     and assign my US number to it.

Claude: ✅ Done! Agent "Sales Agent" created with voice Luna (female, English)
        and assigned to +1 832-905-0973.
```

That's it. You're live.

---

## Available MCP Tools

| Tool | Description |
|---|---|
| `list_agents` | List all your AI voice agents |
| `create_agent` | Create a new inbound or outbound agent |
| `get_agent` | Get full details and system prompt for an agent |
| `update_agent_prompt` | Update an agent's system prompt |
| `list_phone_numbers` | List all phone numbers on your account |
| `make_outbound_call` | Initiate a single outbound call |
| `schedule_callback` | Schedule a future callback |
| `check_phone_compliance` | Run TCPA, DNC & line type checks |
| `create_contact_list` | Create a new contact list |
| `import_contacts_csv` | Import contacts from CSV |
| `import_contacts_from_sheet` | Import contacts from Google Sheets |
| `get_contacts` | Search or list contacts |
| `list_knowledge_bases` | List all knowledge bases |
| `create_knowledge_base_text` | Create knowledge base from text |
| `create_knowledge_base_url` | Create knowledge base from a URL |
| `attach_knowledge_base_to_agent` | Attach knowledge base to an agent |
| `run_bulk_campaign` | Launch a bulk outbound call campaign |
| `get_call_history` | Get recent call history |
| `get_call_details` | Get transcript, summary & recording for a call |
| `get_call_analytics` | Get aggregate call analytics |
| `get_wallet_balance` | Check credits and recent transactions |
| `set_transfer_number` | Set call transfer number on an agent |

---

## Compliance Built-In

Every call through Voizematic runs automatic:
- ✅ **TCPA checks** — per-state rules, calling hours, consent requirements
- ✅ **DNC scrubbing** — Federal + State Do Not Call lists
- ✅ **Line type detection** — flags VoIP, mobile, landline, high-risk numbers

Claude will show you compliance results **before** every dial and block unsafe numbers automatically.

---

## Supported MCP Clients

| Client | Status |
|---|---|
| Claude Desktop | ✅ Supported |
| Claude.ai (web) | ✅ Supported |
| Cursor | ✅ Supported |
| Windsurf | ✅ Supported |
| Any MCP-compatible client | ✅ Supported |

---

## Documentation

- [Authentication](docs/authentication.md)
- [Tool Reference](docs/tool-reference.md)
- [Compliance Guide](docs/compliance.md)
- [Troubleshooting](docs/troubleshooting.md)

---

## About Voizematic

[Voizematic.ai](https://voizematic.ai) is a full-stack AI voice agent platform built for SMBs and enterprises. Key differentiators:

- 🛡️ **World's only** 2-layer TCPA/DNC compliance engine
- 🔗 **World's first** native Google Workspace integration
- 🧠 Conversation memory per contact
- ⚡ Sub-300ms latency
- 🇮🇳 India infrastructure — same-day deployment
- 🎯 Custom call metrics: Goal Achieved, Resistance Level, Buying Signals, Sentiment, Drop-Off Risk
- 🆓 Free $25 credit for US-based businesses

---

## License

MIT © [Voizematic.ai](https://voizematic.ai)
