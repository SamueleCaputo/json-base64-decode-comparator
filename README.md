# JSON & Base64 Decode Comparator

A single-page web app to compare two JSON payloads **or base64-encoded JSON**, normalize them ignoring order, and display a **side-by-side diff** with:

- line numbers,
- highlighted differences,
- empty highlighted lines for missing fields on the opposite side,
- synchronized scrolling,
- copy buttons for the normalized JSON.

Ideal for backend developers, API integrators, QA engineers, and anyone working with complex JSON payloads.

---

## ✨ Features

### Input & base64 support

- Paste **raw JSON** in each input area.
- Or paste a **base64 string** that represents a JSON document.
- For each side, the app:
  1. Tries to parse the input as JSON.
  2. If that fails, it tries to **base64 decode** the input and parse the decoded text as JSON.
  3. If both fail, an error message is shown.

### Normalization (order-insensitive)

To avoid false differences caused only by ordering, both JSON objects are normalized before comparison:

- Object keys are **sorted alphabetically**.
- Arrays are **sorted** using a structural “freeze” function (so array content is compared by value, not by original order).
- Special handling for arrays of objects:
  - If a common unique key exists on both sides (e.g. `id`, `uuid`, `code`, `key`),
  - The app uses that key to **align elements by ID**, so reordering doesn’t matter.

### Bidirectional diff

- The diff walks both structures recursively.
- Differences are tracked for:
  - Type mismatches,
  - Missing keys/indices on one side,
  - Different primitive values.
- Diff paths are mapped back to the **formatted text lines**, so only affected lines are highlighted.

### Aligned side-by-side view

To make visual comparison easier:

- Both normalized JSONs are rendered in side-by-side panels.
- Each line has a **line number**.
- Differences are highlighted in **red**.
- When one side has more lines (extra fields, extra array items), the other side gets **empty highlighted lines** so:
  - Diff blocks stay aligned vertically,
  - It’s clear which fields are missing on which side.

### UI & UX

- Responsive layout using **Bootstrap 5**.
- Two panels with different background colors for easy visual separation (left vs right).
- Compact line height to show as many lines as possible.
- Copy buttons above each result panel:
  - Quickly copy the normalized JSON to your clipboard.

### SEO & accessibility (optional but included)

- HTML5 semantic structure: `header`, `main`, `section`, `footer`.
- Basic SEO meta tags: `title`, `description`, `canonical`, Open Graph and Twitter Card tags.
- JSON-LD structured data for:
  - `WebApplication` (describing the tool),
  - `FAQPage` (common questions about comparing JSON).
- ARIA attributes on key elements (e.g. live region for comparison result message).

---

## 🏗 Tech stack

- **HTML5** – single-page app (`index.html`)
- **CSS3** – custom styles + [Bootstrap 5](https://getbootstrap.com/)
- **Vanilla JavaScript** – no frameworks, no build step
- JSON-LD for structured data / SEO

Everything (markup, style, logic) lives in `index.html` for a super simple deployment.

---

## 📁 Project structure

```text
.
├── index.html   # Main page with HTML, CSS and JS
└── README.md    # This file
