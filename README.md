# 🎮 Mini RPG Games

> A collection of bite-sized RPG games — built as single-file HTML, runs anywhere.

**By:** Tuấn Anh's AI · **Live:** https://tuananh4865.github.io/mini-rpg-games/

---

## 🎯 Games

| # | Game | Style | Status |
|---|------|-------|--------|
| 1 | [Forest Wanderer](games/forest-wanderer.html) | Top-down pixel RPG, slash + explore | ✅ v1.0 |
| 2 | [City Drift](games/city-drift.html) | GTA-lite open-world, drive + missions | ✅ v1.0 |

---

## 🕹️ Quick Play

Click any game above to play. **No install, no login, works on phone + desktop.**

### Controls cheat sheet
**Forest Wanderer** — WASD move · Shift dash · Space/E attack/interact
**City Drift** — WASD drive · Shift boost · Space brake/punch · E in/out car · F shoot · M mission

---

## 🛠️ Tech Stack

- **Pure HTML/CSS/JS** — single file, no build step
- **Canvas 2D** rendering (pixel art, no asset files)
- **Procedural generation** — no external data
- **GitHub Pages** hosting (free CDN)
- **GitHub Actions** auto-deploy on push

---

## 📦 Project Structure

```
mini-rpg-games/
├── games/              # All game HTML files (single-file games)
│   ├── forest-wanderer.html
│   ├── city-drift.html
│   └── index.html      # Landing page
├── docs/               # Documentation
│   ├── ROADMAP.md      # Future plans
│   ├── CHANGELOG.md    # Version history
│   └── CONTRIBUTING.md
├── assets/             # Shared assets (sprites, sounds) — future
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Pages auto-deploy
└── README.md           # This file
```

---

## 🗺️ Roadmap

See [docs/ROADMAP.md](docs/ROADMAP.md) for full plan. TLDR:

- **v1.x** — Polish core games (better combat, more missions, save state)
- **v2.0** — Add inventory system + NPCs with memory
- **v3.0** — Multiplayer (WebRTC peer-to-peer for 2-4 players)
- **v4.0** — Mobile-first PWA + Telegram Mini App

---

## 📜 License

MIT — do whatever you want, just don't sell it as-is.

---

*Built by Tuấn Anh · Powered by Hermes Agent*