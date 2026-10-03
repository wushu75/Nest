# Privacy Policy

**Nest for Etsy** is a privacy-first Chrome extension. This document explains exactly what happens with your data — and more importantly, what doesn't.

---

## The short version

Nest collects **nothing**. There is no analytics, no telemetry, no tracking, no cookies, no accounts. Your data lives in your browser's local storage and never leaves your device unless you explicitly choose to share.

---

## What stays on your device

Everything:

- Your collections (nests) and saved items
- Notes and tags you add to items
- Mood boards and their layouts
- Your browsing history on Etsy (used for style profiling)
- Your style profile and preferences
- All settings and configuration

All of this is stored in your browser's **IndexedDB** and **chrome.storage.local**. These are local storage mechanisms built into your browser. The data never leaves your device unless you explicitly share it.

---

## What gets sent to Etsy

When you browse Etsy with the extension installed, Nest reads the page you're already viewing to extract listing data (title, price, images, reviews). This is the same data your browser has already loaded — Nest simply reads it from the page DOM.

Nest does **not** make any additional network requests to Etsy beyond what your browser already does, with one exception:

- **Price and restock checks**: For items you've saved, Nest periodically fetches the listing page in the background (every 3 hours) to check if the price has dropped or the item has come back in stock. These are standard page fetches, identical to you visiting the page yourself.

---

## What happens when you share

### Inline links and share codes (default)

When you share a nest via link or share code:

1. Your nest data is compressed and encoded into the **URL fragment** — the part of the URL after the `#` symbol
2. Browsers **never send fragments to servers** — this is part of the HTTP specification
3. No server — not even the one hosting the viewer page — ever sees your data
4. The data travels only through whatever channel you paste the link into (a message, an email, social media, etc.)

### Image export

When you export a collage image:

- The image is generated entirely in your browser using an OffscreenCanvas
- The resulting PNG file is saved directly to your device
- No data is sent anywhere

### JSON export

- Your data is serialised to a JSON file and saved to your device
- No data is sent anywhere

### Short links and collaborative sharing (optional)

If you choose to configure a share server (this is **off by default** and requires manual setup):

- The contents of the shared nest are sent to that server
- The server software is open source and self-hostable
- You control where the data goes
- No share server is configured or suggested by default

---

## Third-party services

Nest does **not** use:

- ❌ Analytics (no Google Analytics, no Mixpanel, no Amplitude, nothing)
- ❌ Telemetry or crash reporting
- ❌ Tracking pixels or web beacons
- ❌ Cookies of any kind
- ❌ Third-party SDKs or libraries that phone home
- ❌ Account systems or authentication
- ❌ Advertising networks
- ❌ A/B testing platforms

The only external service Nest communicates with is **Etsy itself** — and only the pages you visit plus periodic price checks on your saved items.

---

## Chrome permissions explained

| Permission | What it does | Why Nest needs it |
|---|---|---|
| `storage` | Access to `chrome.storage.local` | Store your settings (dark mode, density, display name) |
| `alarms` | Schedule periodic background tasks | Run price/restock checks every 3 hours and sync collaborative nests |
| `notifications` | Show browser notifications | Alert you when a saved item drops in price or comes back in stock |
| Host: `etsy.com` | Read pages on etsy.com | Extract listing data (title, price, images) from pages you visit |
| Host: `i.etsystatic.com` | Fetch images from Etsy's CDN | Load listing images for mood board and collage exports (keeps the canvas untainted for PNG export) |

**Optional host permissions** are only requested if you configure a share server. They are never requested by default.

---

## Data storage details

### IndexedDB (via Dexie.js)

| Table | What it stores |
|---|---|
| `nests` | Your nest names, colours, icons, ordering |
| `items` | Saved listings — title, price, image URL, notes, tags |
| `boards` | Mood board layouts — element positions, rotations, z-order |
| `views` | Pages you've viewed on Etsy (used locally for style profiling) |

### chrome.storage.local

Stores your settings: dark mode preference, grid density, display name, viewer URL, share server URL, and onboarding status.

---

## Data deletion

You have full control over your data:

- **Uninstalling the extension** deletes all data (IndexedDB and chrome.storage.local are removed)
- **Settings → Clear browsing data** removes your Etsy browsing history (used for style profiling) without affecting your saved nests
- **Export as JSON** lets you back up everything before deleting
- **Import from JSON** lets you restore from a backup

---

## Children's privacy

Nest does not knowingly collect any information from anyone, including children under 13. There is no data collection mechanism in the extension.

---

## Changes to this policy

If this privacy policy changes, the update will be published in the GitHub repository. Since Nest collects no data, there is very little reason for this policy to change.

---

## Source code

Nest is fully open source under the MIT licence. You can verify every claim in this policy by reading the source code:

**[github.com/wushu75/Nest](https://github.com/wushu75/Nest)**

---

## Contact

This is an open-source project. If you have questions about privacy or anything else, [open an issue on GitHub](https://github.com/wushu75/Nest/issues).
