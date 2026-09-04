# AuraGuide

AI companion for smart glasses — live awareness, proactive nudges, on-demand guidance.

Phone camera is the live view today. Bluetooth earbuds (or speaker) for voice. Meta / Google / Frame / other glasses pair as Bluetooth audio until partner camera APIs exist. AuraGuide is **its own model**; it does not socket into Meta’s onboard assistant.

## Download the beta (phone)

**[Download AuraGuide-beta.apk](https://github.com/xavierscudd-agentchaos/auraguide/releases/download/v0.7.0-beta/AuraGuide-beta.apk)** — or open the [Releases](https://github.com/xavierscudd-agentchaos/auraguide/releases/tag/v0.7.0-beta) page and tap the `.apk` under **Assets**.

On GitHub: repo page → right side **Releases** → **AuraGuide 0.7.0-beta** → **Assets** → `AuraGuide-beta.apk`.

## What’s in this repo

```
web/                 PWA (HTML/CSS/JS)
server/              Bun vision + guide API (`index.js`)
android/             WebView wrapper (minSdk 24)
TESTERS.md           Sideload notes for phone + Meta testers
android/BUILD.md     How to package the APK
```

## Run the web app

Needs [Bun](https://bun.sh). From `server/`:

```bash
bun run index.js
```

`DASHBOARD_PORT` defaults to `3000`. Open `http://localhost:3000`.

Set `ANTHROPIC_API_KEY` (or `ANTHROPIC_AUTH_TOKEN` + `ANTHROPIC_BASE_URL`) so `/api/guide` can see camera frames.

The Android APK loads `file://` assets, so it cannot hit `localhost`. Point it at a public HTTPS URL:

```js
localStorage.setItem("auraguide-guide-url", "https://your-host/api/guide");
```

Or prepend that URL in `web/app.js` (`GUIDE_URLS`).

## Android APK (sideload)

Universal Android 7+ (Motorola, Samsung, Pixel, Razr / foldables). Not a Play Store build unless you confirm.

```bash
bash android/build.sh
```

Output: `dist/AuraGuide-beta.apk` (debug-signed). See `android/BUILD.md`.

Uninstall any older AuraGuide first. Allow unknown sources. If Play Protect warns, that is expected for a debug key.

## Try it

1. Start a session (▶). Allow camera + mic. Volume up.
2. It **watches quietly**. It does not narrate the room.
3. **Talk to Aura** / 👁 / On-Demand — it answers from the live frame.
4. Settings → Voice — Aria, Juniper, Nova, Rowan, Sage (phone neural TTS, not celebrity clones).
5. Settings → Gets to know you — name, notes, people, patterns (on-device).

## GitHub

This folder is a git repo. Create an empty GitHub repository, then:

```bash
cd auraguide
git remote add origin git@github.com:YOUR_USER/auraguide.git
git push -u origin main
```

Do not commit `android/debug.keystore` or built APKs.
