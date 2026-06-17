# Converly MCP

Set up and manage your conversion tracking by chatting with your AI assistant.

Converly tracks form conversions and fires them to ad platforms (Google Ads, Meta, GA4, and more) when someone submits a form on your website. The Converly MCP server lets an AI assistant like Claude or ChatGPT do that work for you: connect ad platforms, build and publish conversion flows, install tracking, and check your conversions, all inside your Converly account.

This is a **remote, hosted MCP server**. There is nothing to install or run. You add it as a custom connector in your AI assistant and authorize it, and that is it.

**Connector address:** `https://app.converly.io/mcp`

## What you can do

Connect it, then just say what you want. For example:

- "Connect my Google Ads account and set up conversion tracking for my contact form."
- "Create a flow that sends a Lead event to Meta whenever someone submits my Typeform."
- "Did my form conversions fire to Google Ads yesterday? Show me what happened."
- "Why is my conversion not showing up in Google Ads?"
- "Publish my new flow and give me the snippet to install on my site."
- "Add our office IP so our own team visits do not get tracked."

## Connect it

### Claude (web or desktop)

1. Open **Settings**, then **Connectors**, then **Add custom connector**.
2. Paste the address: `https://app.converly.io/mcp`
3. Authorize it. You log in to Converly (or create an account, which starts a free trial) and approve access.
4. Start a new chat and try "Help me set up conversion tracking."

### ChatGPT

1. Enable **Developer Mode** under Settings, then Apps, then Advanced.
2. Add a connector and paste the address: `https://app.converly.io/mcp`
3. Authorize it, then start chatting.

> Custom connectors require a supported plan on the AI side. Claude allows one custom connector on the Free plan and more on paid plans. ChatGPT requires a paid plan with Developer Mode.

## How it stays safe

You stay in control the whole way:

- You authorize the connection through Converly's own login and a consent screen.
- The assistant cannot finish ad platform logins by itself. When you connect Google Ads or Meta, it hands you a secure link and you complete the login in your browser.
- Anything destructive or billing related requires explicit confirmation. Deleting a flow, disconnecting a platform, or changing your plan all require you to confirm by name first.
- Access is scoped, and every read or write is checked against your account on each request.

## Tools

The server exposes 27 tools, grouped here by what they do:

**Sites and install**
`list_sites`, `create_site`, `get_install_snippet`, `get_install_status`

**Flows** (a flow fires a conversion when a form is submitted)
`list_flows`, `get_flow`, `create_flow`, `update_flow`, `validate_flow`, `publish_flow`, `unpublish_flow`, `delete_flow`

**Destinations** (your ad platforms)
`list_destinations`, `list_destination_types`, `connect_destination`, `check_handoff_status`, `disconnect_destination`, `list_conversions`

**Conversions and events**
`list_events`, `get_event_detail`, `send_test_event`

**Discovery**
`list_trigger_types`, `list_action_types`

**Account and billing**
`get_subscription`, `list_plans`, `change_plan`

**Internal traffic**
`add_internal_traffic_rule`

The server also ships guided **prompts** (one-click workflows in clients that support them): set up conversion tracking, connect an ad platform, and check recent conversions.

## Links

- Converly for AI assistants: https://converly.io/mcp
- Converly home: https://converly.io
- Pricing and free trial: https://converly.io/pricing

## About this repository

This repository is the public home and documentation for the Converly MCP integration. It does not contain the server code. The server is a hosted part of Converly and runs at `https://app.converly.io/mcp`. For questions or issues with the MCP, open an issue here or contact Converly support.
