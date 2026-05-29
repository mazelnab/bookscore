# 📚 BookScore

**Find the book that fits your *actual* mood — not just "good books," but books that match what you need right now.**

BookScore is a single-file web app that searches real book/audiobook metadata, scores each title with Claude AI across three independent dimensions, and drops it into a ranked, interactive dashboard. It's built on one idea:

> A great book at the wrong time is a bad recommendation.

Goodreads ranks by star rating. StoryGraph ranks by mood and pace. **BookScore ranks by what you actually need right now** — blending *vibe*, *quality*, and *life-fit* into a single Composite Rank.

---

## The scoring model

Every book gets a **Composite Rank (0–100)** built from three independent layers:

```
Composite = Vibe Match × 0.35  +  Quality × 10 × 0.40  +  Fit × 0.25
```

| Layer | Weight | What it measures |
|---|---|---|
| **🎭 Vibe Match** | 35% | How well the book's mood, tone, and pace match what you're craving *right now*. Acts as a filter — a slow-burn masterpiece shouldn't win when you asked for fast-paced. |
| **⭐ Quality** | 40% | Six Claude-scored dimensions: plot, character depth, worldbuilding, narration/prose, entertainment, emotional resonance — weighted by *your* priorities. |
| **🎯 Fit** | 25% | Whether the book fits your real life: length vs. time budget, series position, difficulty, narrator preference. |

Your priorities are set by a quick **5-step vibe quiz**, and you can re-tune them anytime from **Preferences**.

---

## Features

- 🎧 **Audiobook & 📖 Reading modes** — audio scores narrator performance, reading scores prose quality; both coexist in one ranked list.
- 🎲 **Vibe quiz** that sets your mood filters and quality weights via fast A/B questions.
- 🤖 **AI scoring** with [Claude Haiku](https://www.anthropic.com/claude) — mood tags, quality scores with one-line reasons, and fit data inferred from the description.
- 📥 **Batch shelf import** — paste or upload a Goodreads / StoryGraph CSV export and the whole shelf is searched, AI-scored, and ranked. StoryGraph's own mood/pace/content-warning data is used directly when present.
- ✍️ **Manual entry & editing** for books you already know.
- ⬇️ **Import / Export** your library as JSON.
- 🌗 **Light / dark themes**, fully responsive.
- 💾 **Everything saved locally** in your browser — no account, no server.

---

## Getting started

It's a single static file. Two ways to run it:

**Option A — just open it**
Double-click `index.html` to open it in your browser.

**Option B — serve it locally** (recommended, avoids some browser CORS quirks)
```bash
python -m http.server 8000
# then open http://localhost:8000/index.html
```

### You'll need a Claude API key
1. Get one at [console.anthropic.com](https://console.anthropic.com/).
2. Paste it into the **Claude API key** field in the app.
3. *(Optional)* Add a [Google Books API key](https://developers.google.com/books/docs/v1/using#APIKey) to raise the reading-mode search quota.

---

## Privacy

- Your **Claude API key is session-only** — it's never written to disk and is cleared when you close the tab.
- Your **books, preferences, and Google Books key** are stored in your browser's `localStorage` only.
- Nothing is sent anywhere except directly to the iTunes, Google Books, and Anthropic APIs from your own browser.

> **Note:** BookScore calls the Anthropic API directly from the browser (`anthropic-dangerous-direct-browser-access`). This is fine for personal/local use. If you ever host it publicly, route API calls through a small server-side proxy so your key isn't exposed.

---

## Tech

- Vanilla **HTML + CSS + JavaScript**, single file, **no build step, no dependencies**.
- **Claude Haiku** (`claude-haiku-4-5`) for scoring and tag inference.
- **iTunes Search API** (audiobooks) and **Google Books API** (reading) for metadata — both free.

---

## Roadmap

Ideas not yet built:

- ✏️ **Inline tag editing** — confirm or correct AI-guessed mood tags.
- 🚫 **Content-warning filters** as hard exclusions.
- 🔗 **"Find on Audible"** quick links per book.

---

## License

[MIT](LICENSE) © Mazen Elnabawy
