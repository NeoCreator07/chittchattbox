# localchat

A real-time chat app you can host on Netlify for free. No backend code, no server to run — just a single `index.html` powered by **Firebase Realtime Database**. Works across devices, browser tabs, and anyone on the same network visiting your URL.

---

## Features

- **Servers** — separate chat channels. Three defaults (`general`, `random`, `lounge`), anyone can add more
- **Live presence** — see who's online and which server they're in, updates in real time
- **Reliable delivery** — built on Firebase (Google infrastructure), not flaky public peers
- **Auto-reconnect** — a status bar appears if the connection drops and clears when it restores
- **Disconnect cleanup** — when someone closes the tab they're removed from the online list immediately
- **No accounts** — enter a name (letters only) and you're in
- **Name persists** — saved to your browser so you don't retype it
- **Rename anytime** — click your name in the bottom-left

---

## How it works

Messages and presence are stored in **Firebase Realtime Database** — Google's infrastructure. When you push a message it's written server-side and every connected client receives it instantly via a persistent WebSocket. There are no third-party relay peers involved, so messages never get lost.

Presence uses Firebase's `onDisconnect()` hook — your entry is automatically deleted the moment your browser tab closes, even if the page crashes.

---

## Setup (one time, ~5 minutes)

You need a free Firebase project. The config is entered in the app itself and saved to your browser — the `index.html` file stays generic and shareable.

### Step 1 — Create a Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → give it a name → disable Google Analytics → Create
3. In the left menu go to **Build → Realtime Database** → **Create database**
4. Choose a region → select **Start in test mode** → Enable

### Step 2 — Get your config

1. Go to **Project Settings** (gear icon, top-left) → **General** tab
2. Scroll down to **Your apps** → click the **</>** (Web) icon
3. Register the app (nickname doesn't matter)
4. Copy the three values you need:
   - `apiKey`
   - `projectId`
   - `databaseURL` (looks like `https://your-project-default-rtdb.firebaseio.com`)

### Step 3 — Enter config in the app

Open your Netlify URL. You'll see a setup screen asking for those three values. Paste them in and click **Connect**. Done — you won't see this screen again on that browser.

> Anyone else using the app does the same one-time setup with the same values. Put the values in your README or share them with your team so everyone uses the same database.

---

## Deploy to Netlify

### Option 1 — Drag and drop

1. Go to [netlify.com/drop](https://netlify.com/drop)
2. Drag `index.html` onto the page
3. You get a live URL instantly

### Option 2 — From GitHub

1. Push this repo to GitHub
2. Go to [netlify.com](https://netlify.com) → **Add new site → Import from Git**
3. Select your repo — no build settings needed
4. Deploy

---

## File structure

```
index.html    ← entire app, single file
README.md     ← this file
```

No `npm install`, no build step.

---

## Tech

| | |
|---|---|
| [Firebase Realtime Database](https://firebase.google.com/products/realtime-database) | Real-time sync & presence |
| DM Mono / Syne | Typography |
| Vanilla JS | Everything else |

---

## Customisation

**Change default servers** — find the `DEFAULTS` array near the top of the `<script>` tag:
```js
const DEFAULTS = ['general','random','lounge'];
```

**Adjust message history** — messages older than 24 hours are filtered out on load. Change the `24` in `24 * 60 * 60 * 1000` to any number of hours.

**Lock down the database** — once you've deployed, go to Firebase Console → Realtime Database → Rules and tighten the rules so only your Netlify domain can write. The default test mode rules expire after 30 days anyway.

---

## Limitations

- Firebase test mode rules expire after 30 days — update them before then
- No message encryption — don't use for sensitive content
- No moderation — open to anyone with the URL and Firebase config
- Free Spark plan: 100 simultaneous connections, 1 GB storage, 10 GB/month transfer (plenty for a building chat)

---

## License

MIT
