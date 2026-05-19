# Tool Reference

Complete reference for all 22 Voizematic MCP tools. Every tool is callable directly from Claude — just describe what you want in plain English.

---

## Agents

### `list_agents`
List all AI voice agents on your account.

**Example prompt:** *"Show me all my agents"*

**Returns:** Agent ID, name, type (inbound/outbound), voice, assigned phone number, status.

---

### `create_agent`
Create a new inbound or outbound AI voice agent.

**Example prompt:** *"Create an outbound collections agent with a female English voice assigned to my US number"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `name` | ✅ | Display name for the agent |
| `type` | ✅ | `inbound` or `outbound` |
| `voice.gender` | ✅ | `male` or `female` |
| `voice.language` | ✅ | `English`, `Hindi`, etc. |
| `phoneNumber` | ❌ | Phone number to assign (E.164 format) |
| `systemPrompt` | ❌ | Agent's core instructions |
| `greeting` | ❌ | Opening line when call connects |
| `primaryGoals` | ❌ | What the agent is trying to achieve |

> **Note:** Each phone number can have one inbound and one outbound agent.

---

### `get_agent`
Get full details and the system prompt for a specific agent.

**Example prompt:** *"Show me the full system prompt for agent 65"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID (get from `list_agents`) |

---

### `update_agent_prompt`
Update the system prompt of an existing agent.

**Example prompt:** *"Update agent 65's system prompt to focus on upselling"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID |
| `systemPrompt` | ✅ | New system prompt text |

---

### `set_transfer_number`
Set or update the call transfer (forward) number on an agent.

**Example prompt:** *"Set the transfer number for agent 65 to +18001234567"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID |
| `transferNumber` | ✅ | Phone number to transfer calls to (E.164) |
| `transferMode` | ❌ | When to transfer — `on_request`, `always`, etc. |

---

## Phone Numbers

### `list_phone_numbers`
List all phone numbers owned on your account.

**Example prompt:** *"What phone numbers do I have?"*

**Returns:** Phone number, friendly name, provider (Twilio/Plivo), assigned agent.

---

## Calls

### `make_outbound_call`
Initiate a single outbound call from an agent to a phone number.

**Example prompt:** *"Call +12035186279 using my collections agent"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID to use for the call |
| `toNumber` | ✅ | Destination number (E.164 format) |
| `contactName` | ❌ | Name shown in dashboard |
| `objective` | ❌ | What the agent should aim to achieve |
| `complianceConfirmed` | ❌ | Set `true` to proceed past caution warnings |

> ⚠️ Claude will always run `check_phone_compliance` before dialling and surface the results. Blocked numbers are never dialled.

---

### `schedule_callback`
Schedule a future callback call at a specific date and time.

**Example prompt:** *"Schedule a follow-up call to +12035186279 tomorrow at 1 PM Eastern"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID |
| `toNumber` | ✅ | Destination number (E.164) |
| `scheduledAt` | ✅ | ISO 8601 datetime (e.g. `2026-05-21T13:00:00`) |
| `timezone` | ✅ | IANA timezone (e.g. `America/New_York`, `Asia/Kolkata`) |
| `contactName` | ❌ | Contact display name |
| `reason` | ❌ | Reason shown in dashboard |
| `notes` | ❌ | Additional context for the agent |

---

### `get_call_history`
Get recent call history across all agents.

**Example prompt:** *"Show me the last 10 calls"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `limit` | ❌ | Number of calls to return (default: 20) |
| `agentId` | ❌ | Filter by specific agent |

---

### `get_call_details`
Get full details for a specific call: transcript, AI summary, recording URL, sentiment, goal tracking.

**Example prompt:** *"Fetch the transcript for my last call"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `callSid` | ✅ | Call SID (get from `get_call_history` or `make_outbound_call`) |

**Returns:** Full transcript, AI summary, goal achieved (✅/❌), sentiment, emotion, resistance level, buying signals, objections detected, recording URL.

---

### `get_call_analytics`
Get aggregate call analytics: total calls, avg duration, success rate, top agents.

**Example prompt:** *"How are my agents performing this month?"*

---

## Compliance

### `check_phone_compliance`
Run TCPA, DNC, and line-type checks on one or more phone numbers before dialling.

**Example prompt:** *"Is +12035186279 safe to call?"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `phoneNumbers` | ✅ | Array of numbers to check (E.164 format) |

**Returns per number:**
- **Status:** `safe` / `caution` / `blocked`
- **Line type:** mobile, landline, VoIP, non-fixed VoIP
- **State:** US state (for TCPA rules)
- **Risks:** List of specific compliance flags
- **Calling hours:** Allowed hours for that state
- **Penalty:** Potential fine per violation

---

## Contacts

### `create_contact_list`
Create a new, empty contact list.

**Example prompt:** *"Create a contact list called Q2 Leads"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `name` | ✅ | Name for the list |

---

### `import_contacts_csv`
Import contacts into a list from CSV text.

**Example prompt:** *"Import these contacts into my Q2 Leads list"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `listId` | ✅ | Contact list ID |
| `csvData` | ✅ | CSV string with header row (`name,phone,email`) |

---

### `import_contacts_from_sheet`
Import contacts from a Google Sheet URL.

**Example prompt:** *"Import contacts from this Google Sheet into my leads list"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `listId` | ✅ | Contact list ID |
| `sheetUrl` | ✅ | Google Sheets URL (must be publicly accessible or shared) |

---

### `get_contacts`
Search or list contacts across all lists.

**Example prompt:** *"Find all contacts named John"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `query` | ❌ | Search term (name, phone, email) |
| `listId` | ❌ | Filter by specific list |

---

## Knowledge Bases

### `list_knowledge_bases`
List all knowledge bases in your account.

**Example prompt:** *"What knowledge bases do I have?"*

---

### `create_knowledge_base_text`
Create a new knowledge base from plain text content.

**Example prompt:** *"Create a knowledge base from this FAQ text"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `name` | ✅ | Knowledge base name |
| `content` | ✅ | Text content (FAQs, scripts, product info, etc.) |

---

### `create_knowledge_base_url`
Create a new knowledge base by scraping a website or YouTube URL.

**Example prompt:** *"Create a knowledge base from voizematic.ai"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `name` | ✅ | Knowledge base name |
| `url` | ✅ | Website URL or YouTube video URL |

---

### `attach_knowledge_base_to_agent`
Attach one or more knowledge bases to an agent so it can reference them during calls.

**Example prompt:** *"Attach the Product FAQ knowledge base to agent 65"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID |
| `kbIds` | ✅ | Array of knowledge base IDs to attach |

---

## Campaigns

### `run_bulk_campaign`
Launch a bulk outbound call campaign to every contact in a list.

**Example prompt:** *"Run a campaign to my Q2 Leads list using agent 65"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `agentId` | ✅ | Agent ID to use for all calls |
| `contactListId` | ✅ | Contact list to dial |

> Blocked numbers (DNC/TCPA) are automatically skipped. Caution numbers require explicit confirmation.

---

## Account

### `get_wallet_balance`
Get current wallet balance and recent transactions.

**Example prompt:** *"How many credits do I have left?"*

**Returns:** Current balance, currency, recent transaction history.

---

### `get_user`
Look up a platform user account by email address. *(Admin only)*

**Example prompt:** *"Look up the account for user@example.com"*

**Parameters:**
| Field | Required | Description |
|---|---|---|
| `email` | ✅ | Email address of the user to look up |
