---
name: editswarm
description: >-
  Use this for show (or Swarm-styled) full-episode long-form edits:
  dead-air cut, DOAC/Lex-style hook trailer, black/beat who-we-are ID open, DOAC
  captions, sourced graph/quote/table overlays, kiss-out, Drive QA — same method
  as the locked reference episode (host & guest) master.
---
# editswarm

Full-episode long-form packaging. Reverse-engineered from the locked reference episode (host & guest) stack. Works for ~5 minutes to 1+ hour. **Method and visual grammar stay fixed; content comes from the new tape.**

Not for vertical Shorts — use [jedit](../jedit/SKILL.md) for talking-head Shorts.

## Goal
- One **1920×1080 @ 24fps** episode master + **QA ≤ ~160MB** for review.
- Stack: **hook trailer → who-we-are ID open → dead-air body + overlays + DOAC captions → kiss-out**.
- Upload **QA** to Google Drive (anyone-with-link Viewer). Tell the user to **download**. Do **not** post YouTube/social until they QA.
- Keep HQ master local when huge; QA is the review file.

## Inputs (ask only if missing)
- Source video (Drive / Photos / Desktop).
- Episode number + guest name(s).
- Guest LinkedIn (or approved still) for ID circle — **never** a mid-talk Meet grab if a flattering headshot exists.
- Optional: guest podcast / one-line bio chips (no employer pitch on cards unless user explicitly wants an employer/exception card).

## Reference craft (on box when available)
- ID grammar: `local show archive /trailer/id/ID.md` + `make_id*.py`
- Trailer beat: reference episode `TRAILER_V2.md` / reference episode `TRAILER_v3.md`
- Overlay bible: reference episode `overlays/PLACEMENT.md`; hero-graph craft: `inspo_OYg6/NOTES.md` (layout only — no foreign branding)
- Bed: `approved instrumental bed (.wav)` offset **+8.00s** (instrumental). No wall-to-wall music under talk. No Content ID tracks.
- Kiss-out: reference episode `show kiss-out sting (.mp4)` (or current show kiss asset).

---

## Pipeline (do in order)

### 1) Ingest + transcript
1. Download source; probe duration / fps / A/V.
2. Transcribe with timestamps (`transcript.txt` + word-level jsonl if possible).
3. Build a **keep map** for dead-air (silence detect ≈ −35dB, min gap ~0.55s; leave ~0.20s breath on long gaps). Paired `trim`/`atrim` so mouths stay locked.
4. Note chapter themes, hard stats said on tape, cliffhangers, teaching moments (define X).

### 2) Hook trailer (~30–45s) — DOAC energy, Swarm identity
1. **0–3s hard hook** — strongest jaw-drop line on frame 1 + kinetic / lower-third chip.
2. **Topic montage** — 5–7 punches from **different** themes across the episode (~2.5–5s each). Mid-sentence / cliffhanger OK.
3. Prefer: readiness conflict, data-before-scale, spicy project **tease without spoil**, stay-human / can’t automate, one career or labor punch.
4. Short black flashes + `THE SHOW` / `SHOW TAGLINE` type cards between acts.
5. Music: approved instrumental bed under VO (duck ~−4dB under speech; swell on type cards; last punch drier).
6. **Do not resolve** the episode in the trailer — leave open loops.

### 3) Who-we-are ID open (~17.6s)
1. Black + instrumental bed; circle-drop photos + gold ring; grain on **background only**, sharp faces.
2. Order: **HOST** → **CO-HOST** → **GUEST** → lockup.
3. Locked host/co-host bio chips from reference episode ID.md unless user updates them.
4. Guest: LinkedIn (or user still) + concise chips; **no “work wife/husband”**; usually no employer brands on cards.
5. Lockup: `THE SHOW` / `SHOW TAGLINE` / **`EP N`**.

### 4) Body picture lock
1. Start body at natural “hello / welcome” (or agreed cold open). Strip any temporary single-punch cold open once trailer+ID exist.
2. Dead-air cut only — not hyper-choppy. Complete thoughts.
3. Optional host-only natural beauty; guests untouched. No fake 4K.
4. Stings only on open / rare chapter hits / close — silence under conversation (DOAC intimacy).

### 5) DOAC-style captions (body only)
1. Burn ASS on **body talk** only — **no** captions on trailer, ID, or kiss-out.
2. Bold sans (Liberation/Montserrat Bold — **not** Shorts Anton ALL-CAPS).
3. White fill + heavy black outline/shadow; **yellow (#FFE600)** punch word.
4. Lower-center; lift when overlay cards/pillars are on.
5. Chunks ~3–8 words, speech-timed. Map transcript through the keep map so words match mouths. Fix Whisper garbage.

### 6) Overlay system (the retention engine)
Use the transcript to place visuals that **affirm** what is said. Mix types:

| Type | Use |
|------|-----|
| Topic / NOW COVERING chip | Chapter transitions |
| ON THE RECORD / STAT | Numbers said on tape |
| Quote plate | Memorable line |
| Table | Comparisons (skills, tools, ROI) |
| Press / headline | Reputable org framing |
| Hero right pillar (~30–40% width) | Big graph — faces left |
| Teaching define + diagram | Counterfactual, synthetic data, frameworks |
| Guest example flow | Their concrete story (no spoil if trailer teased it) |

**Style lock**
- Dark ~89% rounded card or opaque right pillar; `#F5A623` left/accent bar.
- ALL-CAPS orange header; bold white body; small grey **source line (org + year)**.
- Graphs: orange + blue series; **direct labels on points**; staged reveal when possible (title → axes → draw → labels).
- Hold **6.5–8s** typical; hero graphs **10–12s**. **Never stack two overlays.**
- Dense cadence in the **first ~8 minutes of watching** (~every 25–45s). Continue mid/late on stats, teaching beats, chapter turns.
- Official numbers beat spoken ballparks; quiet-correct on the card without dunking on speakers. Document every figure in `REAL_STATS.md` with URLs. No fake precision.
- Teaching cards: define the concept clearly even if Whisper misheard the word.

### 7) Kiss-out
Append show kiss / JOIN THE SHOW after a short black (peak-end). No captions on kiss.

### 8) Encode + deliver
1. HQ: libx264, sensible CRF (~18–19), yuv420p, AAC, +faststart, 1080p24.
2. QA: recompress to **≤160MB** for Drive review.
3. Proofs: hook 1s, ID guest circle, 3–5 overlay stills, kiss.
4. Drive anyone-with-link Viewer; update a `DRIVE.md`. Prefer Chrome/Drive session for large MP4s (MCP base64 is wrong for ~100MB+ video).
5. Report: open timeline, overlay clock table, Drive URL. **Download to review.**

---

## Stack checklist (final file)
1. Hook trailer (3s punch + topic cliffhangers + type cards + bed)
2. ID open (Host → Co-host → Guest LinkedIn → EP N)
3. Body (dead-air) + DOAC captions + overlays
4. Kiss-out
5. QA on Drive; no YouTube until QA

## Anti-patterns
- Cold open only on co-host/guest; static logo-only open; Meet-still guest circle when LinkedIn exists
- Wall-to-wall music; Shorts Anton captions on long-form; black-box caption banners
- Tiny unreadable lower-thirds; double-stacked cards; spoiling trailer cliffhangers in early overlays
- Invented stats; employer pitch on ID cards unless user exception
- Shipping without mouth-sync check; Drive preview as quality proof

## Iteration
When the user asks for “more overlays at MM:SS” or denser first-N minutes: segment-burn that window, concat, new versioned QA (`vN`), keep prior Drive files unless asked to trash.
