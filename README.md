# ✍️ SCRIBE | Engineering Grade Markdown Engine

A high-performance, zero-dependency Markdown parser and live-preview editor. Built with vanilla JavaScript, focusing on regex-based parsing and secure DOM manipulation.

## ⚙️ Technical Architecture: The Parser
Unlike many editors that rely on external libraries like `marked.js`, Scribe uses a custom-built **Regex Engine** to transform raw text into sanitized HTML.

### Supported Syntax & Logic:
The parser processes text through a sequence of transformations:

1. **Escaping & Sanitization:** First, raw input is escaped to prevent unintended HTML rendering, followed by a `purifier()` function that strips malicious `script` and `iframe` tags.
2. **Headers:** - `# Header` -> `<h1>`
   - `## Header` -> `<h2>`
3. **Blockquotes:** Detected via `^&gt; (.*$)` pattern.
4. **Code Blocks:** Managed via a placeholder system. Multi-line blocks (```) are extracted, stored in an array, and re-injected after text processing to prevent inner-code corruption.
5. **Tables:** Custom pipe-delimited logic `| Cell |` that dynamically generates `<table>` rows.
6. **In-line Styling:**
   - `**Bold**` -> `<strong>`
   - `*Italic*` -> `<em>`
   - `` `Code` `` -> `<code>`

## 🛡️ Security Features
- **DOM Purifier:** A dedicated function that scans the generated HTML for inline event handlers (e.g., `onclick`) and sensitive tags, ensuring a safe sandbox for the preview pane.
- **State Persistence:** Implements `localStorage` API to ensure data recovery across sessions without server-side storage.

## 🛠 Features
- **Monolith Design:** Entire engine, logic, and UI contained in a single-file architecture for zero-latency.
- **MD Export:** Blob-based download system for generating `.md` files on the fly.
- **Clipboard API:** One-click copy functionality for code snippets within the preview.

## 🚀 Deployment
This is a vanilla web application. No build step required.
1. Open `index.html` in any modern browser.
2. Start writing technical documentation.
