# Actionbook Command Reference

Complete reference for all Actionbook commands.

## Browser Commands

### `browser status`
Show current connection status and detected browsers.

```bash
actionbook browser status
```

### `browser open <URL>`
Open URL in a new browser instance with CDP control.

```bash
actionbook browser open "https://example.com"
actionbook --stealth browser open "https://x.com"
actionbook --headless browser open "https://example.com"
```

### `browser goto <URL>`
Navigate the current page to a new URL.

```bash
actionbook browser goto "https://example.com/page2"
```

### `browser close`
Close the browser instance.

```bash
actionbook browser close
```

### `browser restart`
Restart the browser (close and reopen).

```bash
actionbook browser restart
```

### `browser connect <PORT|WS_URL>`
Connect to an existing browser via CDP port or WebSocket URL.

```bash
actionbook browser connect 9222
actionbook browser connect "ws://127.0.0.1:9222/devtools/browser/abc123"
```

## Content Extraction

### `browser eval <JAVASCRIPT>`
Execute JavaScript in the current page context and return the result.

```bash
actionbook browser eval "document.title"
actionbook browser eval "window.location.href"
actionbook browser eval "Array.from(document.querySelectorAll('a')).map(a => a.href)"
```

### `browser snapshot`
Get an accessibility tree snapshot (agent-browser compatible format).

```bash
actionbook browser snapshot
actionbook browser snapshot > page_structure.json
```

### `browser screenshot [PATH]`
Take a screenshot of the current page.

```bash
actionbook browser screenshot
actionbook browser screenshot /tmp/page.png
actionbook browser screenshot --full-page /tmp/full.png
```

### `browser pdf <PATH>`
Save the current page as PDF.

```bash
actionbook browser pdf /tmp/page.pdf
```

## Interaction Commands

### `browser click <SELECTOR>`
Click an element matching the CSS selector.

```bash
actionbook browser click "button.submit"
actionbook browser click "#login-button"
actionbook browser click "[data-testid='tweet-button']"
```

### `browser type <SELECTOR> <TEXT>`
Type text into an input element.

```bash
actionbook browser type "input[name='username']" "myuser"
actionbook browser type "#password" "secret123"
```

### `browser fill <SELECTOR> <TEXT>`
Fill an input field (clears first, then types).

```bash
actionbook browser fill "#search-box" "OpenClaw"
```

### `browser wait <SELECTOR>`
Wait for an element to appear in the DOM.

```bash
actionbook browser wait ".results"
actionbook browser wait "[data-loaded='true']"
```

### `browser inspect <X> <Y>`
Inspect the element at screen coordinates (X, Y).

```bash
actionbook browser inspect 100 200
```

### `browser viewport`
Show the current viewport size.

```bash
actionbook browser viewport
```

## Cookie Management

### `browser cookies list`
List all cookies for the current domain.

```bash
actionbook browser cookies list
```

### `browser cookies get <NAME>`
Get a specific cookie by name.

```bash
actionbook browser cookies get "session_id"
```

### `browser cookies set <NAME> <VALUE>`
Set a cookie.

```bash
actionbook browser cookies set "theme" "dark"
```

### `browser cookies delete <NAME>`
Delete a specific cookie.

```bash
actionbook browser cookies delete "tracking_id"
```

### `browser cookies clear`
Clear all cookies.

```bash
actionbook browser cookies clear
```

## Profile Management

### `profile list`
List all available profiles.

```bash
actionbook profile list
```

### `profile create <NAME>`
Create a new browser profile (isolated session with its own cookies/storage).

```bash
actionbook profile create work
actionbook profile create twitter-bot
```

### `profile delete <NAME>`
Delete a profile.

```bash
actionbook profile delete old-session
```

## Configuration

### `config show`
Display all configuration settings.

```bash
actionbook config show
```

### `config path`
Show the configuration file path.

```bash
actionbook config path
```

### `config get <KEY>`
Get a specific configuration value.

```bash
actionbook config get api_url
```

### `config set <KEY> <VALUE>`
Set a configuration value.

```bash
actionbook config set api_url "https://api.actionbook.dev"
```

## Global Flags

These flags work with any command:

### `--json`
Output results in JSON format.

```bash
actionbook --json browser status
```

### `--verbose`
Enable verbose logging.

```bash
actionbook --verbose browser open "https://example.com"
```

### `--stealth`
Enable anti-detection stealth mode.

```bash
actionbook --stealth browser open "https://x.com"
```

### `--stealth-os <OS>`
Set OS fingerprint for stealth mode.  
Options: `windows`, `macos-arm`, `macos-intel`, `linux`

```bash
actionbook --stealth --stealth-os windows browser open "https://example.com"
```

### `--stealth-gpu <GPU>`
Set GPU fingerprint for stealth mode.  
Options: `rtx4080`, `apple-m4-max`, `gtx1660`, `intel-uhd630`, etc.

```bash
actionbook --stealth --stealth-gpu rtx4080 browser open "https://example.com"
```

### `--profile <NAME>`
Use a specific browser profile.

```bash
actionbook --profile twitter browser open "https://x.com"
```

### `--headless`
Run browser in headless mode (no UI).

```bash
actionbook --headless browser open "https://example.com"
```

### `--browser-path <PATH>`
Use a specific browser executable.

```bash
actionbook --browser-path "/Applications/Brave Browser.app/Contents/MacOS/Brave Browser" browser open "https://example.com"
```

### `--cdp <PORT>`
Connect to an existing CDP port.

```bash
actionbook --cdp 9222 browser goto "https://example.com"
```

### `--api-key <KEY>`
Set API key for authenticated access.

```bash
actionbook --api-key "sk-your-key" search "etsy"
```

## Environment Variables

All flags can be set via environment variables:

```bash
export ACTIONBOOK_STEALTH=true
export ACTIONBOOK_STEALTH_OS=macos-arm
export ACTIONBOOK_STEALTH_GPU=apple-m4-max
export ACTIONBOOK_PROFILE=default
export ACTIONBOOK_HEADLESS=true
export ACTIONBOOK_API_KEY=sk-your-key

# Now use without flags
actionbook browser open "https://example.com"
```

## Exit Codes

- `0` - Success
- `1` - General error
- `126` - Permission denied
- `127` - Command not found
