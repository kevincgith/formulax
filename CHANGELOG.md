# Changelog

All notable changes to **Top Sum** are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project loosely adheres to semantic versioning.

---

## [v14] — 2026-05-10

**URL Challenge** — async multiplayer without a backend. Share a link, a friend plays the exact same questions, head-to-head at the end. Zero accounts, zero servers, zero data leaves either device.

### Added
- **URL Challenge mode.** After any flight, hit **🎯 Share Challenge** to generate a shareable link like `https://mli3w.github.io/top-sum/?c=<seed>-<level>-<score>` (compact base-36 encoding, ~12 chars — fits cleanly in iMessage previews). Recipient opens the URL, taps **Take the challenge** from the title-screen banner, and plays the *exact same questions in the exact same order*. At game over, both scores appear side-by-side with a verdict.
- **Seedable question RNG.** Question generation now routes through a swappable `questionRng` — `Math.random` for normal play, a Mulberry32 PRNG seeded from the URL in Challenge mode. Both players see identical sequences.
- **Title-screen challenge banner.** Pulsing magenta panel when an incoming challenge is detected. Two buttons: Take Challenge (enters challenge mode at the challenger's difficulty) or Skip (strips `?c=` from the URL so refresh doesn't re-surface it).
- **Head-to-head game-over comparison.** When the flight was a challenge, a `vs` block appears above the score lines: *You / Challenger / verdict* (🏆 won, ❌ beaten, 🤝 tied).
- **Share Challenge button on every flight.** Even normal-mode runs can be sent as a challenge — encodes whatever seed that flight was running on.

### Changed
- **Fly Again preserves challenge mode.** If the just-finished flight was a challenge, "Fly Again" replays the *same* questions for a rematch. Without this, a lost challenge would silently become a fresh-seed flight, breaking the natural "I was so close, let me try again" loop.

### How it works (no servers)
The entire "match state" is encoded in the URL itself. `seed.toString(36) + '-' + level + '-' + score.toString(36)`. The recipient's game decodes the URL on load, locks the difficulty and seed, and the Mulberry32 PRNG deterministically reproduces the question sequence. The verdict at the end is local — both players' devices independently know the result without ever communicating with a server.

---

## [v13.2] — 2026-05-10

Internal refactor patch — no new gameplay features. Stabilises three patterns from a senior-review pass: a recurring modal click bug, per-question allocation churn, and synchronous localStorage writes on the render loop.

### Changed
- **Modal pattern consolidated.** Replaced two ad-hoc `pointer-events: auto` rules on `#pause-overlay` and `#unlock-celebration` with a single shared selector: `#hud [role="dialog"] { pointer-events: auto }`. Both overlays gained `role="dialog"` + `aria-modal="true"` + `aria-label` — semantic + accessibility win. Future modals inside `#hud` inherit the click-fix automatically (stops the bug pattern at its source).
- **Gate pool.** Pre-build 3 reusable gate shells at startup instead of allocating fresh `Three.Mesh` + materials + a 256×256 canvas + GPU texture upload per question. `setupGate()` mutates the pool's materials and canvas in place; `clearGates()` hides instead of removing from the scene. Saves ~10 allocations + 1 GPU texture upload per question.
- **`persistAsync` helper.** Wraps `Settings.save()` (5 writes per toggle) and `maybeUpdateBest()`'s best-score write (fires after every correct answer on a best run) in `requestIdleCallback` with a `setTimeout` fallback for older Safari. Pushes localStorage hitches off the render loop.

### Verified clean
- **Frame-rate independence audit** — no animations use raw frame counts. Every per-frame mutation routes through `dt`, `rawDt`, or accumulated `time`. 120 Hz displays should match 60 Hz pacing exactly.

---

## [v13.1] — 2026-05-10

Polish patch on top of v13. Speed Mode gains a Faster tier, wingmate contrails finally look like contrails, and the v13 regression that hid most in-game icons is fixed.

### Added
- **Desktop in-game hint** now surfaces `Z: ZOOOM` so the shortcut is discoverable during play.

### Changed
- **Speed Mode** upgraded from a 2-state toggle to a 3-state cycle:
  - Off (1.0×)
  - ⚡ Fast (1.5× — same as the previous Speed Mode)
  - ⚡⚡ Faster (1.85× — new)
  - Caps at 1.85× so 3-digit hard math stays readable when stacked with Flow ×4 and ZOOOM.
  - Title-screen checkbox replaced with a radio picker mirroring the time-of-day pattern.
  - In-game ⚡ icon cycles through tiers — emoji switches to ⚡⚡ at Faster with a brighter glow and a tighter 0.95s pulse.
  - `S` key cycles Off → Fast → Faster → Off.
  - Backward compat: old `topsum_speedmode='1'` saves map to Fast.
- **Wingmate ZOOOM contrails** replaced with a triangle-strip ribbon mesh — same custom shader and 25 Hz sample rate as the player's plane trail. Was a Points cloud that read as floating squares.
- **Mobile icon column** gap tightened 10 px → 8 px to fit six icons cleanly on smaller phones.

### Fixed
- **In-game icon column on desktop:** a stray CSS rule shipped with v13 hid every icon except Speed Mode. Removed — all six icons render again on both desktop and touch.

---

## [v13] — 2026-05-10

The biggest update since launch. New ZOOOM cinematic boost, Speed Mode for fast players, redesigned title logo, sunset bumps, and an RSAF flypast over Marina Bay.

### Added
- **ZOOOM cinematic boost** — pill-shaped bar fills as you answer correctly (5/7/10 streak by difficulty). Once full, tap or press `Z` to fire a 3/4-of-circuit cinematic lap:
  - Big italic "ZOOOM" word flies across the screen at activation
  - Two F-16 escort jets fade in from the rear, lock onto your flanks, then peel off climbing-and-outward in the final 15% of the lap
  - Each wingmate emits a glowing additive-blend vapor trail (80-sample point cloud)
  - Camera FOV widens from 72° to 92° for a warp-tunnel feel
  - Spinning radial speed-streaks overlay + bright edge vignette
  - Fireworks force-fired across the bay every 0.28–0.50s during the lap (bypasses sunset gating)
  - 3-note rising sting (C5/E5/B5) + low-frequency sawtooth engine swell at activation
  - G-force camera shake on activation
  - Tap mid-question = "ZOOOM ARMED" — auto-fires after the answer settles, never rug-pulls a question
  - Math layer suspended for the lap; base speed × 2.2; gates removed
- **Speed Mode** (50% faster base × flow speed) — title-screen checkbox + in-game `⚡` icon (visible on touch and desktop) + `S` keyboard shortcut. Persists to localStorage. Stacks with Flow multiplier and ZOOOM.
- **NDP-style RSAF fighter flypast** in day mode — 5 jets in arrow formation streak across the bay every ~35–65s with fading white contrails.
- **Star insignia (★)** above the title logo with twinkle + gentle vertical float.
- **Cinematic warm radial bloom** backdrop behind the title logo.
- **Title intro sequence** (~1.6s, one-shot): wings sweep outward, TOP SUM settles, star drops with a subtle overshoot, subtitle rises last.
- **Ambient title loops**: breathing gold pulse on the type; star twinkle + float.
- **Sunset Mode unlock celebration** at 1000 pts now includes a full-screen sun-flare bloom, slow-rotating golden sun-rays behind the card, a pulsing halo ring behind the 🌅 icon, and ~46 falling golden sparkle particles in two bursts.
- **`body.sunset-pending` indicator** — glows the in-game ☀ time icon and the title-screen 🌅 Sunset radio until the player engages sunset for the first time, then auto-clears.
- **Title-screen keyboard hint** now surfaces all six shortcuts (C / M / T / S / Z / ESC).
- `prefers-reduced-motion` disables every new title and ZOOOM animation.
- `README.md`, `LICENSE` (MIT), and this `CHANGELOG.md` added to the repo.

### Changed
- **Title logo redesigned** — single centered swept-forward delta wing pair in chrome forming an inverse triangle that frames the type; V tip drops near the · in the subtitle. TOP SUM now side-by-side same-sized italic gold metallic (was stacked, with SUM in blue). Brighter gradient and warm amber halo replacing the prior dark vignette.
- **Sunset firework palette** doubled — added green / cyan / orange / purple / lime (10 colours total).
- **Sunset firework cadence** tightened from 6–8s to 4–5.5s for a slightly denser sky.
- **Subtitle** letter-spacing tightened ~14%, colour brightened, opacity 0.95 → 1.
- **Open Graph + Twitter card** meta tags now use absolute URLs anchored to `https://mli3w.github.io/top-sum/` with a working `og:image` (234KB PNG — was a 15MB animated GIF that exceeded the 5MB cap on LinkedIn / Slack / WhatsApp, causing share previews to drop to plain links).
- `shareScore()` always shares the canonical play URL — never a local `file://` path or query-string variant.

### Fixed
- **Sunset Mode unlock celebration** "Try it now / Maybe later" buttons were unclickable on desktop. Same root cause as the v12 pause overlay fix — overlay nested inside `#hud` (`pointer-events: none`) without re-enabling pointer events.
- **Wingmate orientation** in earlier ZOOOM iterations had jets facing perpendicular to flight direction; fixed by replacing `lookAt()` with a `Matrix4.makeBasis()` approach that maps the jet model's local +X (nose) onto the path tangent directly.
- **Wingmate roll direction** was reversed (banked opposite of player input); sign flipped so wingmates now bank into the player's turns.

---

## [v12] — 2026-05-07

### Added
- **NDP-style RSAF fighter flypast** (day-only ambience): 5 jets in arrow formation streak across the bay every ~35–65s with fading white contrails.
- **Star insignia** (★) above the title logo with twinkle + gentle vertical float.
- **Cinematic warm radial bloom** behind the whole title logo.
- **Title intro sequence** (~1.6s, one-shot on first render): wings sweep outward, TOP SUM settles, star drops with a subtle overshoot, subtitle rises last.
- **Ambient title loops**: slow breathing gold pulse on the type; star twinkle + float.
- `@media (prefers-reduced-motion: reduce)` disables all title animations.
- **Sunset unlock celebration** at 1000 pts now includes a full-screen sun-flare bloom, slow-rotating golden sun-rays behind the card, a pulsing halo ring behind the 🌅 icon, and ~46 falling golden sparkle particles in two bursts.
- **`body.sunset-pending` state** glows the in-game ☀ time icon and the title-screen 🌅 Sunset radio until the player engages sunset for the first time (then auto-clears).
- `README.md`, `LICENSE` (MIT), and this `CHANGELOG.md` added to the repo.

### Changed
- **Title logo redesign** — replaced flanking feathered gold wings with a single centered swept-forward delta wing pair in chrome that forms an inverse triangle framing the type, V tip dropping near the · in the subtitle.
- **TOP SUM** now side-by-side same-sized italic gold metallic (was stacked, with SUM in blue).
- Brighter, more inviting gold gradient on the type with a warm amber halo replacing the prior dark vignette.
- Subtitle: letter-spacing tightened ~14%, colour brightened, opacity 0.95 → 1.
- **Open Graph / Twitter card** meta tags now use absolute URLs anchored to `https://mli3w.github.io/top-sum/` with a working `og:image` (previously pointed at a non-existent `share-card.png`).
- `shareScore()` always shares the canonical play URL — never a local `file://` path or query-string variant.

### Fixed
- **Pause overlay buttons** (Resume / Restart / End Flight / Back to Menu) were unclickable on desktop. The overlay sat inside `#hud` (`pointer-events: none`) without re-enabling pointer events on itself.

---

## [v11] — earlier

Path re-route, gate colour scheme, ambient world systems (Chinook + flag, fireworks, MBS Spectra), Sunset Mode unlock at 1000 pts with celebration, single ⏸ pause overlay, first-time onboarding, mobile control tip, Tiny mode arrow assist.

See the comment block at the top of [`index.html`](index.html) for the full v11 / v10 / earlier change history.
