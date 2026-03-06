# actionbook-skill

An AI agent skill for browser automation and web scraping with anti-detection stealth mode. Built on [Actionbook](https://github.com/actionbook/actionbook) CLI.

## What It Does

This skill teaches AI agents how to use the Actionbook browser engine for tasks that regular HTTP fetching can't handle:

- **Stealth browsing** — bypass anti-bot detection (navigator overrides, WebGL fingerprint spoofing, automation flag removal)
- **JavaScript-rendered pages** — extract content from SPAs and dynamic sites that `web_fetch` cannot parse
- **Browser interactions** — click, type, navigate, fill forms, take screenshots
- **Session persistence** — manage cookies and browser profiles for login-required workflows
- **Twitter/X scraping** — extract tweets and timelines without login using stealth mode

## Use Cases

- Extract structured data (titles, links, dates, authors) from any web page
- Scrape public feeds and timelines without manual browsing
- Automate multi-step web workflows (search → filter → export)
- Capture screenshots for visual verification
- Handle sites with anti-bot protection, CAPTCHAs, or JavaScript-only rendering

## Usage

Describe your task naturally to the AI agent. Examples:

```
Use actionbook to extract the first 20 titles and links from <URL>.
Use actionbook to open this page and take a screenshot.
Use actionbook to paginate 3 pages and export all item links.
```

The skill provides the agent with command references, CSS selector cheat sheets, and workflow patterns so it knows exactly how to operate the Actionbook CLI.

## Repository Structure

| Path | Description |
|---|---|
| `SKILL.md` | Skill definition — capabilities, commands, workflow patterns, troubleshooting |
| `scripts/fetch_tweet.sh` | Example script for extracting Twitter/X content |
| `references/commands.md` | Complete Actionbook CLI command reference |
| `references/selectors.md` | CSS selectors for popular sites (Twitter, Reddit, LinkedIn, GitHub, etc.) |

## Prerequisites

[Actionbook CLI](https://github.com/actionbook/actionbook) must be installed:

```bash
# macOS / Linux
curl -fsSL https://actionbook.dev/install.sh | bash

# or via npm
npm install -g @actionbookdev/cli

# then run setup
actionbook setup
```

## Responsible Use

- Only scrape data you have permission to access or that is legally permitted.
- Avoid high-frequency requests to target sites. Respect `robots.txt` and terms of service.
- For volatile pages, prefer stable selectors and add retry/timeout controls.

## Links

- [Actionbook CLI](https://github.com/actionbook/actionbook)
- [Actionbook Documentation](https://actionbook.dev/docs)
- [This Skill](https://github.com/longzhi/actionbook-skill)
