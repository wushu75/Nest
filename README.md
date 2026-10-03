<p align="center">
  <img src="public/icons/icon128.png" alt="Nest" width="80" height="80">
</p>

<h1 align="center">Nest for Etsy</h1>

<p align="center">
  <strong>Save, organise, and share your Etsy finds — privately.</strong><br>
  A free, open-source Chrome extension that gives Etsy the collection &amp; sharing features it's always needed.
</p>

<p align="center">
  <a href="#install"><img src="https://img.shields.io/badge/Add_to-Chrome-F1641E?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Add to Chrome"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Manifest-V3-F1641E?style=flat-square" alt="Manifest V3">
  <img src="https://img.shields.io/badge/License-MIT-F1641E?style=flat-square" alt="MIT License">
  <img src="https://img.shields.io/badge/Tracking-None-6B7F5C?style=flat-square" alt="No tracking">
  <img src="https://img.shields.io/badge/Accounts-None-6B7F5C?style=flat-square" alt="No accounts">
  <img src="https://img.shields.io/badge/Price-Free_forever-7BA3AD?style=flat-square" alt="Free forever">
</p>

---

## What is Nest?

Nest adds the collection, sharing, and discovery tools that Etsy has been missing. Everything runs in your browser — no accounts, no servers, no tracking. Your data stays on your device unless you choose to share it.

---

## Features

### 🪺 Smart Nests

- **One-click save** — A save button on every Etsy listing card, or press `N` to quick-save
- **Colour-coded collections** — Create named nests with custom colours and icons
- **Notes & tags** — Annotate any saved item; tags are searchable across all nests
- **Drag & drop** — Reorder items within a nest

### 🔗 Share with anyone

- **No extension needed** — Recipients open a beautiful viewer page in any browser
- **No server involved** — Data is encoded in the URL fragment (browsers never send fragments to servers)
- **Share codes** — Paste a `nest1.` code if you'd rather send text
- **Image export** — Download a 1080×1350 collage, sized for Instagram or WhatsApp
- **JSON export** — Full backup, importable by any Nest user
- **Web Share API** — Use your device's native share menu

### 🎨 Mood boards

- **Free-form canvas** — Drag items, notes and colour swatches onto a visual board
- **Rotate & layer** — Tilt elements, bring to front, arrange freely
- **Export** — Download a crisp 2× PNG

### 🎁 Style & gift matching

- **Style profile** — Nest learns your taste from saved items and browsing (100% local, never leaves your device)
- **"More like this"** — Personalised Etsy search suggestions based on your style
- **Gift ideas** — Pick a persona (Mum, Partner, Best friend…) and get tailored search suggestions

### 🔍 Buyer insights

- **Review summary** — Key pros and cons extracted from review text
- **Shipping & eco signals** — Free shipping, eco-friendly, fast delivery badges
- **Shop signals** — Star seller, established shop indicators

### ⚡ Quality of life

- **Sticky filters** — Etsy's filter bar stays visible while scrolling
- **Compact density** — Tighter grid for power browsers
- **Dark mode** — System-aware or manual toggle
- **Keyboard shortcuts** — `N` save · `Shift+N` open manager · `Alt+Shift+N` anywhere
- **Price drop & restock alerts** — Background checks every 3 hours, browser notifications

---

## Install

<h3 id="install">From the Chrome Web Store</h3>

> Coming soon — the extension is currently in review.

### From source (development)

```bash
git clone https://github.com/wushu75/Nest.git
cd Nest
npm install
npm run build
```

Then in Chrome:

1. Go to `chrome://extensions`
2. Enable **Developer mode** (top right)
3. Click **Load unpacked** → select the `dist/` folder

For live rebuilds while developing:

```bash
npm run watch
```

---

## Project structure

```
nest/
├── public/               Static assets copied into dist/
│   ├── manifest.json     MV3 manifest
│   ├── popup/            Toolbar popup HTML & CSS
│   ├── manager/          Manager page HTML & CSS
│   └── icons/            Extension icons
├── src/
│   ├── background/       Service worker (alarms, message bus, price checks)
│   ├── content/          Content script (card buttons, insights overlay)
│   ├── popup/            Toolbar popup logic
│   ├── manager/          Full-page nest manager
│   ├── viewer/           Public share viewer (self-contained HTML)
│   ├── shared/           Shared modules
│   │   ├── types.ts      Core data model
│   │   ├── db.ts         Dexie / IndexedDB wrapper
│   │   ├── store.ts      Item CRUD operations
│   │   ├── settings.ts   Settings via chrome.storage.local
│   │   ├── messages.ts   Typed message bus
│   │   ├── listing.ts    Listing data extraction
│   │   ├── share-codec.ts Share encoding / decoding
│   │   ├── style-engine.ts Style profiling & suggestions
│   │   ├── canvas.ts     Image export rendering
│   │   ├── icons.ts      SVG icon set
│   │   ├── dom.ts        DOM helpers & hyperscript
│   │   └── config.ts     Build-time defaults
│   └── ui/
│       ├── theme.css     Shared design tokens
│       └── art.ts        Hand-drawn SVG illustrations
├── build.mjs             esbuild build script
├── tsconfig.json
├── package.json
├── LICENSE               MIT
└── PRIVACY.md            Privacy policy
```

---

## Architecture

| | |
|---|---|
| **Runtime** | Manifest V3 — service worker, no persistent background page |
| **Language** | TypeScript in strict mode, no framework, plain DOM via `h()` hyperscript |
| **Storage** | Dexie.js wrapping IndexedDB for all local data |
| **Bundler** | esbuild — fast builds, IIFE format for content scripts |
| **Accounts** | None. Everything stored locally in IndexedDB + chrome.storage.local |
| **Privacy** | Share links encode data in URL fragments (never sent to servers) |

---

## How sharing works

Nest's sharing system is designed so that **no server ever sees your data**:

```
Your nest
  → Pack into compact arrays (short keys, image prefix stripping)
  → Compress with the browser's built-in deflate-raw
  → Encode as base64url
  → Place in the URL fragment (#n=…)
```

Browsers never send the fragment to servers, so even the static page hosting the viewer never sees what's in your nest. The same string works as a pasteable `nest1.` share code.

### Optional: share server

For short links and collaborative nests, you can deploy the optional Cloudflare Worker. This is entirely opt-in and self-hostable — no share server is configured by default.

---

## Permissions

| Permission | Why |
|---|---|
| `storage` | Save your settings locally |
| `alarms` | Schedule price/restock checks |
| `notifications` | Alert you to price drops and restocks |
| `etsy.com` host | Read listing data from pages you visit |
| `i.etsystatic.com` host | Load listing images for mood board exports |

No optional permissions are requested unless you configure a share server.

---

## Contributing

Contributions welcome! The codebase is intentionally framework-free and readable.

```bash
npm run watch     # live rebuilds
npm run typecheck # TypeScript checks
npm run zip       # package for distribution
```

Load the `dist/` folder in Chrome as an unpacked extension, and changes rebuild automatically.

---

## Privacy

See [PRIVACY.md](PRIVACY.md) for the full privacy policy. The short version: **Nest collects nothing. There is no analytics, no telemetry, no tracking. Your data lives in your browser and nowhere else.**

---

## License

[MIT](LICENSE) — do whatever you want with it.

<p align="center">
  <br>
  <img src="https://img.shields.io/badge/Made_with-🧡-F1641E?style=for-the-badge" alt="Made with love">
  <br><br>
  <sub>Nest is not affiliated with Etsy, Inc.</sub>
</p>
