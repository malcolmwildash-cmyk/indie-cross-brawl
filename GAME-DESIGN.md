# INDIE CROSS: BRAWL — Game Design Doc

*A fan homage — all characters built with our own original art & names where needed. Non-commercial, personal project.*

## What it is
A **2.5D beat-em-up** (Castle Crashers / Streets of Rage style) set in the Indie Cross
crossover world. Walk through themed stages, beat waves of enemies, fight a boss.

## Tech (as actually built)
- **3D with Three.js**, loaded from a CDN via importmap in a **single `index.html`** — NO build
  step, NO Node.js needed (Node wasn't installed; React+Vite was the original aim but we pivoted
  to single-file so we could start immediately). Can move to React/Vite later for menus.
- Needs an internet connection (Three.js comes from a CDN).
- Run/preview locally with a static server, e.g. `python3 -m http.server` (a `.claude/launch.json`
  config named "brawl" on port 8123 exists for the preview tool). Or just open `index.html`.
- **Look = TMNT: Shredder's Revenge style:** flat **side-on orthographic** camera +
  `RenderPixelatedPass` (pixel-art filter) + `MeshToonMaterial` (flat cel shading) + a pixel-art
  city skyline backdrop. Plus real shadows, **bloom**, **screen shake**, **hit-stop**, particles.

## Locked decisions
- **Camera:** flat **side-on** arcade beat-em-up view (Shredder's Revenge). Walk left/right to
  scroll, up/down for depth. *(Pending request: zoom the camera out a bit more — see build status.)*
- **Players:** solo for the first version (co-op can come later).
- **Roster:** designed by Malcolm (below). Movesets to be defined later.

## ✅ BUILD STATUS (end of first session)
**Implemented and verified working in `index.html`:**
- Playable **Frisk** (rounded model — sphere head + capsule limbs): run/jump/dash, **light (J)** &
  **heavy (K)** attacks, combos, **SYNC special (L)**.
- **Three enemy types:** Runner (fast/weak), Blob (normal), Brute (big/tanky); spawn in waves.
- **Portal Shards** drop from enemies and magnetize to you; **saved permanently** (localStorage,
  survive death AND closing the game).
- Juice: hit particles, **screen shake**, **hit-stop**, **bloom**, falling-block visuals.
- **Charlotte's Lab hub** (mode `hub`): Charlotte robot (black orb, 3 yellow rings, 3 blade-legs)
  runs an **upgrade shop** — spend shards on **+25 HP** or **+25% damage**.
- **Cuphead-style World Map** (mode `map`): node medallions on a path (Lab / Snowdin / Ink Studio /
  Devil's Casino / Gamaster). ←→ + Enter or click to pick a place.
- **Gamaster boss fight** (mode `boss`): floating arcade-screen boss with HP bar, drops hazard
  blocks; **GENRE SHIFT** ~10s in → original **falling-block puzzle** (←→ move, ↑ rotate, ↓ drop;
  clear 3 lines / survive timer → big boss damage → back to brawl).
- **Flow:** Lab → purple portal → World Map → pick node → Stage/Boss → return portal → World Map.

**Controls:** Move WASD/arrows · Jump Space · Dash Shift · Light J · Heavy K · Sync L.

**Known issues / requests still OPEN (from end of session — NOT yet done):**
- ⚠️ **"I can't play"** — Malcolm reported being unable to play; needs investigating (likely
  needs to open `index.html` in a real browser with internet for the CDN, OR a control/focus issue).
  REPRODUCE & FIX before adding features.
- **Zoom the camera out** a bit more (increase `FRUSTUM` in index.html; currently 16).
- **Finish the roster:** build the other 9 fighters as playable, each with their signature
  movement (table below) + light/heavy movesets.
- **Frisk should wield the real knife** (the toy/real knife from Undertale) — give him an actual
  knife in-hand and a slashing attack animation.
- Levels aren't visually themed yet (all load the placeholder neon-city stage) — Snowdin first.
- Gamaster fights on the placeholder stage (no unique boss arena yet); other bosses' genre shifts
  (shmup / rhythm / auto-runner) not built; Sync team move, skill trees, cosmetics not built.

## ⭐ Signature mechanic — SYNC GAUGE (team-up move)
Inspired by Hyrule Warriors' special gauge. A meter fills as you fight; when it's full,
**two characters perform a combined Team Move that deals massive damage.**

> **Open question:** since v1 is solo, how does a *team* move work with one player?
> Likely design: you bring **two characters** into a stage — one active, one as a partner
> you can tag/call. When the Sync Gauge is full, both unleash the duo move together.
> *(Need to confirm with Malcolm.)*

## Combat / moveset framework
Every fighter shares the same button layout, but the *feel* differs per character:
- **Light attacks** — fast, low damage, chain into combos
- **Heavy attacks** — slow, high damage, knockback / launchers
- **Movement system** — ⭐ **each fighter moves exactly like they do in their home game.**
  This is the heart of the game's identity. Proposed signature moves:
  | Fighter | Signature movement (from their game) |
  |---|---|
  | Cuphead | dash + **pink parry-bounce** off pink objects/attacks |
  | Frisk | **basic & beginner-friendly** — simple run, jump, and dash |
  | Bendy | sink into an **ink puddle** and resurface elsewhere; climb walls as ink |
  | Shovel Knight | **shovel pogo-bounce** (down-attack bounces off enemies) |
  | Madeline / Badeline | 8-directional **air-dash** + climb; switching halves changes dash feel |
  | The Drifter | the **Hyper Light dash** — short, chainable teleport-dash |
  | The Beheaded | fast **roll-dodge** through enemies (Dead Cells) |
  | V1 | super-fast **slide + dash**, wall-jump (Ultrakill speed) |
  | Zagreus | the **Hades dash** — dash through enemies into a dash-strike |
  | Niko | **basic & beginner-friendly** — same run, jump, dash as Frisk |
- **Sync Gauge** team move (see signature mechanic above)

## Hub world & progression loop
- **Home World** — a hub you return to between stages.
- **Charlotte** — a **little robot** (homage to the little robot from *Indie Cross* ep 2).
  Lives in the hub and runs upgrades — tinkers on your fighters to give them new powers.
  - **Look:** a small **ball body** suspended off the ground on **three blade-like legs**
    jutting out of the ball (tripod stance, ball held up high).
  - **Colors:** mostly **black** with **yellow accents**.
  - **Detail:** **three yellow lines intersecting** in the middle of the ball.
  - *(Yellow accents = great for a glowing/bloom look.)*
- **Portal Shards** — currency. **Every enemy drops a couple.** Collect them in stages.
- **Skill trees** — each fighter has their **own skill tree**. Spend Portal Shards with
  Charlotte to buy nodes and climb the tree, unlocking **new powers, abilities & stat boosts**.
  (Per-fighter, permanent. Gives every character a long-term progression goal.)
- Core loop: *play a stage → beat enemies → collect shards → return to hub → buy skill-tree
  upgrades → next stage stronger.*

## Cosmetics & per-character goals
- **Cosmetics** — unlockable looks (skins / color palettes / accessories), **per character**.
- **Earned by completing goals**, not bought — each fighter has their **own set of challenges**
  (e.g. "beat a stage without taking damage as Cuphead", "land 50 pogo-bounces as Shovel Knight").
- Purely for show / bragging rights — keeps players replaying with each character.

## Levels & bosses
Two kinds of levels:
- **Run-and-gun levels** — Cuphead-style side-scrolling **platforming** stages (move, jump,
  shoot/fight through hazards and enemies that drop Portal Shards).
- **Boss fights** — dedicated, **replayable** showdowns against the rogues.

**World map (built):** a Cuphead-style overworld with node medallions on a winding path
(Charlotte's Lab → Snowdin → Ink Studio → Devil's Casino → Gamaster boss). Reached from the
lab's portal; move with ← →, Enter (or click) to go. Level nodes load a stage; the Lab node
returns to Charlotte. *(Levels not yet visually themed — all load the placeholder city stage.)*

### ⭐ Levels = the fighters' home worlds
Each level is themed after a roster character's home game (Malcolm's idea). Proposed:
| Level | Home of | Look |
|---|---|---|
| **Snowdin** | Frisk (Undertale) | snowy pine forest & little town, soft blues/whites |
| The Ink Studio | Bendy | black-and-white haunted cartoon studio, ink |
| The Devil's Casino | Cuphead | neon run-and-gun carnival |
| Mount Celeste | Madeline/Badeline | snowy/purple mountain cliffs |
| The Underworld | Zagreus (Hades) | red Tartarus halls, lava |
| Neon Ruins | The Drifter (Hyper Light) | teal/pink crystalline ruins |
| The Prison | The Beheaded (Dead Cells) | grimy ramparts |
| Hell (industrial) | V1 (Ultrakill) | brutalist steel & blood |
| Tower of Fate | Shovel Knight | classic castle platforming |
| The Barrens | Niko (OneShot) | dim world under a dead sun |

*Current build ships a placeholder **neon city street** stage; first themed pass = **Snowdin**
(fits Frisk, the starter).*

**Bosses — the rogues of Indie Cross:**
| Boss | Notes |
|---|---|
| Gamaster | rogue boss |
| Unithor | rogue boss |
| Midrusa | rogue boss |
| Goitrixs | rogue boss |
| **Unreal** | **huge Marvel-vs-Capcom *Galactus*-style fight** (screen-filling giant) |
| **Charlotte** | **separate boss in her own right** — the betrayal fight (see ending below) |

*(Spellings as given — confirm later. These are homages to the Indie Cross series villains.)*

## ⭐ Boss mechanic — GENRE SHIFT
A signature boss twist (Malcolm's idea): a few seconds into a boss fight (~10s), the boss
**warps the whole game into a different genre** for a phase, then it may shift back/again.
Fits the "reality-warping" rogues — Gamaster especially (a literal Game Master).
Proposed per-boss shifts:
| Boss | Genre it shifts into |
|---|---|
| **Gamaster** | **falling-block puzzle** (Tetris-style) — survive/clear lines while dodging |
| Unithor | top-down bullet-hell / shmup |
| Midrusa | rhythm section (hit to the beat) |
| Goitrixs | classic auto-runner platformer |

**Applies to EVERY boss EXCEPT Unreal.** Unreal (the finale) has **no genre shift** — it's a
straight, giant screen-filling cosmic showdown (MvC Galactus-style). After a whole game of
reality being warped, the last fight is pure, which makes it feel climactic.

Notes: build these as **original mini-modes** (no copyrighted assets/branding — the *genre*
is the homage). Each shift is a timed phase; clearing it returns to the brawl and damages the
boss.

**BUILT (Gamaster):** the Gamaster boss fight is in — a floating arcade-screen-headed boss
with an HP bar; it drops hazard blocks; melee + the genre shift damage it. ~10s in it triggers
the **falling-block genre shift** (own original mini-mode): move/rotate/drop pieces, clear 3
lines (or survive the timer) to deal big damage, then back to the brawl. Other bosses' shifts
(shmup / rhythm / auto-runner) still to build.

## Campaign ending — the Charlotte betrayal
- At the end of the campaign, **Charlotte says a betrayal line** — the helpful upgrade robot
  turns on you.
- **Inverse-difficulty final fight:** the fight scales to how much you upgraded with her.
  - **No upgrades → easier fight**
  - **Lots of upgrades → harder fight** (your own power is used against you)
- **You fight Charlotte herself** — she is a **separate boss in her own right** (not just the
  hub NPC). Her boss form uses her blade-legs and whatever upgrades she gave you against you.

## Starting roster (heroes) — 10 fighters, all available from the start
| In-game | Homage to | Source game |
|---|---|---|
| Cuphead | Cuphead | Cuphead |
| Frisk | Frisk (the red SOUL / DETERMINATION) | Undertale |
| Bendy | Bendy | Bendy and the Ink Machine |
| Shovel Knight | Shovel Knight | Shovel Knight |
| Madeline / Badeline | one fighter — **switch between** Madeline & Badeline mid-fight | Celeste |
| The Drifter | The Drifter | Hyper Light Drifter |
| The Beheaded | The Beheaded | Dead Cells |
| V1 | V1 | Ultrakill |
| Zagreus | Zagreus (*"zurgarus"* — confirm?) | Hades |
| Niko | Niko (*"Nico"* — confirm?) | OneShot |

## Unlockable characters
| In-game | Homage to | Source game |
|---|---|---|
| Springtrap | Springtrap | Five Nights at Freddy's |
| The Untitled Goose | the goose | Untitled Goose Game |

## TODO / still to design
- [x] Movement system — each fighter moves like their home game
- [x] Hub world + Charlotte + Portal Shards + upgrades
- [x] Charlotte's design
- [ ] Light/heavy attack specifics per character (framework done; details later)
- [ ] How Sync Gauge team move works in solo play (tag two fighters?) — needed before
      we build Sync, but NOT needed for the first playable build
- [ ] Natural Sync pairings (e.g. Madeline + Badeline)
- [x] Level types (run-and-gun platforming + replayable boss fights)
- [x] Bosses (the rogues: Gamaster, Unithor, Midrusa, Goitrixs, Unreal)
- [x] Campaign ending (Charlotte betrayal + inverse-difficulty final fight)
- [x] Final fight = Charlotte herself (a separate boss in her own right)
- [ ] Stage/enemy details per world
- [x] Skill trees + cosmetics/goals

## First playable build (v1 scope)
Smallest version that's actually fun and shows off the graphics:
1. One playable fighter (suggest **Frisk** — simplest movement) with light + heavy + dash
2. The classic beat-em-up camera + one short stage
3. A few enemies that drop **Portal Shards**, with hit particles + screen shake + bloom
4. The **Home World** hub with **Charlotte** and a basic upgrade
Then expand: more fighters → their signature movement → more stages → Sync Gauge.
