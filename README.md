# SMART RABBIT (AKILLI TAVŞAN)

![babayigit.png](babayigit.png)

> **"We didn't come here for nothing, tough guy."**

The internet is a massive city, and web pages are its dark alleys. Some hide behind HTML tags, some change CSS classes daily to lose their trail, and others build JavaScript labyrinths to keep us out.

**We don't take off our sunglasses when we enter those labyrinths.**

---

## MISSION DOSSIER

Manifest V3 Chrome Extension. No frameworks, no bundlers—pure field operation. It gathers data using a 3-phase strategy, structures it with AI, and puts it on the table.

### 3-Phase Operation

**Phase 0 — DOM Recon (Smart Schema Discovery)**
Identifies repeating elements on the page. Sends 3-5 examples to the AI, which returns the schema (field mapping). The rest is mechanical—no further AI needed. Also captures lazy-loaded content via scrolling.

**Phase 1 — API Hunting (Mechanical Pagination)**
Monitors network traffic to find JSON endpoints. Detects pagination patterns (page/offset/cursor). Fetches all pages mechanically; AI is only called once for the schema.

**Phase 2 — Agent Loop (Last Resort)**
If Phases 0 and 1 fail, the AI agent takes over. It interacts with the page—scrolling, clicking, navigating, and fetching URLs. Max 30 iterations; stops after 3 consecutive empty steps.

### Capabilities

- **Schema Discovery**: Instead of processing all data, the AI only sees 3-5 examples to produce a mapping. ~90% token savings.
- **Cross-Parent Pattern Detection**: Merges elements with the same structure even if they are in different carousels or containers.
- **Network Intercept**: Captures all API traffic via fetch/XHR monkey-patching (200 request buffer).
- **Accumulate Mode**: Collects data from different pages into a single table. Automatically skips duplicates.
- **JSON & CSV Export**: Download the collected data with a single click.
- **3 AI Providers**: OpenAI, Claude, Gemini. API keys are stored locally in the browser.

## TECHNICAL DETAILS

| Unit | Technology |
|-------|-----------|
| Extension | Chrome Manifest V3, Vanilla JS |
| Content Script | DOM analysis, network intercept, page actions |
| Background | Service worker, message router |
| Side Panel | Scraping orchestrator, AI integration, UI |
| AI Providers | OpenAI (gpt-4o-mini), Claude (claude-sonnet-4-20250514), Gemini (gemini-2.0-flash) |

## LIMITS

| Limit | Value |
|-------|-------|
| Network capture buffer | 200 requests (FIFO) |
| Request body — JSON | max 100KB |
| Request body — other | max 10KB |
| HTML sent to AI | max 50K characters |
| Max pagination | 50 additional pages |
| Max agent loop iterations | 30 |
| Max scroll loop | 50 iterations |

## INSTALLATION

1. Clone this repository.
2. Go to `chrome://extensions` → Enable Developer mode → Click "Load unpacked" → Select the folder.
3. Click the extension icon → The side panel opens.
4. Enter your AI provider and API key in Settings.
5. Enter the target, and "Start Operation."

## ARCHITECTURE

```
Side Panel (sidepanel.js)
    | chrome.runtime.sendMessage()
Background Service Worker (background.js)
    | chrome.tabs.sendMessage()
Content Script (content.js)
    | sendResponse()
(The response returns through the same chain)
```

---

> **"We read the page, we're heading out."**

*Some rabbits don't like carrots. They love data.*

---
**Disclaimer:** *The tone of this documentation is a satirical tribute to the character "Pala" from the Turkish cult TV series "Valley of the Wolves" (Kurtlar Vadisi).*
