---
name: jedit
description: >-
  Use this when you get a talking-head clip (iPad/phone vertical or
  rotate-flagged HEVC) to cut as a show YouTube Short the jedit way —
  same as the locked “You can’t prompt a substation” HQ download.
---
# jedit

Show talking-head Shorts, locked to the HQ download of “You can’t prompt a substation” (2026-08-31). Same treatment every time. Do not invent a new look.

## Goal
- One vertical YouTube Short, **1080×1920**, **≤ 3:00** (hard cap 179.5s).
- Keep the speaker’s flow. Dead-air only. Not choppy. Complete thoughts. Mouth-synced on delivery.
- Deliver a **Google Drive** anyone-with-link file. Tell the reviewer to **download** it. Drive’s in-browser player transcodes and looks worse than the file.
- Do **not** post or schedule YouTube/social until the show owner QAs.

## Source
- Prefer the handed file (Photos/Drive/Desktop). iPad Pro HEVC is often **1920×1080 with rotation −90**. FFmpeg autorotates to 1080×1920.
- **Never extra transpose.** That flips the speaker.
- After autorotate, **do not scale**. No pad-to-fit if it is already 1080×1920.

## Cut
- Transcribe with word timestamps.
- Cold open on the claim. Drop “hey friends” if the first beat is just a greeting.
- Keep windows = complete thoughts, ~40ms pad so words are not clipped.
- Hard cuts on breaths **inside** a clip. **0.12s** audio+video crossfade only **between** source clips.
- Loop close if the tape returns to the first line. Hard cut end, no fade-to-black.

## Audio (the silent-voice bug)
- iPad HEVC: **`ffmpeg -ss` after `-i` on a mid-file in-point yields silent audio** with picture still moving.
- Extract voice with **`atrim` + `asetpts=PTS-STARTPTS`** from the original AAC (or `-ss` **before** `-i` for audio-only).
- Rebuild voice from those atrims, then mux. Verify RMS on every keep, not just the first keep of each clip.
- If a later keep’s RMS is ~0, the extract method is wrong. Fix audio. Do not ship.

## Picture encode (HQ)
- Rebuild from the **original HEVC**, one generation. Do not encode from a prior H.264 master.
- `libx264` **preset medium**, **CRF 12**, **yuvj420p**, **pc/full range**, **bt709**.
- **No `veryfast`.** No second-generation recode for audio (audio fix = `-c:v copy`).
- Target ~20–26 Mbps at 1080×1920. File will be large (~500MB+ for ~3 min). That is correct.

## Captions
- Burned in from frame 1.
- 2–4 words, ALL-CAPS **Anton**, white + black stroke (outline ~5).
- One Swarm-gold punch word (`#F5C518`, ASS BGR `&H18C5F5&`).
- Lower-middle: PlayRes 1080×1920, Alignment 2, **MarginV ~430**. Clears Shorts buttons and the speaker’s mouth.
- Not a black box. Not a full sentence. Caption-led. Fix Whisper garbage (do not burn “NURCSERT”, “AI TIPS”, etc.). As-said only.

## Overlay cards
- Dark rounded plate `(16,16,16,232)`, gold left bar `#F5C518`, Archivo/Anton gold ALL-CAPS header, white body, small source line.
- Top of 1080×1920, not over the speaker’s mouth.
- Full-frame transparent PNG. Overlay with `eof_action=repeat:enable='between(t,s,e)'`. Do **not** `-loop 1 -t` five full-frame PNGs.
- Proof on screen as it is said (names, certs, exchanges). **Do not label spoken pay as BLS.** Official cert/cost only when sourced. Mark unknown prices UNKNOWN. Do not invent.

## Music
- **Original instrumental only.** No trending songs, no library track with Content ID. A Short **>1:00 + Content ID = global block**.
- ~**122 BPM**, upbeat, major/bright. Kick/clap/hats + bass + pluck. No vocals.
- Sidechain-duck under VO so the bed is felt in pauses and gets out of the way of consonants. Hits/risers on **section changes** only (a handful, not every cut).
- Voice wins. Phone-speaker test: every word is clear.

## Thumb
- Never stretch the base photo. Unstretched frame, natural **left fade of that same image**, then type. No black slab.
- Type off the face. Yellow brand pill. Hook in Archivo/Oswald, gold on the punch line.

## QC before Drive
- Upright (not sideways/mirrored). Wardrobe / props match source.
- Duration ≤ 179.5s. A/V start together. Voice RMS present on **every** keep.
- Proof stills: hook, each card, a mid-job, close.

## Delivery
- Upload the HQ file to the show Drive. Anyone-with-link viewer.
- One link. Say: download it, Drive preview will look softer.
- Hold YouTube + social until the show owner signs off.
