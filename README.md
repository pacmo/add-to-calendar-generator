# 📅 Add to Calendar Generator 

A **single-file, zero-dependency** HTML tool for generating production-ready "Add to Calendar" button code for Eloqua email campaigns. Supports multiple events, `.ics` file import, responsive layout, and is hardened to OWASP standards — all client-side, all offline-capable.

---

## ✨ Features

### Core
- **Multi-event support** — add, edit, and delete as many events as you need
- **Live preview** — button renders in real time on a white email background
- **All major calendar providers** — Google Calendar, Outlook.com, Apple / iCal (`.ics`), Yahoo Calendar
- **Eloqua-safe HTML** — table-based layout with MSO conditional comments for Outlook on Windows
- **Two output modes** per panel — *One per event* (individual button blocks) or *Combined block* (stacked digest layout)
- **Full email template output** — complete Eloqua-ready wrapper with header, event details, button, and footer

### Customization
- Three button styles: **Filled**, **Outline**, **Pill**
- Color pickers for button background, button text, and link color
- Custom button label text

### Import
- **Drag-and-drop `.ics` import** — parse single or multi-event iCalendar files
- Selectively add individual events from an imported file into your event list
- All parsing is done locally — files never leave the browser

### Responsive
- Full two-panel layout on desktop
- Slide-out drawer with overlay on mobile (≤720px)
- Narrower left panel on mid-size screens (721–1100px)

---

## Security

This tool is built to OWASP standards. All user input is treated as untrusted.

| Risk | Mitigation |
|---|---|
| **XSS via event data** | Preview built entirely with `createElement` / `textContent` — no `innerHTML` for user-controlled data |
| **XSS in code output** | All user data HTML-entity-encoded via `esc()` before output; written to `textContent` of code blocks |
| **URL injection** | `safeUrl()` allowlists `http://`, `https://`, `mailto:` only — `javascript:`, `data:`, `vbscript:` rejected |
| **Malicious .ics files** | 2MB file size cap; `.ics`/`.ical` extension check; `BEGIN:VCALENDAR` content validation; max 50 events per import; max 1000 chars per field |
| **Input length abuse** | All `<input>` fields have `maxlength` attributes; values re-capped via `sanitizeText()` |
| **Color injection** | `safeColor()` validates strict 6-digit hex before use in any output |
| **Inline event handlers** | Zero `onclick`/`on*` attributes in HTML — all listeners attached via `addEventListener` |
| **Content Security Policy** | `<meta>` CSP blocks external scripts, eval, and external connections |
| **Referrer leakage** | `Referrer-Policy: no-referrer` prevents page URL leaking to calendar services |
| **ICS comment injection** | `-->` stripped from event titles before insertion into HTML comments |

> All processing is 100% client-side. No data is sent to any server.

---

## Usage

1. Download `add-to-calendar-generator.html`
2. Open it in any modern browser — no install, no server needed
3. **Add events** in the Events tab (or import a `.ics` file from the Import tab)
4. **Customize** button style and colors in the Style tab
5. Switch to the **Snippet** or **Full Email** tab on the right
6. Choose *One per event* or *Combined block* output mode
7. Hit **Copy** and paste into your Eloqua Custom HTML content block

---

## 📋 Output Modes

### One per event
Each event gets its own self-contained button block. Best when events appear at different points in an email.

```html
<!-- [Q3 Webinar] Add to Calendar -->
<table width="100%" ...>
  <tr><td align="center">
    <table ...><tr><td style="background-color:#0055CC;border-radius:4px;padding:13px 28px;">
      <a href="https://calendar.google.com/..." ...>📅 Add to Calendar</a>
    </td></tr></table>
    <p ...>Add to: Google | Outlook.com | Apple / iCal | Yahoo</p>
  </td></tr>
</table>
```

### Combined block
All events in one stacked table with a title and date row per event. Best for digest or newsletter-style emails.

---

## Calendar Provider Notes

| Provider | Method | Notes |
|---|---|---|
| Google Calendar | URL redirect | Opens Google Calendar pre-filled |
| Outlook.com | URL redirect | Opens Outlook.com compose view |
| Apple / iCal | `.ics` data URI | Works in Gmail and Apple Mail; may be blocked by corporate gateways — host the file on a CDN if needed |
| Yahoo Calendar | URL redirect | Opens Yahoo Calendar pre-filled |

> **Outlook on Windows** intercepts calendar-linked emails and shows its own native "Add to Calendar" prompt, hiding the provider link row. This is Outlook's built-in rendering behavior and cannot be overridden in HTML.

---

## ICS Import

1. Click the **Import .ics** tab
2. Drag and drop a `.ics` file, or click to browse
3. The parser extracts all events (up to 50) and lists them
4. Click **Add** next to any event to bring it into your event list

**Supported:** single-event and multi-event `.ics` files, RFC 5545 line folding, escaped characters (`\n`, `\,`, `\;`).

**Note:** Files using `TZID`-based timestamps (e.g. `DTSTART;TZID=America/New_York:...`) will parse correctly for date and time, but timezone offsets are not auto-converted. Verify times for non-UTC events.

---

## Email Client Notes

- Times are converted to UTC in all generated links. Enter start/end in your local time.
- Test in [Litmus](https://www.litmus.com) or [Email on Acid](https://www.emailonacid.com) before sending, especially for Outlook 2016/2019.
- Replace `<!-- UNSUBSCRIBE_LINK -->` in the full email template with your Eloqua unsubscribe merge field.

---

## Built With

- Vanilla HTML5, CSS3, and ES6+ JavaScript — no frameworks, no build step
- [DM Sans](https://fonts.google.com/specimen/DM+Sans) · [Fira Code](https://fonts.google.com/specimen/Fira+Code) · [Syne](https://fonts.google.com/specimen/Syne) via Google Fonts

---

## Version History

| Version | Highlights |
|---|---|
| v1.0 | Single event, live preview, snippet + full email output, style/color picker |
| v2.0 | Multi-event, `.ics` import, combined/separate output modes, responsive layout, OWASP hardening |

---

## 📄 License

MIT
