<div align="center">

<img src="assets/cover.png" alt="Slack through HeyMetra's MCP server" width="100%">

# Slack &times; HeyMetra

**Post to Slack, in whichever channel you say.**

An answer nobody reads is not an answer. Have it delivered to Slack, where the team already is.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.heymetra%2Fheymetra-1f6feb)](https://registry.modelcontextprotocol.io/v0/servers/com.heymetra%2Fheymetra/versions)
[![Transport](https://img.shields.io/badge/transport-Streamable_HTTP-444)](https://modelcontextprotocol.io/)
[![Auth](https://img.shields.io/badge/auth-OAuth_2.1-444)](https://heymetra.com/security/)
[![Connector page](https://img.shields.io/badge/heymetra.com-slack-1f6feb)](https://heymetra.com/connectors/slack/)

```
https://mcp.heymetra.com/mcp
```

</div>

---

## Connect Slack

**1. Install the HeyMetra app in your Slack workspace**

On the Connections screen choose Slack. Slack shows you what the app may do — post messages, and list channels so it can ask you which one — and you approve it there. You are back in HeyMetra when it is done.

> One install covers the whole workspace. You do not connect Slack again per channel, and there is nothing to choose here.

**2. Invite the app to any PRIVATE channel you want to use**

Public channels need nothing: the app can post to them without joining. A private channel is different — type /invite @HeyMetra in it. Until you do, HeyMetra cannot see that the channel exists, so it will not be offered.

> This is the step people skip and then wonder why a channel is missing from the list. If a private channel is not offered, it has not been invited.

**3. Ask for something to be sent, and name the channel**

Say what you want posted. Your assistant asks which channel, then shows a card with the exact text and the exact channel before anything is sent. Approve it and it goes; until then nothing has left HeyMetra. It posts what you asked for, when you ask — there is nothing here that posts on a timer.

**4. Check it from the Connections screen**

The send button beside the connection posts a fixed test message, so you can confirm delivery works without composing anything.

## Then add HeyMetra to your assistant

Add HeyMetra once and it is there in every conversation. The address is the same everywhere:

```
https://mcp.heymetra.com/mcp
```

<details>
<summary><b>Claude</b> — Settings → Customize → Connectors → Add custom connector</summary>

Paste the address above into Settings → Customize → Connectors → Add custom connector.

_On Team and Enterprise plans only an owner can add it, under Organization settings._

Full walkthrough: [heymetra.com/mcp/claude/](https://heymetra.com/mcp/claude/)
</details>

<details>
<summary><b>ChatGPT</b> — Settings → Security and login → Developer mode, then chatgpt.com/plugins</summary>

Paste the address above into Settings → Security and login → Developer mode, then chatgpt.com/plugins.

_The endpoint has to include its /mcp path here._

Full walkthrough: [heymetra.com/mcp/chatgpt/](https://heymetra.com/mcp/chatgpt/)
</details>

<details>
<summary><b>Grok</b> — grok.com/connectors → New Connector → Custom</summary>

Paste the address above into grok.com/connectors → New Connector → Custom.

_XAI calls this “bring your own MCP”._

Full walkthrough: [heymetra.com/mcp/grok/](https://heymetra.com/mcp/grok/)
</details>

<details>
<summary><b>Perplexity</b> — Settings → Connectors → Custom connector → Remote</summary>

Paste the address above into Settings → Connectors → Custom connector → Remote.

_Perplexity documents it as a Pro, Max and Enterprise feature._

Full walkthrough: [heymetra.com/mcp/perplexity/](https://heymetra.com/mcp/perplexity/)
</details>

<details>
<summary><b>Claude Code</b> — claude mcp add --transport http</summary>

```bash
claude mcp add --transport http heymetra https://mcp.heymetra.com/mcp
```

_Or a .mcp.json in the project root; /mcp inside a session shows what connected._

Full walkthrough: [heymetra.com/mcp/claude-code/](https://heymetra.com/mcp/claude-code/)
</details>

<details>
<summary><b>Codex</b> — ~/.codex/config.toml</summary>

```toml
[mcp_servers.heymetra]
url = "https://mcp.heymetra.com/mcp"
```

_Under an [mcp_servers.<name>] section, then codex mcp login._

Full walkthrough: [heymetra.com/mcp/codex/](https://heymetra.com/mcp/codex/)
</details>

<details>
<summary><b>Cursor</b> — ~/.cursor/mcp.json, or .cursor/mcp.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "url": "https://mcp.heymetra.com/mcp" }
  }
}
```

_Leave the static OAuth fields empty — they exist for servers that cannot register themselves._

Full walkthrough: [heymetra.com/mcp/cursor/](https://heymetra.com/mcp/cursor/)
</details>

<details>
<summary><b>Antigravity</b> — ~/.gemini/config/mcp_config.json, or .agents/mcp_config.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "serverUrl": "https://mcp.heymetra.com/mcp" }
  }
}
```

_The key is serverUrl, not url — the one every other JSON client spells differently._

Full walkthrough: [heymetra.com/mcp/antigravity/](https://heymetra.com/mcp/antigravity/)
</details>

## What it may and may not touch

Send a message to the linked Slack channel — proposed first, with the exact text, and posted only once you approve. Everyone in that channel sees it, and it cannot be unsent.

Permissions are switched on per connection, and one you leave off is a tool your assistant never sees.

| Permission | What it covers | Changes anything? |
|---|---|---|
| **Included with the connection** | What HeyMetra needs to set the connection up and nothing more. It cannot be switched off on its own — removing the connection is how you withdraw it. | No, read only |
| **Send messages** | Let your assistant post to this channel, with your approval each time. Turn it off and only the test button can reach it. | Yes — every change waits for your approval |

<details>
<summary>What each permission lets an assistant do, in full</summary>

- Send a message to the linked Slack channel — proposed first, with the exact text, and posted only once you approve. Everyone in that channel sees it, and it cannot be unsent.
</details>

Anything that would change something comes back as a proposal you approve, inside bounds that live in code rather than in a prompt: at most 20 messages a rolling day, counted separately from account changes, and an approval that expires after 30 minutes. [How that works](https://heymetra.com/security/).

## When something goes wrong

<details>
<summary>A channel you use every day is not in the list.</summary>

**Why:** It is private, and the HeyMetra app has not been invited to it. Slack does not reveal private channels an app is not in.

**Fix:** Open that channel and type /invite @HeyMetra, then ask again.

</details>

<details>
<summary>Your assistant says it cannot choose a channel, or posts nothing at all.</summary>

**Why:** Some assistants cache the list of tools from when they first connected, and an older description of this one said the channel could not be chosen.

**Fix:** Start a new conversation in your assistant so it reloads the tools from HeyMetra.

</details>

<details>
<summary>A message went to the wrong channel.</summary>

**Why:** The channel is named on the approval card, and approving is what sends it — so a message in the wrong place was approved for that place.

**Fix:** Read the destination line on the card before approving; it names the channel, not an id. HeyMetra cannot unsend a Slack message afterwards, and neither can Slack.

</details>

<details>
<summary>The app was removed from Slack and sends now fail.</summary>

**Why:** Uninstalling the app in Slack revokes the token HeyMetra holds. The connection remains on the Connections screen and stops working.

**Fix:** Connect Slack again from the Connections screen. The same channels become available as soon as the install is back.

</details>

## What HeyMetra reads from Slack

Install the app once into your Slack workspace. There is no channel to pick while connecting: the install reaches every public channel in your workspace, plus any private one you invite it to. When you ask for something to be sent, your assistant asks which channel, shows you the exact text and the exact channel, and nothing leaves until you approve it. Everyone in that channel sees what is posted and a posted message cannot be unsent. Nothing is ever read from Slack.

<details>
<summary>About Slack</summary>

Slack is where your team already works. Connecting it gives your assistant somewhere to post what you ask it to post — and it asks which channel every time, because choosing the channel is choosing who reads it.
</details>

## One connection, not seven

The reason to read Slack through HeyMetra rather than through a server that only knows Slack is everything else it can answer in the same breath:

**Ads** — [Google Ads](https://heymetra.com/connectors/google-ads/) · [Meta](https://heymetra.com/connectors/meta-ads/)

**Analytics** — [Google Analytics 4](https://heymetra.com/connectors/google-analytics-4/) · [Google Search Console](https://github.com/zeisoft/google-search-console-mcp)

**Ecommerce** — [Shopify](https://heymetra.com/connectors/shopify/) · [Trendyol](https://github.com/zeisoft/trendyol-mcp) · [WooCommerce](https://github.com/zeisoft/woocommerce-mcp)

**Revenue & CRM** — [Stripe](https://heymetra.com/connectors/stripe/) · [HubSpot](https://heymetra.com/connectors/hubspot/) · [Zoho CRM](https://github.com/zeisoft/zoho-crm-mcp) · [Zoho SalesIQ](https://github.com/zeisoft/zoho-salesiq-mcp) · [Zoho Marketing Automation](https://github.com/zeisoft/zoho-marketing-automation-mcp)

**Mobile** — [AppsFlyer](https://github.com/zeisoft/appsflyer-mcp) · [RevenueCat](https://heymetra.com/connectors/revenuecat/) · [Adapty](https://github.com/zeisoft/adapty-mcp) · [App Store Connect](https://github.com/zeisoft/app-store-connect-mcp)

**Channels** — **Slack** · [Telegram](https://github.com/zeisoft/telegram-mcp)

The full catalogue is at [heymetra.com/connectors/](https://heymetra.com/connectors/).

## Links

- [Slack connector page](https://heymetra.com/connectors/slack/)
- [HeyMetra](https://heymetra.com/) — what the product is
- [Setup for every assistant](https://heymetra.com/mcp/)
- [Security and limits](https://heymetra.com/security/)
- [Pricing](https://heymetra.com/pricing/)
- [HeyMetra's own repository](https://github.com/zeisoft/heymetra-mcp)

---

<sub>Built by <a href="https://zeisoft.com">Zeisoft</a>, who make HeyMetra. Not affiliated with Slack. This README is generated from HeyMetra's live connector catalogue and refreshed daily; corrections are welcome as issues.</sub>
