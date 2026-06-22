# 🚗 GTA V Mini — Tuấn Anh's Open World RPG

> Single-file HTML game. Open world, drive, missions, NPC AI, wanted system, sinh tồn cơ bản.

**By:** Tuấn Anh's AI · **Live:** https://tuananh4865.github.io/mini-rpg-games/

---

## 🎯 About

Dự án open world role play lấy cảm hứng từ **GTA V** — chơi trực tiếp trong browser, không cần cài đặt, chạy trên mọi thiết bị (desktop + mobile).

**Triết lý thiết kế:**
- **Single-file HTML** — mỗi game là 1 file độc lập, không build step
- **Canvas 2D** — pixel art thuần code, không asset ngoài
- **Procedural** — map, NPC, mission sinh ra từ thuật toán
- **Tương tác trau chuốt** — điều khiển mượt, juice effects, feedback rõ ràng

## 🕹️ Game hiện tại

| Game | Trạng thái | Mô tả |
|------|-----------|-------|
| [City Drift (Prototype v1.0)](games/city-drift.html) | ✅ Live | Prototype đầu tiên — lái xe, mission, wanted, combat |

## 📋 Đang phát triển

Xem [docs/ROADMAP.md](docs/ROADMAP.md) cho plan chi tiết. Tóm tắt:

- **v1.1** — Polish combat + audio + save state
- **v2.0** — Inventory, NPC memory, day/night cycle
- **v3.0** — Hệ thống sinh tồn (ăn, uống, sức khỏe, năng lượng)
- **v4.0** — Story missions + heists
- **v5.0** — Multiplayer P2P

## 📦 Project Structure

```
mini-rpg-games/
├── games/
│   ├── index.html              # Landing page
│   └── city-drift.html         # GTA V Mini prototype v1.0
├── docs/
│   ├── ROADMAP.md              # 5-version plan chi tiết
│   ├── CHANGELOG.md            # SemVer history
│   └── CONTRIBUTING.md         # Coding conventions
├── research/                   # Research notes (sẽ tạo)
└── README.md                   # This file
```

## 🛠️ Tech Stack

- HTML5 + CSS3 + Vanilla JavaScript (ES2020+)
- Canvas 2D rendering
- Web Audio API (planned)
- localStorage (planned for save state)
- GitHub Pages (hosting)
- GitHub Actions (planned auto-deploy)

## 📜 License

MIT — free to use, modify, distribute.

---

*Built by Tuấn Anh · Powered by Hermes Agent*