# 🤝 Contributing

Solo project, but here's the convention if you fork / want to add games.

---

## Adding a new game

1. **File location:** `games/your-game.html`
2. **Single-file rule:** All CSS + JS inline. No external assets (CDN OK).
3. **Naming:** kebab-case, e.g. `dungeon-crawler.html`
4. **Size budget:** Aim for < 50KB per game. Single-file means everything fits.
5. **Update landing page:** Add card to `games/index.html`
6. **Update ROADMAP:** Add to experiments log
7. **Bump version:** Edit `docs/CHANGELOG.md` + bump version in `games/index.html`

---

## Code style

- **No build step** — vanilla JS, ES2020+
- **No frameworks** — jQuery/React/Vue forbidden (defeats single-file purpose)
- **Comments:** Vietnamese or English, OK either way
- **Magic numbers:** OK for prototypes, refactor if game grows
- **Variable naming:** camelCase (JS), kebab-case (CSS classes)

---

## Testing checklist before commit

- [ ] Game loads with no console errors
- [ ] Controls responsive on keyboard
- [ ] Player can save/load state if applicable
- [ ] No external network calls (except CDN libs)
- [ ] Tested on Chrome + Safari + Firefox
- [ ] Mobile viewport tested (touch if supported)

---

## Commit message format

```
🎮 [game] short description

- detail 1
- detail 2
```

Examples:
- `🎮 [forest-wanderer] add sword trail particles`
- `🎮 [city-drift] fix police chase stuck on building`

---

## Roadmap priorities

Check `docs/ROADMAP.md` for what's next. Don't build features not in roadmap without discussing.