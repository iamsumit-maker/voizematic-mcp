# Troubleshooting

## Claude doesn't see Voizematic tools

**Fix:** Make sure you've fully quit and relaunched Claude Desktop after editing the config file. On macOS, `Cmd+Q` — don't just close the window.

**Check:** Open Claude Desktop → click the tools/plug icon → Voizematic tools should appear in the list.

## "Unauthorized" error

Your API key is missing or incorrect. Double-check:
- The key is copied in full (no trailing spaces)
- It's placed under `"Authorization": "Bearer YOUR_KEY"` in the config
- The key hasn't been deleted from your Voizematic dashboard

## "Number already has an outbound agent" error

Each phone number can only have **one inbound** and **one outbound** agent. To assign a number to a new agent, first unassign it from the existing agent via the [dashboard](https://voizematic.ai/ai-agents).

## Call not connecting

1. Check that the destination number is in E.164 format (e.g. `+12035186279`)
2. Run a compliance check first — blocked numbers won't connect
3. Verify the agent has a phone number assigned
4. Check your wallet balance — calls require credits

## MCP server URL not loading

The Voizematic MCP server is hosted at `https://voizematic.ai/mcp`. If it's unreachable:
- Check your internet connection
- Check [status.voizematic.ai](https://voizematic.ai) for any outages
- Try again in a few minutes

## Still stuck?

Email [support@voizematic.ai](mailto:support@voizematic.ai) or open an issue on this repo.
