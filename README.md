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
- Wrong answers or collisions cost lives
- Fast restart loop designed for "one more run"

### 🔥 Flow System
- Consecutive correct answers increase your multiplier (×1 → ×2 → ×3 → ×4)
- Dynamic speed scaling
- "Flow State" visual effects and slow-motion moments

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
Each correct answer fills a glowing **ZOOOM bar** at the top of the screen. When it's full, tap the bar (or press `Z`) to fire:

- A 3/4-circuit cinematic lap — no math questions, just sky
- Two F-16 escort jets fade in from behind, lock onto your wings, and peel off climbing into the distance
- Base speed bumped 2.2×, camera FOV widens, screen edges streak with warp-tunnel rays
- Fireworks blooming over the bay throughout the lap
- A triumphant 3-note rising sting at activation

Charge thresholds vary by difficulty — Tiny: 5, Easy: 7, Medium / Hard: 10. Tap the bar mid-question and it'll auto-fire after you answer — no rug-pull.

### ⚡ Speed Mode
For fast players who find the base pace too gentle. Three tiers, picked from the title screen, cycled by the in-game ⚡ icon, or stepped via the `S` key:

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
- Stylised Singapore skyline (Merlion, bay, boats, water)
- Day and Sunset modes
- Fireworks during sunset
- A Chinook with a Singapore flag orbits at altitude during the day
- Occasional NDP-style RSAF fighter formation flypast with contrails
- Dynamic lighting and atmosphere

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

---

## 🎯 Controls

### Desktop
| Key | Action |
|-----|--------|
| `← ↑ → ↓` or `WASD` | Steer |
| `M` | Toggle sound |
| `C` | Toggle auto-center |
| `T` | Toggle Day / Sunset |
| `S` | Cycle Speed Mode (Off → Fast → Faster) |
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
- Fully client-side — no backend, no analytics, no tracking
- Single-file architecture (`index.html`)

Requires a modern browser with WebGL — Chrome, Safari, Firefox, or Edge on desktop or recent mobile.

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
