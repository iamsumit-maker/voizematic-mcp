# Compliance Guide

Voizematic is the **world's only** AI voice agent platform with built-in 2-layer TCPA/DNC compliance. Every call is checked automatically before dialling.

## What Gets Checked

### 1. TCPA (Telephone Consumer Protection Act)
- Per-state calling hours (e.g. Connecticut: 8 AM–9 PM)
- Consent requirements for automated calls to wireless numbers
- State-specific penalties and enforcement risk levels

### 2. DNC (Do Not Call) Scrubbing
- Federal DNC Registry
- State-level DNC lists
- Internal suppression lists

### 3. Line Type Detection
- **Mobile** — requires prior written consent under TCPA
- **Landline** — standard rules apply
- **Non-fixed VoIP** — flagged as high fraud/disposable risk
- **Fixed VoIP** — moderate risk, standard rules apply

## Compliance Result States

| Status | Meaning | Action |
|---|---|---|
| ✅ Safe | Clear on all checks | Call proceeds automatically |
| ⚠️ Caution | Passes DNC but has TCPA risk factors | Requires explicit confirmation |
| 🚫 Blocked | On DNC list or calling hours violation | Call is blocked |

## Calling from Claude

When you ask Claude to make a call, it will automatically run compliance first:

```
You: Call +12035186279 using my collections agent

Claude: ⚠️ Compliance Check — CAUTION
        • Non-fixed VoIP (high fraud risk)
        • Connecticut — strict TCPA state ($11,000/violation)
        • Requires prior written consent
        
        Proceed anyway?
```

Claude will never silently bypass a compliance warning — you must explicitly confirm.

## India Compliance (NDNC)

For India-based calls:
- Numbers are scrubbed against the **NDNC (National Do Not Call)** registry via Vilpower API
- TRAI regulations apply
- Customers accept compliance responsibility via Voizematic's Terms of Service

## Disclaimer

Voizematic provides compliance infrastructure. Ultimate legal responsibility for outbound calling compliance remains with the operator. Always consult legal counsel for high-volume campaigns in regulated industries (debt collection, healthcare, financial services).
