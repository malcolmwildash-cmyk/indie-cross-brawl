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
