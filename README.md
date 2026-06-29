# Indie Cross: Brawl

A 3D pixel-art beat-em-up in the style of *TMNT: Shredder's Revenge* — walk
through themed stages, beat waves of enemies, and take down the boss.

Built with [Three.js](https://threejs.org/) loaded from a CDN, all in a single
`index.html` — no build step, no Node.js needed.

## How to play

**Option A — open the file directly**
Open `index.html` in a web browser. (Needs an internet connection, because
Three.js loads from a CDN.)

**Option B — run a local server**
From inside this folder:

```bash
python3 -m http.server
```

then open the URL it prints (usually <http://localhost:8000>).

### Controls

| Action        | Keys              |
| ------------- | ----------------- |
| Move          | WASD / Arrow keys |
| Jump          | Space             |
| Dash          | Shift             |
| Light attack  | J                 |
| Heavy attack  | K                 |
| Sync special  | L                 |

## Fan homage

This is a **non-commercial, personal fan project**. All characters are built
with our own **original art and names**, inspired by indie games. Not affiliated
with or endorsed by any of those games or their creators.

## Design doc

See [GAME-DESIGN.md](GAME-DESIGN.md) for the full design notes.

## 🏗️ Hosting & Deployment — read this first (humans + AI agents)

Malcolm's sites span **two different accounts**, which is the easy thing to get wrong:

- **GitHub** — `malcolmwildash-cmyk` (Malcolm's account; **all** source lives here)
- **Vercel** — `travis-9112` / team `travis-9112s-projects` (Travis's account; hosts the Vercel sites)
- **Domain `malcolmwildash.com`** — registrar **and** DNS at **GoDaddy** (Travis's account).
  DNS points the domain at Vercel:
  - `A   @   → 76.76.21.21`
  - `CNAME  www → cname.vercel-dns.com`

### This repo (`indie-cross-brawl`)
- **Host:** **GitHub Pages** (no Vercel)
- **Live:** https://malcolmwildash-cmyk.github.io/indie-cross-brawl/
- **Deploy:** Served by GitHub Pages from `main`. A stale Pages custom domain (`www.malcolmwildash.com`) was removed 2026-06-28 — that domain belongs to the Vercel-hosted flagship, not this repo.

### Every Malcolm site (one account map, mixed hosting)
| Repo | Host | Live URL |
|---|---|---|
| `malcolmwildash.com` | Vercel | https://malcolmwildash.com (flagship + `/games`) |
| `star-robot` | Vercel | https://star-robot.vercel.app |
| `olives-bug-guide` | Vercel | https://olives-bug-guide.vercel.app |
| `minecraft-rpg` | Vercel | https://minecraft-rpg.vercel.app |
| `undertale-simulator` | GitHub Pages | https://malcolmwildash-cmyk.github.io/undertale-simulator/ |
| `minecraft-stick-fighters` | GitHub Pages | https://malcolmwildash-cmyk.github.io/minecraft-stick-fighters/ |
| `indie-cross-brawl` | GitHub Pages | https://malcolmwildash-cmyk.github.io/indie-cross-brawl/ |
| `indy-cross-smash` | not deployed (private WIP) | — |

> Note: hosting is **mixed** — some repos are on **Vercel**, some on **GitHub Pages**. Check the row above for this one. `malcolmwildash.com` itself is on **Vercel**, *not* GitHub Pages.

### ⚠️ Security — credentials
Never commit tokens or embed them in a git remote URL. A local clone of the
`malcolmwildash.com` repo was set up with an **embedded classic, admin-scoped GitHub
Personal Access Token** in `.git/config`. That token **must be rotated**
(GitHub → Settings → Developer settings → Personal access tokens) and git auth should use
the **`gh` CLI credential helper** (`gh auth login`) instead of an embedded token. Do not
paste tokens into code, READMEs, or remote URLs.

---
