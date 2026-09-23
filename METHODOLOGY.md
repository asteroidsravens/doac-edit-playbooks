# Bohemian Swarm / DOAC Edit Methodology
### Master brief for Claude (and any second editor) — read this BEFORE the skill files

**Audience:** Thomas + Claude.  
**Purpose:** Reproduce Jess’s locked cut quality without Vizzy in the loop. Quality must not drop while we free time for creation.  
**Repo skills (after this doc):** `skills/jedit` · `skills/jtube-thumb` · `skills/editswarm` · `skills/swarm-shorts-elon`

---

## 0. How to use this document (critical)

1. **Read this file top to bottom once** before touching tape.
2. Pick the job type (Short vs long-form) in §1.
3. Follow the **ordered pipeline** for that job — do not skip steps or reorder.
4. Open the matching `SKILL.md` only as the execution checklist for that job.
5. Deliver to Drive for QA. **Never publish YouTube/social until Jess signs off.**
6. When unsure, choose the option that preserves **mouth sync, continuous motion, sourced numbers, and punch in the first 3 seconds**.

Claude: treat every bullet under **HARD RULES** and **NEVER** as non-negotiable. Preferences are not suggestions.

---

## 1. Job types (pick one first)

| Job | When | Skill | Output |
|-----|------|-------|--------|
| **A. Talking-head Short** | Vertical phone/iPad clip of host speaking | `jedit` | 1080×1920 ≤179.5s HQ + Drive link |
| **B. Shorts thumbnail** | After Short pack is locked | `jtube-thumb` | 1080×1920 JPG, soft left fade + WHY |
| **C. Full episode long-form** | Full podcast/Meet tape | `editswarm` | 1920×1080@24fps master + ≤160MB QA |
| **D. Episode-clip Short** | Pull Short from existing episode (no new film) | `swarm-shorts-elon` then craft via `jedit` if 9:16 | ~35–45s, heresy title, binary closer |

Do not mix pipelines. A Short is not a mini long-form. Long-form captions are not Shorts Anton.

---

## 2. North star (what “good” means)

We cut like **Diary of a CEO (DOAC)** / Lex Fridman packaging energy:

- **Hook first** — jaw-drop claim in the first 1–3 seconds. No slow lead-in. No cold open on co-host/guest unless Jess explicitly asks.
- **Retention engine** — visuals that teach while people talk: sourced graphs, stats, quote plates, tables, teaching defines. Viewers should *learn*, not just hear.
- **Dopamine without cheap tricks** — variety of chart types, clear takeaway cards, continuous live motion (never freeze-frame pads).
- **Credibility** — every number on screen has a real source (org + year). Official data beats spoken ballparks. Never invent precision.
- **Voice wins** — music is felt in pauses, ducked under consonants. Phone-speaker test: every word clear.
- **Show-don’t-tell** — after a graph (~5s on Shorts / 6.5–8s long-form), a second card translates what it *means*.

Brand grammar (Bohemian Swarm):

- Gold accent `#F5C518` / `#F5A623` (Swarm gold/orange) — **not** McDonald’s red, not generic TikTok yellow for brand.
- Shorts punch word in captions: Swarm gold. Long-form punch word: yellow `#FFE600`.
- Edge-pinned overlays for porch/graphic Shorts (top WHY bar + bottom fact plates), not floating mid-frame junk.
- Soft **left fade of the same image** on thumbs — never a black box / hard seam across a face.

---

## 3. Global HARD RULES (all jobs)

### 3.1 Order of operations (always)

1. Ingest source → probe A/V  
2. Transcribe with timestamps (word-level if possible)  
3. Build keep map / cut plan **and get it approved if Thomas is new to the tape**  
4. Picture lock (dead-air only) **before** captions/overlays  
5. Captions  
6. Overlays / cards / graphs (sourced)  
7. Music bed (if any) ducked  
8. Encode HQ  
9. Proof stills + QC checklist  
10. Drive upload (anyone-with-link) → tell reviewer to **download**  
11. Hold YouTube until Jess QA  

Never burn overlays onto a rough cut you plan to retime later. Never publish from Drive’s in-browser preview judgment.

### 3.2 NEVER

- **NEVER** extend duration with freeze-frame / visual hold / screen pause. Jess flagged frozen opens and weird pauses. To make room for cards, **recut from the live master** and burn overlays on **continuous motion**.
- **NEVER** invent stats, prices, cert costs, or “BLS” labels on spoken pay. Mark unknowns `UNKNOWN`. Document every figure in `REAL_STATS.md` with URLs.
- **NEVER** stretch faces in thumbs. **NEVER** black-slab left column on thumbs.
- **NEVER** open a Short with greeting / “hey friends” / co-host face if the punch is elsewhere — punch in **first 3 seconds**.
- **NEVER** wall-to-wall music under talk. **NEVER** trending/library tracks with Content ID on Shorts >1:00 (global block risk). Original instrumental only.
- **NEVER** double-stack overlays. One card/graph at a time.
- **NEVER** ship silent audio keeps (iPad HEVC silent-voice bug — see §4).
- **NEVER** post YouTube/social before Jess signs off.
- **NEVER** use Shorts Anton ALL-CAPS captions on long-form (wrong grammar).
- **NEVER** use Meet mid-talk still for guest ID if LinkedIn/headshot exists.

### 3.3 Long rants & repetition (critical for Claude)

When the host goes long, winds, or repeats:

1. **Keep every distinct point** — do not delete ideas to “make it short.”
2. **Cut repetition and dead air** — same sentence twice → keep the clearer take.
3. **Keep complete thoughts** — do not chop mid-clause. ~40ms pad so words aren’t clipped.
4. **Hard cuts on breaths inside a clip**; **0.12s** A/V crossfade only **between** different source clips.
5. After picture lock, use overlays to **carry** the dense info (stat → takeaway) so the rant becomes teachable, not boring.
6. For debate Shorts: keep balanced pushback when it’s a dialogue; don’t flatten the other voice unless Jess asks.

Pattern that worked on porch/debate packs: tighten CLIP rant by removing repetition/dead air **while keeping all points**, then layer Swarm graph/stat/WHY cards + DOAC captions.

---

## 4. Job A — Talking-head Short (`jedit`)

### 4.1 Specs

- **1080×1920**, ≤ **179.5s** hard cap  
- Encode from **original HEVC**, one generation: `libx264` preset **medium**, **CRF 12**, yuvj420p, pc/full, bt709  
- Target ~20–26 Mbps. Large file (~500MB+ for ~3 min) is **correct**. No `veryfast`.  
- Deliver Drive HQ; say “download — Drive preview looks softer.”

### 4.2 Source traps

- iPad Pro often **1920×1080 with rotation −90** → FFmpeg autorotate to 1080×1920.  
- **Never extra transpose** (flips speaker).  
- After autorotate, **do not scale/pad** if already 1080×1920.  
- **Silent-voice bug:** `-ss` after `-i` on mid-file in-point → picture moves, audio silent. Fix with `atrim`+`asetpts` from original AAC (or `-ss` before `-i` for audio-only). Verify **RMS on every keep**, not just the first.

### 4.3 Cut

1. Transcribe with word timestamps.  
2. Cold open on the **claim**. Drop greeting-only opens.  
3. Keep windows = complete thoughts.  
4. Loop close if tape returns to first line; hard cut end; no fade-to-black.

### 4.4 Captions (Shorts grammar)

- Burned from frame 1.  
- **2–4 words**, ALL-CAPS **Anton**, white + black stroke (~outline 5).  
- One **Swarm-gold** punch word `#F5C518` (ASS BGR `&H18C5F5&`).  
- Lower-middle: PlayRes 1080×1920, Alignment 2, **MarginV ~430** (clears Shorts UI + mouth).  
- Not a black box. Not a full sentence. Caption-led. Fix Whisper garbage. As-said only.

### 4.5 Overlay cards (Shorts)

- Dark rounded plate `(16,16,16,232)`, gold left bar `#F5C518`, gold ALL-CAPS header, white body, small source line.  
- Top of frame, not over mouth.  
- Full-frame transparent PNG; overlay with enable between(t,s,e). Do not `-loop 1 -t` a stack of full-frame PNGs.  
- Proof names/certs/exchanges as said. No fake BLS labels.

### 4.6 Porch / graphic Shorts overlays (extra grammar)

When the Short is porch debate / policy / teaching (not pure talking-head card style):

- **Narrative flow first** — cards frame; no choppy flash-cuts.  
- **Edge-pinned** layout (333 Part 1/2 pin style) but **Swarm colors only** (no McD red):  
  - Top bar flush y=0: brand + **WHY question**  
  - Bottom: white fact plates that **update with speech**  
- Chart **variety**: line, pie, bubble, bar/column, tables, big stat slams, meters.  
- Hold each graph **~5s**, then a **second takeaway card** that translates meaning.  
- Vertical: **DOAC-style blur fill** so full faces stay in frame — no black box, no weird zoom crop.  
- Music: Swarm intro-style bed ducked under debate (not wall-to-wall over the open). Pack audio reference: porch CLIP_05-style bed level after ~2.5s.  
- Max encode quality.

### 4.7 Music

- Original instrumental only. ~122 BPM, upbeat, no vocals.  
- Sidechain-duck under VO. Hits/risers on **section changes** only (handful).  
- Phone-speaker test.

### 4.8 QC before Drive

- Upright, not mirrored; wardrobe/props match source.  
- Duration ≤179.5s; A/V start together; RMS on every keep.  
- Proof stills: hook, each card, mid, close. Continuous motion from frame 1.

---

## 5. Job B — Shorts thumbnail (`jtube-thumb`)

Do this **after** the Short cut is locked.

1. Strongest flattering still (mouth closed; no mid-word / mid-squawk unless disaster *is* the hook).  
2. **Never stretch.** Scale-to-cover, center-crop bias to eyes.  
3. Soft **left fade/blur of the same image** into type column — **no black box / hard seam across face**.  
4. Type: heavy condensed ALL-CAPS, white + one gold punch, black stroke; left stack; off the face.  
5. Copy = **WHY click** in ≤3 short lines (curiosity gap), not a synopsis. Optional small pill (`SATURDAY 9:05`).  
6. 1080×1920 JPG. Offer primary + one alt; Jess locks.  
7. Hold YouTube until she says go.

---

## 6. Job C — Full episode long-form (`editswarm`)

Locked reverse-engineer of Ep7-quality Swarm long-form. Method fixed; content from new tape.

### 6.1 Stack order (do not reorder)

1. Hook trailer (~30–45s)  
2. Who-we-are ID open (~17.6s)  
3. Body (dead-air) + DOAC captions + overlays  
4. Kiss-out  
5. Encode HQ + QA ≤160MB → Drive

### 6.2 Step 1 — Ingest + transcript

- Probe duration/fps/A/V.  
- Transcript + word jsonl.  
- Dead-air keep map: silence ≈ −35dB, min gap ~0.55s, leave ~0.20s breath. Paired trim/atrim for mouth lock.  
- Note: chapter themes, hard stats on tape, cliffhangers, teaching “define X” moments.

### 6.3 Step 2 — Hook trailer (DOAC energy)

1. **0–3s hard hook** — strongest jaw-drop line on frame 1 + kinetic/lower-third chip.  
2. Topic montage: 5–7 punches from **different** themes (~2.5–5s each). Mid-sentence/cliffhanger OK.  
3. Prefer: readiness conflict, data-before-scale, spicy project tease **without spoil**, stay-human/can’t automate, one career/labor punch.  
4. Short black flashes + `BOHEMIAN SWARM` / `PRACTITIONERS, NOT PUNDITS` type cards between acts.  
5. Approved instrumental bed under VO (duck ~−4dB under speech; swell on type cards; last punch drier). Offset bed **+8.00s** when using the locked Lofi instrumental.  
6. **Do not resolve** the episode in the trailer — leave open loops.

### 6.4 Step 3 — Who-we-are ID open

1. Black + bed; circle-drop photos + gold ring; grain on **background only**, sharp faces.  
2. Order: **HOST (Jess) → CO-HOST (Thomas) → GUEST → lockup**.  
3. Locked bio chips unless Jess updates. Guest: LinkedIn still + chips; no “work wife/husband”; usually no employer brands.  
4. Lockup: `BOHEMIAN SWARM` / `PRACTITIONERS, NOT PUNDITS` / **`EP N`**.

### 6.5 Step 4 — Body picture lock

- Start at natural hello/welcome (or agreed cold open).  
- Dead-air only — not hyper-choppy. Complete thoughts.  
- Optional host-only natural beauty; guests untouched. No fake 4K.  
- Stings only on open / rare chapter / close — **silence under conversation** (DOAC intimacy).

### 6.6 Step 5 — DOAC captions (body only)

- ASS on body talk only — **no** captions on trailer, ID, kiss-out.  
- Bold sans (Liberation/Montserrat Bold) — **not** Shorts Anton.  
- White + heavy black outline; **yellow `#FFE600`** punch word.  
- Lower-center; lift when overlay cards on.  
- Chunks ~3–8 words, speech-timed through keep map. Fix Whisper garbage.

### 6.7 Step 6 — Overlay system (retention engine)

Place visuals that **affirm** what is said. Mix types:

| Type | Use |
|------|-----|
| Topic / NOW COVERING chip | Chapter transitions |
| ON THE RECORD / STAT | Numbers said on tape |
| Quote plate | Memorable line |
| Table | Comparisons (skills, tools, ROI) |
| Press / headline | Reputable org framing |
| Hero right pillar (~30–40% width) | Big graph — faces left |
| Teaching define + diagram | Counterfactual, synthetic data, frameworks |
| Guest example flow | Concrete story (no spoil if trailer teased it) |

**Style lock**

- Dark ~89% rounded card or opaque right pillar; `#F5A623` left/accent bar.  
- ALL-CAPS orange header; bold white body; small grey **source line (org + year)**.  
- Graphs: orange + blue series; **direct labels on points**; staged reveal when possible (title → axes → draw → labels).  
- Hold **6.5–8s** typical; hero graphs **10–12s**. **Never stack two overlays.**  
- Dense cadence in the **first ~8 minutes of watching** (~every 25–45s). Continue mid/late on stats, teaching beats, chapter turns.  
- Official numbers beat spoken ballparks; quiet-correct on the card without dunking on speakers. Every figure in `REAL_STATS.md` with URLs.  
- Teaching cards: define clearly even if Whisper misheard the word.  
- Long critical rants / dense teaching: this is where overlays earn their keep — graph then takeaway so viewers stay engaged through the long wind.

### 6.8 Step 7 — Kiss-out

Append Swarm kiss / JOIN THE SWARM after short black (peak-end). No captions on kiss.

### 6.9 Step 8 — Encode + deliver

- HQ: libx264 CRF ~18–19, yuv420p, AAC, +faststart, 1080p24.  
- QA ≤160MB.  
- Proofs: hook 1s, ID guest circle, 3–5 overlay stills, kiss.  
- Drive anyone-with-link; update `DRIVE.md`. Report open timeline + overlay clock table + URL. **Download to review.**

### 6.10 Long-form anti-patterns

- Cold open only on co-host/guest; static logo-only open; Meet-still guest circle  
- Wall-to-wall music; Shorts Anton on long-form; black-box caption banners  
- Tiny unreadable lower-thirds; double-stacked cards; spoiling trailer cliffhangers early  
- Invented stats; employer pitch on ID cards unless Jess exception  
- Shipping without mouth-sync check; Drive preview as quality proof

---

## 7. Job D — Episode-clip Short (`swarm-shorts-elon`)

No new filming. Package moments from existing episodes.

### Formula

1. Named famous person OR named fear  
2. A heresy (the claim)  
3. Completes in ~35–45s (prefer ≤45; hard ~60)  
4. **Title IS the heresy** — never “Ep N …”  
5. Ends on a **binary question** (“Are you getting paid?” / “Would you leave?”)

### Cut rules

- Hard start on claim; hard end on question.  
- Cold open — no preamble, no trailer voice.  
- Approve cut plan (IN/OUT + title + closer) before burning tokens.  
- Use `jedit` craft when delivering 9:16 talking-head.  
- First frame: face mid-sentence (or existing mascot on tape).  
- On-screen text: title, 4–8 words, huge Anton caps.  
- Description: one sentence + link to **specific episode**.  
- Weekly cap mindset: ~5 Shorts; post one/day; winners get longer packaged cut later.

Niche wants a sentence that feels slightly illegal and already lives in the body (power bill/town/job rewritten; someone paid off my work; race real / official story incomplete). Not tokenomics or episode labels as the lead.

---

## 8. Preference cheat-sheet (Jess locks)

| Preference | Rule |
|------------|------|
| Punch timing | First **3 seconds** — no slow lead-in |
| Motion | Continuous live tape; **no freeze pads** |
| Short captions | Anton 2–4 words, gold punch, MarginV ~430 |
| Long captions | Sans bold, yellow punch, body only |
| Graphs Shorts | Variety; ~5s then takeaway card |
| Graphs long-form | 6.5–8s (hero 10–12s); dense first ~8 min |
| Thumbs | Soft same-image left fade; flattering mouth-closed; WHY curiosity |
| Vertical faces | DOAC blur fill; no black box crop |
| Music | Original/instrumental; ducked; Content-ID safe |
| QA | Drive download; Jess sign-off before YouTube |
| Rants | Cut repetition/dead air; **keep all distinct points** |
| Debate Shorts | Keep pushback; balance; overlays for clarity/credibility |
| Colors | Swarm gold/white/charcoal — no McD red |
| Overlays porch | Edge-pinned top WHY + updating bottom fact plates |

---

## 9. Delivery template (every handoff)

```
JOB: [A/B/C/D]
SOURCE: [path or Drive]
CUT PLAN: [approved IN/OUT or keep map]
OUTPUT HQ: [path]
OUTPUT QA: [path / size]
DRIVE: [anyone-with-link URL] — DOWNLOAD to review
OVERLAY CLOCK: [MM:SS type — source]
REAL_STATS.md: [yes/no]
PROOF STILLS: [hook / cards / mid / close]
HOLD: YouTube + social until Jess QA
```

---

## 10. Suggested Claude session prompt (Thomas)

Copy-paste to start a Claude edit session:

> You are cutting Bohemian Swarm to Jess’s locked DOAC/Swarm methodology.  
> Read `METHODOLOGY.md` first, then the matching skill under `skills/`.  
> Follow HARD RULES and NEVER lists exactly.  
> Punch in first 3 seconds. No freeze-frames. Sourced overlays only.  
> Dead-air cut; keep all distinct points when tightening rants.  
> Deliver Drive QA and wait for Jess before YouTube.  
> Job type today: [A/B/C/D]. Source: [link]. Episode/clip notes: […].

Then point Claude at this repo and the specific skill file.

---

## 11. Skill map (read after this doc)

1. [`skills/jedit/SKILL.md`](skills/jedit/SKILL.md) — talking-head Shorts  
2. [`skills/jtube-thumb/SKILL.md`](skills/jtube-thumb/SKILL.md) — thumbs  
3. [`skills/editswarm/SKILL.md`](skills/editswarm/SKILL.md) — full episode  
4. [`skills/swarm-shorts-elon/SKILL.md`](skills/swarm-shorts-elon/SKILL.md) — episode-clip Shorts formula  

---

*Locked craft distilled from Vizzy/Jess edit logs (porch Shorts, Ep7 long-form, debate packs, JTube thumbs). When craft upgrades, update this file first, then the skill files.*