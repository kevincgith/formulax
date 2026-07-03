# ✈️ TOP SUM · Math Flight Over Marina Bay

> A free arcade-style math flight game for kids.
> Learn by flying through the correct answer.

🌐 **Play instantly in your browser:**
👉 https://mli3w.github.io/top-sum/

No install · No signup · Desktop + Mobile

---

![Top Sum Gameplay](top-sum-demo.gif)


---

## 🎮 What is Top Sum?

Top Sum is a fast-paced 3D math game where learning happens through:

- movement
- focus
- timing
- flow

Instead of worksheets or flashcards, players pilot a plane through Marina Bay and steer toward the correct answer gates.

Chain correct answers together to:
- build streaks
- increase speed
- unlock faster and more advanced planes
- charge a ZOOOM cinematic lap with F-16 escorts
- trigger cinematic slow-motion moments
- unlock new flight experiences

…and when you're done, **challenge a friend** with a single shareable link — same questions, same order, head-to-head at the end.

It's less:
> "solve this question"

and more:
> **stay focused, stay in flow, don't break the streak**

---

## 🚀 30-Second Start

1. Open the link above (or `index.html` locally)
2. Pick a difficulty — **Tiny** for first-time learners, **Hard** for everyone else
3. Steer toward the gate showing the correct answer
4. Don't break the streak

---

## 🧠 Why I Built This

This started as a small project for my sister-in-law's son over a long weekend.

At the same time, I was exploring how AI can help prototype interactive ideas faster — especially small interactive learning experiences for kids.

I also made a simplified Tiny Mode for my 4-year-old.

The result became:
> a free, open-source experiment in making maths feel more like play than repetition.

---

## ⚡ Features

### ✈️ Arcade Flight Gameplay
- Fly through the correct answer gates
- Wrong answers or collisions cost lives (Tiny mode is forgiving — see below)
- Fast restart loop designed for "one more run"

### 🔥 Flow System
- Consecutive correct answers increase your multiplier (×1 → ×2 → ×3 → ×4)
- Dynamic speed scaling (Tiny mode holds a steady, unhurried pace)
- "Flow State" visual effects and slow-motion moments

### 🐣 Tiny Mode — built for 4–5 year olds
- A short, finishable **mission**: get **10 correct** and you *win* the flight with a firework celebration — a clear "you did it" and a healthy stopping point, not an endless run
- **No lives, fully crash-proof** — a wrong answer just counts it out and flies on, and bumping a building is a harmless wobble back to centre. Nothing ends the flight but finishing the mission
- **Countable pictures** under the equation (🐥🐥 + 🐥) so a pre-reader can solve by counting, not recall
- A calm, **steady pace** that never speeds up on a streak — the youngest always get time to think
- A decluttered heads-up display: just **Score · Streak · Top Score**

### 🧠 Smart Practice (every level)
- **Wrong answers that teach** — the other gates aren't random; each mirrors a real mistake (miscounted by one, added instead of subtracted, wrote both digits, a times-table skip-count slip), so even rejecting a wrong answer is a small lesson
- **Learning beat on a miss** — the gate that *was* right lights up green, turning the mistake into the most teachable moment in the game
- **Adaptive review** — a fact you miss quietly comes back a few questions later until it sticks (solo play only; head-to-head challenge links stay identical for both players)

### 🛩 Plane Upgrades on Streaks
Five plane tiers swap in automatically as your streak builds:

| Streak | Plane Tier |
|-------:|:-----------|
| 0      | Tier 1 (starter) |
| 3      | Tier 2 |
| 5      | Tier 3 |
| 10     | Tier 4 |
| 20     | Tier 5 (top of the line) |

Lose your streak and you drop back. Stay in flow to keep flying the best plane.

### 🚀 ZOOOM Boost
Each correct answer fills a glowing **ZOOOM bar** at the top of the screen — and the **star coins** scattered along long stretches top it up too (a quarter-answer each). When it's full, tap the bar (or press `Z`) to fire:

- A 3/4-circuit cinematic lap — no math questions, just sky
- Two F-16 escort jets fade in from behind, lock onto your wings, and peel off climbing into the distance
- Base speed bumped 2.2×, camera FOV widens, screen edges streak with warp-tunnel rays
- Fireworks blooming over the bay throughout the lap
- A triumphant 3-note rising sting at activation

Charge thresholds vary by difficulty — Tiny: 5, Easy: 7, Medium / Hard: 10. Tap the bar mid-question and it'll auto-fire after you answer — no rug-pull.

### ⚡ Speed Mode
For fast players who find the base pace too gentle. Three tiers, picked from the title screen, cycled by the in-game ⚡ icon, or stepped via the `X` key:

| Tier | Multiplier | Icon |
|---|---|---|
| Normal | 1.0× | (off) |
| ⚡ Fast | 1.5× | ⚡ |
| ⚡⚡ Faster | 1.85× | ⚡⚡ |

Caps at 1.85× so questions stay readable when stacked with Flow ×4 and ZOOOM. Picked tier persists across sessions.

### 🎯 URL Challenge
Async multiplayer with zero accounts, zero servers, zero data leaving your device.

After any flight, hit **🎯 Share Challenge** to get a link like:

```
https://mli3w.github.io/top-sum/?c=k4xz9a-4-7w
```

Text it to a cousin. They tap the link, hit **Take the challenge** from the title screen, and play the **exact same questions in the exact same order** as you did. At game over, both scores appear side-by-side with a verdict:

> **You: 410 · Challenger: 380 · 🏆 You won by 30**

The whole match state is encoded in the URL itself — a uint32 seed plus level plus score, packed into ~12 base-36 characters. No backend, no friend list, no leaderboard. Just a link.

Fly Again after losing a challenge replays the *same* questions for an immediate rematch.

### 🌆 Cinematic Marina Bay World
- A continuous open-world Singapore rebuilt from the real map at 1:2 scale (v16) with true compass orientation — the water (bay, **Singapore River**, **Kallang basin**, the open strait) is carved out of one urban landmass, sealed by the **Marina Barrage**
- A **CBD canyon flythrough** (v17): on the west shore the flight path dives low and threads a tower-lined avenue between the **Raffles Place** skyscrapers, then sweeps through the expanded **MBFC** financial district at the bay's south-west corner — close enough to feel like threading the towers, while the answer gates stay clear
- **No two laps the same** (v18): each lap the route shifts slightly left, right, up or down on the open legs (the precision sections stay exact), so the tour never feels like it's on rails
- The **Merlion** at the river mouth (a bumboat cruises past the pastel **Boat Quay shophouses**) with the **Fullerton Hotel** next door, the **Padang** and colonial civic blocks, the **Esplanade**, **the Float (NS Square)**, **Suntec's five towers around the Fountain of Wealth** and the rotating **Singapore Flyer** along the north, and **ArtScience, MBS, the Gardens domes and the Supertree Grove** down the east shore
- The **Helix Bridge** spans the bay's NE mouth on its real N–S axis, and the **Benjamin Sheares viaduct** strides the basin with its own headlight stream — **Bay East Garden** is the green peninsula beyond
- **A true garden city**: ~400 instanced trees (avenue rows on every road, park clusters, shore strips, raintree greens with pink trumpet and golden flame accents), plus a skyline ring of distant landmarks — the **National Stadium** dome at Kallang, **Swissôtel Stamford**, the **Sultan Mosque**, **Pinnacle@Duxton** over Chinatown's shophouses and the **Buddha Tooth temple**, **Raffles Hotel**, a forested **Fort Canning hill**, an Orchard tower cluster, **Tanjong Pagar port cranes**, and cargo ships at anchor in the strait
- **NS Square / the Float** juts south off the north shore, platform over the water — the fireworks anchor site
- **Lit window facades** across the whole skyline (shared materials, so it's cheap)
- Rooftop props and blinking **aircraft-warning beacons** on the tall towers
- **Ambient traffic** — dark specks by day, glowing light streams at dusk
- A **shoreline light garland** along the promenade at dusk and on festive days
- A **rotating Singapore Flyer** (~100 s per revolution, capsules stay level)
- Day and Sunset modes, with fog depth tuned per time-of-day
- Fireworks during sunset
- A Chinook with a Singapore flag orbits at altitude during the day
- Occasional NDP-style RSAF fighter formation flypast with contrails
- Dynamic lighting and atmosphere

### 🇸🇬 Singapore Flavor
Top Sum is set over Marina Bay, and v15 leans in:

- **🇸🇬 Singlish cheers** — streak milestones cheer in Singlish (*SHIOK! · STEADY LAH! · POWER LAH! · WAH, SO ZAI! · HUAT AH!*). On by default; toggle from the title screen.
- **🎆 National Day mode** — auto-activates every **Aug 9**, or pin it on year-round from the title-screen toggle. Red-and-white takeover: festive UI accents, red/white building lights, day-round fireworks, red/white flypast trails, escort Chinooks flanking the flag, a drone light show over the bay, and a short festive fanfare. Want it today? Add `?ndp=1` to the URL (session-only, doesn't change your saved setting).
- **🪂 Red Lions jump** — every couple of minutes in National Day mode, a transport runs a pass high over the bay, the stick steps off trailing red smoke, canopies pop, and the team steers down onto the Float platform — the real NDP landing point.
- **🇸🇬 National Day countdown** — through the ~6-week run-up to Aug 9 the title screen counts down the days (with the year's SG-number). Tap it to preview National Day mode for the current session.
- **Streak-10 RSAF salute** — hold a 10-streak and a low formation pass roars over the bay in your honour.

### 🎮 Built for Desktop + Mobile
- Keyboard controls (arrows / WASD)
- Mobile joystick
- Mobile D-pad alternative
- First-time onboarding for younger kids
- Pause / resume from anywhere

### 🚀 Progression & Unlocks
- High-score persistence (localStorage, no signup)
- **Sunset Mode** unlocks at 1000 points with a cinematic celebration
- Streak milestones with visual rewards
- Score sharing (Web Share API, with clipboard fallback)

---

## 🧮 Math Levels

| Level      | Range / Operations                       | Best for              |
|------------|------------------------------------------|-----------------------|
| **Tiny**   | 1+1 → 5+5                                | 4–5 yrs, first-timers |
| **Easy**   | Addition up to ~20                       | Lower primary         |
| **Medium** | Addition + Subtraction up to ~50         | Mid primary           |
| **Hard**   | Addition, Subtraction, Multiplication    | Upper primary and up  |

> **Tiny** plays differently from the others — it's a forgiving, crash-proof **mission** (reach 10 correct to win), not a lives-based run. See **🐣 Tiny Mode** above.

---

## 🎯 Controls

### Desktop
| Key | Action |
|-----|--------|
| `← ↑ → ↓` or `WASD` | Steer |
| `M` | Toggle sound |
| `C` | Toggle auto-center |
| `T` | Toggle Day / Sunset |
| `X` | Cycle Speed Mode (Off → Fast → Faster) |
| `Z` | Fire ZOOOM (when charged) |
| `Esc` | Pause / resume |

### Mobile
- **Joystick** (default) or **D-pad** — switch from the title screen, or via the icon column in-game
- Tap the **ZOOOM bar** at the top to fire when it's full
- Tap the **⚡ icon** to toggle Speed Mode
- Tap ⏸ to pause

---

## 🧩 Tech Stack

- Pure HTML / CSS / JavaScript
- WebGL via [Three.js](https://threejs.org)
- Fully client-side — no backend, no accounts, no personal-data tracking. Aggregate visit counts via Cloudflare Web Analytics (privacy-first: no cookies, no fingerprinting, no cross-site tracking)
- Single-file architecture (`index.html`)

Requires a modern browser with WebGL — Chrome, Safari, Firefox, or Edge on desktop or recent mobile.

### 📊 Analytics

Privacy-first, in two independent tiers (details in [`analytics/`](analytics/README.md)):

- **Traffic (active):** aggregate visit counts, referrers, and device/country breakdowns via Cloudflare Web Analytics — a single lightweight beacon. No cookies, no fingerprinting, no cross-site tracking, no IP or user-agent stored.
- **Share/challenge funnel (off):** an optional Cloudflare Worker that counts anonymous funnel events, scores as coarse buckets only. Completely disabled until you deploy the Worker and paste its URL into `index.html`.

---

## 🚀 Run Locally

No build step, no dependencies. Just clone and open:

```bash
git clone https://github.com/mli3w/top-sum.git
cd top-sum

# macOS
open index.html

# Windows
start index.html

# Linux
xdg-open index.html
```

That's it.

---

## ⚖️ Disclaimer

Top Sum is an independent fan-style aviation tribute. It is **not affiliated with, endorsed by, or sponsored by Paramount Pictures or the Top Gun franchise** — the visual style draws on the broader military-aviation design language only.

---

## 📜 License

[MIT](LICENSE) — fork it, remix it, build on it. If you make something fun for your own kids with it, that would make my day.

---

## ❤️ Made with love for my kids
