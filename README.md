# MCP for Priority

The Model Context Protocol server for Priority ERP.

Connect Claude, ChatGPT, Copilot or any MCP client directly to Priority. Ask about revenue, check stock, raise an order — in Hebrew or English, without opening a single form.

**Works with Priority version 18 and above.**

MCP for Priority is a hosted service by LeonAI Ltd. This repository holds its documentation only; there is no source code here.

## Server address

```
https://priority-mcp.leonai.io/mcp
```

Streamable HTTP.

## Connect

1. Sign up for MCP for Priority and connect your Priority in its setup wizard: [Sign up](https://priority-mcp.leonai.io/signup?lang=en). Or join through the invitation link your organization's administrator sends.
2. In your MCP client, add the server address above as an MCP connector (a remote or custom connector).
3. Sign in. Each person signs in as themselves, with OAuth 2.1 and PKCE.
4. Ask a first question about your Priority data.

You can compare the plans first on [MCP plans and availability](https://priority-mcp.leonai.io/pricing?lang=en).

**Claude:** [How to connect Claude to Priority ERP: the steps](https://www.leonai.io/en/mcp/claude).

**Claude Code:**

```
claude mcp add --transport http priority-erp https://priority-mcp.leonai.io/mcp
```

Then run `/mcp` inside Claude Code to complete the OAuth flow and confirm the connection is live.

**Other clients:** setup for every MCP client, working with data and troubleshooting are in [the documentation](https://priority-mcp.leonai.io/docs?lang=en). Access is allowlisted at the network edge. Claude, ChatGPT and GitHub Copilot are already allowed, as is any client connecting from Israel. For anything else, email care@leonai.io with the client name and we will add it.

## What it does

- **Knows your Priority.** Reads your company's own data dictionary, custom fields and screens included after a metadata refresh, and searches it in Hebrew or English. Turn on the AI features and it searches by meaning too, not only by word.
- **Analytics that say what they counted.** P&L, sales trends, customer churn, stock movement and anomaly detection — using Priority's own revenue arithmetic. Every total states what it includes and what time its data is from, and a partial answer is marked partial.
- **Writes that check twice.** Orders, invoices, customers and remarks can be created and updated, and in a conversation every operation is shown for approval first. Before an update the server checks nobody changed the record since the preview, and after creating an order it reads the lines back. No tool in the catalog removes Priority data. Write operations are a paid add-on on the Base, Base Plus and Unlimited plans — see [MCP plans and availability](https://priority-mcp.leonai.io/pricing?lang=en).
- **Big questions don't stall.** A large result arrives page by page, with whether more remains and the way to the next page, instead of being cut off; the total is given when the read ran to the end. Long work moves to the background, and the assistant collects the answer when it is ready — instead of the conversation stalling.
- **Files in and out.** Attaches a PDF or an image to a Priority record, previewed and then confirmed. Lists a record's files with short-lived download links, and exports data to Excel, CSV or JSON — up to two million rows.
- **Text and remarks.** Reads and writes Priority's text tabs — remarks, internal, shipping, invoicing and ordering — order lines included. Writing appends by default, and Priority's internal HTML is handled, so you read and write plain text.
- **Procedures and reports.** Finds a procedure or a report by its Hebrew or English name, runs it step by step and returns the output: PDF, Word or HTML. Word output is parsed into tables and text.
- **Hebrew, properly.** Hebrew search terms go to Priority unchanged. Field descriptions, currency aliases and RTL output are handled rather than approximated.
- **WhatsApp and Outlook — optional, paid add-ons.** Add messaging and mail to the same assistant that reads your ERP: send messages, read chats, manage the inbox and calendar. Outlook signs in with per-user OAuth, and WhatsApp links your own number by QR code or pairing code. Off by default, enabled per tenant.

### Tool reference

The same tools on every plan: Sales, procurement, inventory, finance, shipping and service.

Each account's tool reference — every tool it is served, with the exact description the assistant receives — is inside its tenant portal, under ERP connection › Tool catalogue. Directory reviewers can request the complete list from care@leonai.io.

## Security

- Core processing and storage (application, database, cache and object storage) run on Google Cloud Run in me-west1, Tel Aviv. A private Enterprise deployment runs in the region agreed in its contract.
- Some data leaves Israel: edge traffic metadata, billing and partner records, the AI features and the WhatsApp and Outlook add-ons when they are turned on, and the AI assistant you connect. The full list is on the [Security](https://priority-mcp.leonai.io/security?lang=en) page.
- TLS 1.2+ on every hop — client, database, cache and ERP.
- OAuth 2.1 with mandatory PKCE S256; 2FA (TOTP) available on every plan, per user or enforced tenant-wide; SAML 2.0 / OIDC single sign-on (SSO) on the Enterprise plan.
- AES-256 on managed storage; ERP credentials additionally encrypted with Fernet.
- Tenant credentials are stored encrypted with Fernet, using a key derived with PBKDF2 at 480,000 iterations.
- An optional per-tenant IP allowlist, off until an administrator turns it on.
- Every query, cache key and storage object namespaced by tenant.
- Credentials and identifying details are masked in every log handler — passwords, API keys and tokens are never logged.
- An audit log of every tool call. A nightly job chains its rows with SHA-256.
- Access logs are retained for 24 months, satisfying the Israeli Privacy Protection Regulations' access-logging requirement. The 24-month policy started in August 2026, so the archive is still growing toward that depth.
- Writes are off by default. In a conversation each write is shown for approval first and runs once, through a server-signed, single-use confirmation. An automation skips that approval only with an API key an administrator explicitly allowed to do so.
- MCP for Priority has no ERP delete tool at all.
- ISO 27001 certified — certificate scope: automations and integrations for companies.
- SOC 2 Type II in progress.

More: [Security](https://priority-mcp.leonai.io/security?lang=en) · [Trust center](https://www.leonai.io/en/security).

## Plans and pricing

Plans and prices: [MCP plans and availability](https://priority-mcp.leonai.io/pricing?lang=en).

## Links

- Product page: https://www.leonai.io/en/products/mcp-for-priority
- Documentation: https://priority-mcp.leonai.io/docs?lang=en
- Support: https://priority-mcp.leonai.io/support?lang=en
- Contact: care@leonai.io
- Service status: https://status.leonai.io

## עברית

<div dir="rtl" lang="he">

**שרת MCP ל־Priority ERP.** בינה מלאכותית לפריוריטי: מחבר את Priority ERP ל־Claude, ל־ChatGPT, ל־Copilot ול־n8n, עם יומן ביקורת ומנגנון כתיבה דו־שלבי.

- תומך ב־Priority 18 ומעלה.
- כתובת השרת: `https://priority-mcp.leonai.io/mcp`
- [נרשמים ל־MCP for Priority](https://priority-mcp.leonai.io/signup?lang=he)
- [חיבור Claude לפריוריטי: איך מחברים, צעד אחר צעד](https://www.leonai.io/mcp/claude)
- [עמוד המוצר](https://www.leonai.io/products/mcp-for-priority)
- [התיעוד, עם ההתקנה לכל לקוח MCP](https://priority-mcp.leonai.io/docs?lang=he)
- [מסלולי MCP וזמינות](https://priority-mcp.leonai.io/pricing?lang=he)
- [אבטחה](https://priority-mcp.leonai.io/security?lang=he)

</div>

---

Priority is a trademark of Priority Software Ltd. LeonAI is an independent company, and its products are independent products.

© LeonAI Ltd. All rights reserved. This repository contains documentation only; no licence to use or copy any software is granted by it.
