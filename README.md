# TalkMate 💬

**English** · [Tiếng Việt](README.vi.md)

A personal language-learning app that runs on your phone as a PWA: chat with an AI buddy **without fear of making mistakes**, build vocabulary with Anki-style spaced repetition, practice listening at exactly your level, and speak through your microphone — with a weekly study plan the AI writes from your real learning data.

**Supported languages:** 🇬🇧 English · 🇨🇳 Chinese · 🇯🇵 Japanese · 🇰🇷 Korean · 🇫🇷 French · 🇪🇸 Spanish — pick one in ⚙️ Settings; each language keeps its own word book and TTS voice. Chinese mode adds **stroke-order handwriting practice** for Hanzi (trace each stroke with your finger, graded stroke by stroke).

No server, no accounts — it runs on your own free Gemini API key, and all learning data stays on your device. The app's interface and explanations are in Vietnamese (built for Vietnamese native speakers).

## Features

- **💬 Chat**: the AI is a patient conversation buddy that never interrupts to correct you mid-conversation — tap "End session" to get a gentle review instead. Tap any word in an AI message to look it up and save it to your word book. Stuck? Tap 💡 for three suggested replies with translations. Tap 🎤 to speak — the AI listens to your audio directly, replies, and reads its answer aloud.
- **🎧 Listening**: the AI generates listening exercises (dialogue / story / news) matched to your level and interests, weaving in the words you're currently studying. Transcript is blurred for blind listening first, playback speed 0.6x–1.2x, and a 3-question quiz at the end.
- **📚 Vocabulary**: spaced-repetition review (SM-2: Again / Hard / Good / Easy), automatic pronunciation on card flip, manual word entry. In Chinese mode: a ✍️ handwriting panel — watch the stroke-order animation, then trace it yourself.
- **🧭 Study plan**: daily streak 🔥, a 3-item daily checklist, and a 7-day plan generator — the AI reads your actual data (words you keep forgetting, past sessions) and is explicitly forbidden from generic advice.
- **🌱 Foundation mode** (for adults restarting from zero): ultra-simple sentences with a Vietnamese translation under each one; you can even type in Vietnamese and the AI shows you how to say it. Font size adjustable up to extra large.

## Try it on a computer

Open `app/index.html` in Chrome/Edge. Go to ⚙️ Settings → paste your API key (free at [aistudio.google.com](https://aistudio.google.com) → API keys) → tap 🔌 Test connection. Note: the microphone only works over https (the GitHub Pages build).

## Install on your phone (GitHub Pages)

1. Push the code to GitHub (below) — the repo must be **Public**.
2. On GitHub: **Settings → Pages → Source: Deploy from a branch → Branch `main`, folder `/ (root)` → Save**.
3. Wait ~1 minute, then open on your phone: `https://chuyennm.github.io/TalkMate/`
4. Choose **"Add to Home Screen"** — the app gets an icon and runs full-screen like a native app.
5. Paste your API key in ⚙️ Settings (once per device). Allow microphone access the first time you tap 🎤.

## Pushing code

First time:

```
git init
git add .
git commit -m "TalkMate"
git branch -M main
git remote add origin https://github.com/chuyennm/TalkMate.git
git push -u origin main
```

After that: `git add . && git commit -m "..." && git push`. Installed phones pick up the new version after reopening the app once or twice.

## Data & cost

- Your API key and all learning data live only in your device's browser — never in the code, so a public repo is safe.
- Using two phones? The **Export/Import** buttons in ⚙️ Settings move your word book and progress as a JSON file.
- Gemini's free tier covers 30–60 minutes of study per day. Browser TTS voices: free. GitHub Pages hosting: free.

## Project layout

```
TalkMate/
├── index.html            ← redirects to app/
├── PLAN.md               ← architecture, dev history, roadmap (Vietnamese)
└── app/
    ├── index.html        ← the entire app (HTML + CSS + JS, one file)
    ├── manifest.webmanifest
    ├── sw.js             ← service worker (offline shell cache)
    └── icon-192.png / icon-512.png
```
