# MrScraper for ChatGPT and Codex

This marketplace packages MrScraper's MCP-oriented skills together with the
hosted MrScraper MCP server. It is a test distribution for ChatGPT Work mode,
the ChatGPT desktop app, and Codex.

## Add the marketplace

Use the GitHub `owner/repo` value as the marketplace source:

```text
mrscraper-com/mrscraper-chatgpt-plugin
```

If the client specifically asks for a Git repository URL, use
`https://github.com/mrscraper-com/mrscraper-chatgpt-plugin.git`.

From Codex CLI, add the marketplace and install the plugin:

```bash
codex plugin marketplace add mrscraper-com/mrscraper-chatgpt-plugin
codex plugin add mrscraper@mrscraper-plugins
```

The plugin connects to `https://mcp.mrscraper.com/mcp`. When prompted, finish
the OAuth authorization flow in your browser. Do not paste OAuth tokens or API
keys into chat.

## Try it

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

The server exposes seven tools:

| Tool | Description |
| --- | --- |
| `status` | Return the raw account status API response without summarizing, redacting body fields, or adding calculated fields. |
| `scrapeHtml` | Retrieve the raw HTML of a page. Browser rendering and a screenshot are optional. |
| `scrapeMarkdown` | Retrieve a page as Markdown. Browser rendering is optional. |
| `getScreenshot` | Capture a base64 PNG screenshot of the full page, the top viewport, or a custom viewport size. Browser rendering is always enabled. |
| `scrapeBrand` | Extract a website's colors, typography, logos, and social links as JSON. |
| `scrapeJson` | Extract structured JSON from a page using a natural-language prompt. Append Json Schema: and a JSON schema to shape the output. |
| `webSearch` | Search the web and return ranked results with titles, URLs, descriptions, and sources. |

The included skills use `scrapeMarkdown`, or `scrapeHtml` when the page
structure matters, as the normal first step when a URL is known because they
preserve the page response for flexible agent-led analysis. The skills read
only public pages the user is allowed to read, never sign in to websites, and
stop and tell the user when a site refuses the request or requires signing in.

## Contents

- `plugins/mrscraper/.codex-plugin/plugin.json`: ChatGPT/Codex plugin manifest
- `plugins/mrscraper/skills/`: MCP-oriented MrScraper skill pack
- `.agents/plugins/marketplace.json`: repository marketplace catalog

## Submission packaging

Package the contents of `plugins/mrscraper`, not the marketplace repository.
The ZIP root must contain `.codex-plugin/plugin.json`, `.mcp.json`, `assets/`,
and `skills/`. Increment the plugin manifest version when listing metadata
changes; this version is independent of the hosted MCP server version.

The listing uses the `Productivity` category and
<https://mrscraper.com/support> for customer support. Keep the description and
capability labels aligned with the actual tools.

The review test cases (five positive, three negative) and the release notes
are in `extensions.com.openai` of the plugin manifest. The dashboard imports
them from the ZIP and shows them read-only, so change them in the manifest and
upload a new version. The demo video URL and reviewer credentials stay in the
dashboard.

The privacy-policy URL points to the published policy at
<https://mrscraper.com/privacy-policy>. A new ZIP does not update that page.
Before resubmitting, ensure the published policy covers MCP inputs, scraped
content, backend model processing, recipient categories, retention timelines,
and available user controls.

## Development validation

```bash
codex plugin marketplace add .
codex plugin list
```

This repository is for marketplace testing before the equivalent packaging is
integrated into the official MrScraper repositories.
