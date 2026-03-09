# Polyglot AI — Neural Translation Engine

> A sleek, privacy-first translation tool that runs entirely in the browser. No backend, no tracking, no server costs.

![Version](https://img.shields.io/badge/version-2.2-e8c97a?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-7ae8b4?style=flat-square)
![Zero Backend](https://img.shields.io/badge/backend-none-7ab4e8?style=flat-square)

---

## Overview

Polyglot AI is a single-file HTML translation app powered by the [MyMemory API](https://mymemory.translated.net/) (free, no key required) with optional [Google Translate API](https://cloud.google.com/translate) support for higher volume and quality. Everything runs client-side — API keys are stored in `localStorage` and sent directly to the provider, never to any intermediate server.

---

## Features

- **Instant translation** across 60+ languages with Ctrl+Enter shortcut
- **Dual engine support** — MyMemory (free tier) or Google Translate (API key)
- **Automatic fallback** from Google to MyMemory on API errors
- **Honest quality scoring** — derived from real Translation Memory match data, not fabricated numbers
- **Language detection** — shows what the API actually detected, clearly labeled; no fake probability bars
- **Batch translation** — paste multiple lines, translate all at once, export as JSON or TXT
- **RTL support** — Arabic, Hebrew, Persian, Urdu, Yiddish render right-to-left automatically
- **Text analysis** — word count, sentence count, readability level, formality estimate
- **Translation history** — last 30 translations, clickable to reload, persisted via `localStorage`
- **Text-to-speech** — listen to source or translated text via the Web Speech API
- **Export** — download individual translations as `.txt` or batch results as `.json` / `.txt`
- **Zero dependencies** — one `.html` file, no npm, no build step, no framework

---

## Getting Started

No installation required. Download the file and open it.

```bash
git clone https://github.com/your-username/polyglot-ai.git
cd polyglot-ai
open polyglot-fixed.html   # or just double-click it
```

That's it. The app works immediately using the free MyMemory API.

---

## API Configuration

### MyMemory (default, free)

Works out of the box with no setup. Limits:

| Plan | Daily Limit |
|---|---|
| No email | ~1,000 words/day |
| With email registered | ~10,000 words/day |

To raise your limit, go to **API Config** tab and enter your email in the MyMemory Email field.

### Google Translate (optional)

For unlimited translations at higher quality:

1. Enable the [Cloud Translation API](https://console.cloud.google.com/apis/library/translate.googleapis.com) in Google Cloud Console
2. Create an API key and restrict it to the Translation API
3. In the app, go to **API Config** → select **Google Translate** → paste your key → **Save**

Your key is stored only in your browser's `localStorage` and is sent exclusively to `translation.googleapis.com`.

---

## Quality Score

The **Translation Quality** score is derived from real signals in the MyMemory API response — not estimated or randomised:

- **TM Match Quality** — the best quality score across all Translation Memory hits returned by the API (0–100)
- **Match strength** — bonus for multiple high-quality matches backing the same translation
- **Length penalty** — short or single-word queries are scored more conservatively
- **Identity penalty** — if the output is identical to the input (a failed translation), the score is penalised

When no TM data is available (novel text with no prior matches), the score is capped at 55 and labeled **"No TM data — estimated quality"** so you know it's an approximation.

For Google Translate, a fixed high score is used with a small penalty for known weaker language pairs (Esperanto, Yiddish, Haitian Creole, etc.).

---

## Language Detection

Detection is shown honestly:

- **Auto-Detect mode** — displays the language the API actually returned, labeled "Detected"
- **Manual source selection** — shows your chosen language labeled "Selected" with a note that no detection was performed
- No fake confidence percentages or fabricated alternative-language probability bars

---

## Project Structure

```
polyglot-fixed.html   # The entire app — HTML, CSS, and JS in one file
README.md
```

The app is intentionally a single file for maximum portability. Drop it on any static host (GitHub Pages, Netlify, S3) or just open it locally.

---

## Browser Support

Works in any modern browser. Requires:

- `fetch` API (all modern browsers)
- `localStorage` (for history and API key storage)
- `SpeechSynthesisUtterance` (for listen/TTS — gracefully disabled if unavailable)
- `navigator.clipboard` (for copy — requires HTTPS or localhost)

---

## Privacy

- No analytics, no telemetry, no cookies
- API keys never leave your browser except in direct calls to the provider you configured
- Translation history is stored only in your own `localStorage` and never transmitted anywhere
- The app makes no requests except to `api.mymemory.translated.net` or `translation.googleapis.com`

---

## Roadmap

- [ ] DeepL API support
- [ ] LibreTranslate (self-hosted) engine option
- [ ] Glossary / custom terminology management
- [ ] Side-by-side diff view for iterative editing
- [ ] PWA / offline mode

---

## License

MIT .
