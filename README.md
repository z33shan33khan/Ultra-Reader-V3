# Ultra Reader v3

A single-file, offline-friendly reading app with natural text-to-speech. Drop in a novel, import an EPUB/PDF, or open a web chapter — Ultra Pro Reader reads it aloud with word-level highlighting, chapters, bookmarks, and a built-in mini browser.

Everything lives in one `Ultra-Reader-v3.html` file: no build step, no server, no dependencies to install.

---

## Features

### Reading & speech

- **Read aloud** with the browser's built-in voices, with play, pause, stop, previous/next sentence, and previous/next page.
- **Karaoke-style highlighting** — choose Word by Word, Entire Sentence, Sentence + Word, Entire Paragraph, or Paragraph + Word.
- **Click to read from anywhere** — tap any word or sentence in the page to start or resume from that point.
- **Auto-scroll** keeps the spoken line in view.
- **Auto-continue** to the next chapter (or the next web chapter) when the current one finishes.
- **Time left estimate** and page counter for the current chapter.
- **100+ voice languages**, with automatic matching of an installed voice.

### Make the voice sound right

- **Skip words & punctuation** — symbols like `—`, `*`, `【】`, `♪` are silently skipped without changing the visible text. Named entries like `comma`, `period`, or `dash` are supported too.
- **Pronunciation fixes** — built-in Chinese pinyin rules (`Xin → Shin`, `Qing → Ching`, `Cai → Tsai`, …), plus your own find-and-replace rules. Combined names such as `Qingcheng` are split into syllables automatically.
- **Test box** previews exactly what the voice will say before you commit a rule.
- **Speed control** from 0.5× to 3× with quick presets, and **voice selection** per language.

### Library

- **Import** `.txt`, `.md`, `.html`, `.epub`, and `.pdf` files, paste raw text, or pull a chapter straight from a website.
- Automatic **chapter detection** (`Chapter`, `Ch`, `Episode`, `Part`, number forms, and Chinese numerals).
- **Search and sort** by title, chapters, or recently added.
- **Collapsible tree view** of books and chapters, with expand/collapse all.
- **Bookmarks** store the book, chapter, page, and text excerpt.
- **Reading progress is saved** per book and restored the next time you open it.

### Mini browser

- Up to **8 tabs** with back, forward, reload, home, and a quick-links start page.
- **Reader view** extracts a clean article from a page; **Live view** loads the real site (needed for signing in).
- Multi-source fetching with automatic fallback, so a blocked source doesn't stop the extraction.
- **Read page** sends the extracted article to the reader, and web chapter navigation detects previous/next chapters.
- Paste a **YouTube** link to watch it in place.
- Open any page in your normal browser with one click.

### Appearance

- Warm **dark** and **paper-light** themes.
- Adjustable font family (including Noto Nastaliq Urdu, Noto Serif SC, Noto Sans JP, and Amiri) and font size.
- Pick from installed system fonts via the font browser.
- Optional **auto-translate** of pages using Google Translate.
- Fully responsive layout; on phones the playback bar becomes a bottom dock.

### Library contents

A complete sample novella, *The Jade Sword Chronicle* (3 chapters), is included on first launch so you can try everything immediately.

---

## Getting started

1. Download or clone the repository.
2. Open `Ultra-Reader-Finished-version.html` in a modern browser.
3. Press **Play** to hear the sample book, or use the buttons at the top to open a file, paste text, or load a web page.

That's it — there is no install step.

### Recommended browsers

| Browser | Support |
| --- | --- |
| Chrome / Edge (desktop & Android) | Best — Web Speech API, EPUB, PDF |
| Safari (macOS / iOS) | Works, voice list varies |
| Firefox | Reading works; speech support depends on OS voices |

> **Note:** Reading aloud uses the Web Speech API (`speechSynthesis`), which is available in all current major browsers. If no voices appear, make sure voices are installed in your operating system.

### Internet access

The app itself is fully local, but a few optional features use the network:

- Google Fonts and the PDF.js library are loaded from CDNs.
- **Auto-translate** uses Google Translate.
- **Web page fetching** goes through public CORS proxies.
- **YouTube** playback and external page loading need a connection.

Without a connection, reading, imports, the library, and settings all still work.

---

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Space` | Play / pause |
| `←` / `→` | Previous / next page |
| `S` | Stop reading |
| `B` | Add bookmark |
| `Esc` | Close the drawer or any dialog |

Shortcuts are ignored while typing in an input, textarea, or select.

---

## How it works

- **Pagination** splits chapters into pages of roughly 420 words, then wraps words in spans for highlighting.
- **Speech sync** uses `SpeechSynthesisUtterance` boundary events, with the spoken text mapped back to original character offsets so highlighting stays accurate even after skip rules and pronunciation fixes.
- **Chapters** are detected with pattern matching and a small Chinese-numeral converter.
- **EPUB** parsing reads the ZIP container directly using `DecompressionStream`.
- **PDF** text is extracted page by page with PDF.js.
- **Storage** uses `localStorage` for settings, library, bookmarks, and progress — nothing is uploaded.

### Project structure

```text
Ultra-Reader-Finished-version.html   # the whole app: HTML + CSS + JavaScript
README.md
```

---

## Known limitations

- Voice quality and availability come from the operating system, not the app.
- Some sites block embedding or CORS proxies; Reader view usually gets around this, Live view may not.
- Signing in to a site only works in Live view, and only where the site permits embedding.
- Importing very large books can exceed browser `localStorage` limits; the app warns you and keeps the book for the session.
- Auto-translate sends page text to Google Translate; leave it off if you need to stay fully offline.

---

## License

Add a `LICENSE` file (for example, MIT) before publishing the repository if you want to grant reuse rights.
