# localchat

A lightweight, real-time chat app you can host on Netlify for free. No backend, no database, no accounts — just open the URL, enter your name, and start talking.

Built for local use cases like an office, a building on shared WiFi, or just testing with multiple browser tabs.

---

## Features

- **Servers** — separate chat channels (like Discord servers). Three defaults: `general`, `random`, `announcements`. Anyone can create more.
- **Live presence** — see who's online in the sidebar. The member list updates in real time and clears anyone who closes the tab.
- **No signup** — just enter a name (letters only) and you're in.
- **Persistent name** — your name is saved to the browser so you don't retype it each visit.
- **Rename anytime** — click your name in the bottom-left corner.
- **Works across tabs** — open the same URL in two tabs with different names to test it yourself.

---

## How it works

Messages and presence are synced using [Gun.js](https://gun.eco/) — a decentralized peer-to-peer sync library that runs entirely in the browser. There's no server you need to run. Gun relays data through free public peers and syncs it across every connected client instantly.

Messages older than 24 hours are ignored. Presence pings every 4 seconds and anyone inactive for 12+ seconds is removed from the online list.

---

## Deploy to Netlify

### Option 1 — Drag and drop (easiest)

1. Go to [netlify.com/drop](https://netlify.com/drop)
2. Drag your `index.html` file onto the page
3. Netlify gives you a live URL instantly

### Option 2 — From GitHub

1. Push this repo to GitHub
2. Go to [netlify.com](https://netlify.com) and click **Add new site → Import from Git**
3. Connect your repo — no build settings needed
4. Deploy

---

## Usage

1. Open the Netlify URL in your browser
2. Type your name (letters only) and hit **start chatting**
3. Pick a server from the left sidebar
4. Start messaging — anyone else on the same URL in the same server will see it live

To test alone, open two browser tabs with different names.

---

## File structure

```
index.html    ← the entire app, single file
README.md     ← this file
```

That's it. No dependencies to install, no build step.

---

## Tech

| Thing | What it does |
|---|---|
| [Gun.js](https://gun.eco/) | Real-time P2P data sync |
| IBM Plex Mono / Sans | Typography |
| Vanilla JS | Everything else |

---

## Customisation

- **Change the default servers** — find `DEFAULT_SERVERS` near the top of the script and edit the array
- **Change the app name** — search for `localchat` in the HTML and replace it
- **Adjust presence timeout** — change `PRESENCE_TTL` (ms) to make members drop off faster or slower

---

## Limitations

- Messages are stored on Gun's public relay peers — don't use this for anything sensitive
- No message history beyond the current session if the Gun peers restart
- No moderation or authentication — it's open to anyone with the URL

---

## License

MIT — do whatever you want with it.
