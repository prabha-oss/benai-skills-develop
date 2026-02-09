# Browser Automation for Research

When WebFetch is blocked by a site, use `agent-browser` CLI to analyze inspiration websites.

**Source:** [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)

---

## When to Use

- WebFetch returns "blocked" or fails to fetch content
- Need to interact with dynamic content (SPAs, JavaScript-heavy sites)
- Need screenshots of inspiration sites
- Need to extract design elements from protected pages

---

## Core Workflow

```bash
# 1. Navigate
agent-browser open <url>

# 2. Snapshot (get element refs like @e1, @e2)
agent-browser snapshot -i

# 3. Interact (if needed)
agent-browser click @e1
agent-browser scroll down 500

# 4. Re-snapshot (after page changes)
agent-browser snapshot -i

# 5. Capture
agent-browser screenshot
```

---

## Essential Commands

```bash
# Navigation
agent-browser open <url>              # Navigate to URL
agent-browser close                   # Close browser

# Snapshot
agent-browser snapshot -i             # Interactive elements with refs
agent-browser snapshot -i -C          # Include cursor-interactive elements

# Get Information
agent-browser get text @e1            # Get element text
agent-browser get text body > page.txt  # Get all page text
agent-browser get url                 # Get current URL
agent-browser get title               # Get page title

# Wait
agent-browser wait --load networkidle # Wait for network idle
agent-browser wait 2000               # Wait milliseconds

# Capture
agent-browser screenshot              # Screenshot to temp dir
agent-browser screenshot --full       # Full page screenshot
agent-browser pdf output.pdf          # Save as PDF
```

---

## Extracting Design Elements

### Get Page Colors and Styles

```bash
agent-browser open <inspiration-url>
agent-browser snapshot -i

# Screenshot for visual reference
agent-browser screenshot --full inspiration.png
```

### Extract Text Content

```bash
agent-browser get text body > content.txt
```

### Analyze Specific Sections

```bash
agent-browser snapshot -s "#hero"     # Scope to hero section
agent-browser screenshot hero.png     # Screenshot that section
```

---

## Ref Lifecycle (Important)

Refs (`@e1`, `@e2`) are **invalidated when the page changes**. Always re-snapshot after:

- Clicking links or buttons that navigate
- Scrolling that loads new content
- Any dynamic content loading

```bash
agent-browser click @e5               # Navigates to new page
agent-browser snapshot -i             # MUST re-snapshot
agent-browser click @e1               # Use new refs
```

---

## Visual Browser (Debugging)

```bash
agent-browser --headed open <url>     # Open visible browser
agent-browser highlight @e1           # Highlight element
```

---

## Use in Research Phase

When analyzing user's inspiration site:

1. If WebFetch fails → Use `agent-browser open <url>`
2. Take full page screenshot → `agent-browser screenshot --full`
3. Extract visible text → `agent-browser get text body`
4. Analyze the screenshot visually
5. Report findings to user

---

## Installation

```bash
npm install -g @anthropics/agent-browser
```

Or use via npx:

```bash
npx @anthropics/agent-browser open <url>
```
