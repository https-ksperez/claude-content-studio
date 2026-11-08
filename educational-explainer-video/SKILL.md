---
name: educational-explainer-video
description: Make vertical educational explainer videos with code (stop-motion React scenes to MP4, AI-voiced title cards, music, narration script, interactive page, social copy). Use for any explainer, tutorial, Reel/TikTok lesson or series chapter, even if code or stop-motion isn't mentioned.
---

# Educational explainer videos, built with code

This skill makes short vertical explainer videos (typically 60–135 s, 1080×1920) that teach one topic in clear chapters. Every frame is drawn by code as a pure function of time, so the video is deterministic and editable, and characters, logos and colors stay identical in every shot. A change request means editing a constant and re-rendering, not regenerating footage.

The house style comes from a finished Spanish series about Supabase (Auth, Database, and "Supabase + AI: From Sensors to Intelligence"). It is a hand-made stop-motion look at 12 fps: cardboard and clay cut-outs on a dark studio set, letters typed in one by one, chapter title cards that slam, slide or sweep in while a voice reads them, and a closing with the brand logo and slogan. The style system below is the default. The discovery interview lets each user change the palette, the look and the story.

## What you deliver

Each video is a package. Name files after the topic, e.g. `supabase_auth_9x16.mp4`.

1. **MP4**: 1080×1920, H.264 + AAC, `+faststart`. Encode at 24 fps with each 12 fps drawing held for two frames.
2. **Audio track (WAV)**: music, SFX and the title-card voice, with room left for the creator's narration.
3. **Source component (`.jsx`)**: one self-contained React file. It renders both the video (`renderMode`) and the interactive web version.
4. **Interactive web page**: published as an artifact when the session can publish. It shows a phone frame with player controls, tappable pieces that pause the video and open an info sheet, and a per-chapter explore panel. Republishing to the same URL keeps the link.
5. **Recording script (`.md`)**: per scene, the title-card line (AI voice), the exact window in which to record, and the narration text that fits the window.
6. **On request**: social copy for Instagram, LinkedIn and TikTok, a WhatsApp/community message, or a thumbnail frame.

Send the files with the session's file-delivery tool. If the session is attached to a Project, also save the brief and the recording script there.

---

## Step 0 — Discovery interview (first use)

Before writing anything, look for an existing brief: a `video-brief.md` in the attached Project, the working folder or memory.

- **No brief yet**: run the interview below. A wrong guess about goal, palette or narration costs a full re-render, while a question costs one message.
- **Brief exists** (for example, the next chapter of a series): don't re-ask the style questions. Confirm in one line that you'll reuse it, then ask only what's new: the topic, the real facts or architecture, characters, and anything the user wants changed.
- **The user hands you a script**: still run the interview, but use it to check and adapt their script to this format (Step 1). Don't skip ahead to building.

Use the multiple-choice question tool if the session has one: up to 4 questions per call, 2–4 options each, with the recommended option first. Otherwise ask in plain text. Ask in two short rounds, and write the user's own words into the brief.

**Round 1 — the video**
1. *Goal*: what should a viewer understand or be able to do after watching? Ask for the one sentence they want people to remember. Options might be "explain what X is to beginners", "show how X works step by step", "present a project I built", "promote a product or feature".
2. *Audience and level*: total beginners (use everyday analogies such as "a database is like Excel with superpowers"), people who already code, or technical peers.
3. *Platform and length*: Instagram/TikTok/Shorts/LinkedIn. One to two minutes is fine when the video teaches something; retention depends more on the hook than on length. Suggest about 6 s per intro, 6–10 s per scene and 3.5–4 s per title card. Five to nine chapters work well.
4. *Language and voices*: what language is the video in? Will the creator record their own narration (the default, which saves TTS credits)? Should a second, AI voice read only the chapter title cards? Which voice or TTS connector, and is there a credit budget?

**Round 2 — the look and story**
1. *Palette*: offer the options in "Palettes" below. (a) brand-dark studio with one accent color (default; Supabase used #3ECF8E); (b) research-based light paper and ink for classroom-style teaching; (c) the user's own hex colors or brand guide. Ask for the official logo file if a brand appears; never redraw a logo.
2. *Visual style*: (a) 12 fps stop-motion cut-outs (default, no GPU needed); (b) smooth motion graphics at 24/30 fps with the same engine and stepping off; (c) isometric 3D with Three.js (heavier, needs a GPU for comfortable render times; see "3D variant").
3. *Story device*: a named character the viewer follows (for example "Esperancita", the grandmother wearing the sensor), named users acting out the concept (Ana, Luis, a visitor), or objects only. Ask for names.
4. *Closing and identity*: brand slogan in the video's language, the creator's handle or sign-off line, and any call to action.

Also collect, whenever the topic involves real systems:
- **The true architecture and facts**: which component does what, real module names and labels. Also ask for the "do not claim" list. For example: Supabase stores and serves data but does not train the model; the ESP32 does not write to Postgres directly; MQTT is not Supabase Realtime; no invented metrics; no clinical claims; no credentials on screen.
- **Series context**: chapter order and which earlier file to reuse the engine from. Ask too whether the series numbering should appear anywhere public. The creator may not want "chapter 3" in a post.

Save the answers to `video-brief.md`: goal, audience, platform, length, language, voices (voice id or name), palette tokens, fonts, style, characters, closing lines, the do-not-claim list and series info. Show the user a 5-line summary of the brief, then continue.

---

## Step 1 — Script and scene plan (get approval before building)

A script is cheap to change and a render is not. Deliver the scene table first and let the user react.

**Shape of a video**
- **Intro (≈6 s)**: a hook question in the first 2 s, the topic name typed in, and the character introduced with a name tag that is already attached to them.
- **Chapters (6–10 s each)**: one idea per chapter. Each one opens with a title card: a title of 1–3 words plus a short subtitle that says why it matters, e.g. "MQTT. El cartero de tus sensores."
- **Closing (≈7 s)**: the brand logo, the brand name and the slogan typed line by line, then a fade to black. Leave the character out of the closing. Use the user's slogan or the brand's official slogan in the video's language (e.g. "Supabase / Construye en un fin de semana / Escala a millones").

**Writing rules (learned from user corrections)**
- **Keep what is essential and useful for someone learning.** Cut anything that adds noise, even when it's true. In the AI chapter, the pulse-oximeter sensor was part of the real project but not of this story; viewers would ask "when was that used?", so it was removed and saved for another video.
- **Use one anchoring analogy, stated once, early.** Don't repeat it at the end; the end belongs to the brand slogan.
- **Avoid references the audience may not know.** A spreadsheet-function comparison (VLOOKUP/BUSCARV) was replaced with "Link, don't copy" because even the creator didn't know what the function did.
- **Explain how the data or the result came to exist.** For machine learning, show how the labels were obtained (a capture program that told the tester when to walk and when to simulate a fall, so each reading got label 0 or 1). That step is what makes the rest believable.
- **Be faithful to the architecture.** Show who does what, in the true order, and keep the do-not-claim list. Values, confidence scores and algorithms shown on screen are demo values unless the user gives real ones; say so in the script notes.
- **Check facts about real products** against official docs before stating them, e.g. which plans include backups, or what must be enabled for Realtime.
- **Keep risky actions on a stand-in.** If a scene shows something risky, a separate "test person" performs it, not the main character.

**Word budget for the creator's narration**: about 2.2–2.5 spoken words per second of window, leaving about 0.5 s of air. A 9 s window holds about 20 words. Flag windows that are tight and offer a shorter line.

**Script table format** (also the final recording script):

| Scene | Title card (AI voice) | Record between | Narration |
|---|---|---|---|
| Intro | — | 0:00 – 0:06 | Hook question + "let's see how, with X." |
| Sensors | "Sensors. Motion, turned into data." | 0:10.0 – 0:19.0 | … |

Add notes underneath for the key moments the narration should land on (e.g. "the fall happens at 0:54.5"), which values are demo values, and what was deliberately left out.

---

## Step 2 — Title-card voice first (audio-first timing)

Generate the AI voice for each title card before animating. The card's length comes from the speech, not from a fixed 2 s.

- Generate each line once. Each TTS call costs credits, so cache the clips and never regenerate a clip to fix timing. Retime the visuals instead.
- Trim and tighten each clip:
  `ffmpeg -i in.wav -af "silenceremove=start_periods=1:start_threshold=-45dB:start_silence=0.05,areverse,silenceremove=start_periods=1:start_threshold=-45dB:start_silence=0.05,areverse,atempo=1.08,aresample=48000" out_t.wav`
- Measure each trimmed clip with `ffprobe`. Card length in frames: `round((0.30 s entrance + speech + ~0.5 s air) × 12)`, typically 41–50 frames (3.4–4.2 s).
- Some TTS connectors return the audio as large base64 JSON that gets saved to a file instead of shown. Decode it with Python (`json` + `base64`) rather than reading it into context.
- The series used Speko → Cartesia voice "Fernanda" (es-MX, model `sonic-3.5`), but use whatever voice the brief names. Without a voice track, the web page can fall back to the browser's `speechSynthesis` for the card lines.

---

## Step 3 — Build the component

### Architecture

Write one React file (React 18 + Framer Motion + lucide-react + Tailwind). The only bitmap is the official logo, embedded as a data URI. Draw everything else with layered SVG, CSS gradients and transforms. Other brands appear as objects with their name written on them (an "ESP32" board, a "Raspberry Pi"), not as their logos.

- Design on a **360×640 canvas** and scale it ×3 to 1080×1920.
- **Timeline**: `SCENE_BASE` holds scene ids, labels, card titles and subtitles, and lengths. `CARD_FRAMES` holds each title card's length in frames, measured from the voice. The `SCENES` array with absolute start and end times is derived from both, so a change in one card's length shifts everything after it automatically.
- **Layer order** in the root: `Backdrop` → scenes (each mounted only while `sceneVisible`) → name tags and hotspots → `Captions` → `TitleCards` → `FilmLayers` (grain, vignette, flicker) → `Hud`.
- **`renderMode`**: show only the canvas at 1080×1920 and expose `window.__smSeek(frame)` and `window.__smTotal`. Outside render mode, wrap the canvas in a phone frame with controls.
- **Audio-master sync**: when an `audioSrc` is playing, the picture follows `audio.currentTime`, so there is no drift. Browsers need a tap before playing sound, so the deck has a sound button.
- **For a big file, write it in parts** (`p1_head` constants and timeline, `p2_art` drawn objects, `p3_scenes_a`, `p4_scenes_b`, `p5_tail` captions, cards, hotspots and root) and concatenate them with a small script. Edits stay local, and engine blocks can be copied unchanged from the previous chapter of a series instead of being rewritten.

### Engine core (copy and adapt)

```jsx
const FPS = 12, W = 360, H = 640;
const CARD_FRAMES = [0, 48, 46, 45 /* … one per scene; 0 for the intro */];
const SCENE_BASE = [
  { id: "intro", label: "Intro", len: 6 },
  { id: "sensors", label: "Sensors", card: "Sensores", sub: "El movimiento, convertido en datos", len: 9 },
  // …
];
const SCENES = (() => { let at = 0; return SCENE_BASE.map((b, i) => {
  const cardLen = CARD_FRAMES[i] / FPS; const start = i === 0 ? 0 : at + cardLen;
  at = start + b.len; return { ...b, cardLen, start, end: at }; }); })();
const DURATION = SCENES.at(-1).end, TOTAL = Math.round(FPS * DURATION);
// Scene-local time; frozen at first/last frame while a title card covers it.
const sceneTime = (i, t) => clamp(t, SCENES[i].start, SCENES[i].end) - SCENES[i].start;
const sceneVisible = (i, t) => t >= SCENES[i].start - 0.3 && t <= SCENES[i].end + 0.3;

const clamp = (v, lo = 0, hi = 1) => Math.min(hi, Math.max(lo, v));
const lerp = (a, b, p) => a + (b - a) * p;
const prog = (t, a, b) => clamp((t - a) / (b - a));
const easeOutCubic = (p) => 1 - Math.pow(1 - p, 3);
const springCurve = (p, k = 5.2, w = 12) => { if (p <= 0) return 0; if (p >= 1) return 1;
  return (1 - Math.exp(-k * p) * Math.cos(w * p)) / (1 - Math.exp(-k) * Math.cos(w)); };
const popIn = (t, t0, dur = 0.4) => springCurve(prog(t, t0, t0 + dur));
// Quantize any easing into n held steps (for Framer Motion transitions at 12 fps).
const stepped = (n, fn = (p) => p) => (p) => (p >= 1 ? fn(1) : fn(Math.floor(p * n) / n));
const rand = (n) => { const x = Math.sin(n * 127.1 + 311.7) * 43758.5453123; return x - Math.floor(x); }; // never Math.random
const kf = (x, xs, ys) => { if (x <= xs[0]) return ys[0];
  for (let i = 1; i < xs.length; i++) if (x <= xs[i]) return lerp(ys[i-1], ys[i], (x - xs[i-1]) / (xs[i] - xs[i-1]));
  return ys.at(-1); };
// "Boil": hand-made jitter that changes every 2 frames; m = 0 under reduced motion.
const boil = (amb, id, m = 1) => { const b = Math.floor(amb / 2);
  return { x: (rand(b*1.37+id*9.1)-.5)*1.3*m, y: (rand(b*2.11+id*4.7)-.5)*1.3*m, r: (rand(b*3.07+id*7.3)-.5)*.8*m }; };
// A piece dropped on the table: fall, two bounces, squash on contact.
const dropPose = (t, t0, fall = .42, bounce = .5, h0 = 520) => { const f = prog(t, t0, t0 + fall);
  if (f < 1) return { y: -h0 * (1 - f*f), sx: 1, sy: 1, rz: lerp(-8, 0, f) };
  const b = prog(t, t0 + fall, t0 + fall + bounce), h = Math.abs(Math.sin(b*Math.PI*2)) * 24 * (1-b);
  const c = h < 4 && b < .95 ? 1 - b : 0; return { y: -h, sx: 1 + .05*c, sy: 1 - .08*c, rz: Math.sin(b*Math.PI*3)*3*(1-b) }; };
```

**The clock** (`useStopMotionClock`) advances whole frames at 12 fps with a requestAnimationFrame accumulator. It keeps `frame`, the timeline position, and `amb`, an always-running counter that drives the boil so the picture stays alive while paused. It exposes `seek`, `play`, `pause`, `stepFrame(±1)` and `stepScene(±1)`. In render mode it sets `frame = amb = f` inside `__smSeek`, so every render is identical.

**`StopText`** types text letter by letter at `cps` characters per second. Each letter gets a small seeded tilt and boil, the newest letter pops at a scale of 1.28, and at `end` the letters fall away with rotation. Use it for every on-screen sentence; text never fades in as a block.

### Style system

**Palettes** (store them as tokens in a `C` object and use nothing else):

*(a) Brand-dark studio (default)*: studio `#121212`, slate `#1C1C1C`, accent `#3ECF8E` (high `#9BF7C9`, low `#1C8F5C`), paper `#F2F0EA`, ink `#EDEDED`, alert `#E5484D` (high `#FF8A8E`). Swap the accent for the user's brand color and derive its high and low tints.

*(b) Research-based light teaching palette*: paper `#F2ECDF` (tile `#E7DFCD`), ink `#1B1B1B` (not pure black), soft ink `#55504A`, flat shadow `#2F4BA8` at 32 %, one fixed color per concept (e.g. `#2F4BA8`, `#2E8B66`, `#FFC24A`, `#F0521E`), and data cards in lime `#B6F23A` on `#0E0F14`. The rules behind it:
- Keep the world neutral and give strong color only to what is being explained right now.
- The same color ties together the spoken keyword, the object and the diagram.
- Never rely on color alone; add a label or a shape.
- Text contrast is at least 4.5:1 (3:1 for large text); check it with a script.
- Use blue and orange as the main pair, which is safe for color-blind viewers.
- Paper mode is for explaining and dark mode is for data; don't mix the two in one shot.

*(c) Custom*: take the user's hex values, assign them to the same roles, and check contrast.

**Type**: Bricolage Grotesque 500–800 for display and JetBrains Mono for eyebrows, data and the HUD. For the light teaching palette, Lexend (titles), Atkinson Hyperlegible (captions) and JetBrains Mono (numbers) are a strong set. For local rendering, inline the fonts as base64 `@font-face` (for example from `@fontsource`) so frames never render with a fallback font.

**Materials** (cut-out and clay look):
- **Clay pieces**: a 155° gradient (`#282828 → #1C1C1C → #151515`), an inset top highlight and a bottom shade, plus a **hard offset shadow** (`4px 6px 0 rgba(0,0,0,.62)`). Never use soft drop shadows.
- **Paper tags**: paper color with dark ink text and a hard shadow. Use them for names and labels.
- **Grain overlay**: SVG `feTurbulence` noise at about 12 % opacity, overlay blend, jittered every frame.
- **Vignette**: plus a tiny per-frame brightness flicker (1–4 %).
- **Backdrop**: a radial gradient "studio" with a few slow bokeh discs or dust specks in the accent color, used sparingly.

**HUD** (film-set feel, small mono text in the corners): a red rec dot + `SC.03` · `FR 412` · `12 FPS · ON ONES` · timecode. Dim it in the closing.

**Captions**: at the top of each scene, an **eyebrow** (mono, uppercase, letter-spaced, accent, about 9.5 px at 360 width) typed at about 24 cps, then a **display line** of 2–4 words (bold, about 28 px, hard 2–3 px shadow, at y≈80) typed at about 20 cps. Keep text out of the platform UI zones (top about 50 px, bottom about 240 px, right-edge buttons). Burned-in captions are short statements, not a transcript; the creator's voice carries the explanation.

### Motion vocabulary

- **Stepped time**: every pose is computed from `t = frame / 12`, so movement happens "on ones" at 12 fps. To drive Framer Motion transitions, use an easing quantized to 12 fps (`stepped(n, fn)`).
- **Entrances**: spring scale (`popIn`), a drop with bounces and squash (`dropPose`), a slide with an overshoot, or typing. Use plain fades only for whole-screen exits. Mechanical parts and sensors arrive with a spring scale rather than a bare pop.
- **Focus and turntable**: items on a platform rotate in 60° steps. The front item scales up and gets its name; items at the back blur and darken.
- **Flows**: packets or envelopes travel along a path between stations (device → broker → database), with small labels for each hop (PUBLISHES / LISTENS / STORES). A ripple and a tick sound play on arrival.
- **Stamps and confirmations**: a stamp slams with squash and a shake of 2–4 px; small confetti bursts for success; a red flash and a shake for an attack or error.
- **Characters**: simple and built from a few parts, with a walk cycle (bob plus sway), a few poses, and a name tag. **A name tag belongs to its character.** It is tethered by a thin line to the head, sways with the walk and settles when the character stops. It appears together with the character, never earlier or detached. Its text types in letter by letter with a caret, and a ripple plays when it completes.
- **Freeze under cards**: while a title card covers the screen, the outgoing and incoming scenes hold their last and first frames, through `sceneTime` clamping.
- **Solid things stay solid**: keep the boil to about 1 px, and remove it from objects that should feel locked or heavy (a closed padlock, a logo at rest). A hero object that trembles reads as a bug.
- **The ghost pointer clicks for real**: the hand lands exactly on the control, and the state changes on the frame of the click, not before and not after.

---

## Step 4 — Title cards (the signature element)

Every chapter opens with a cardboard board that enters, holds and leaves while the AI voice reads "Title. Subtitle." Entrance and exit take about 0.28 s each.

**The card shows**:
- an animated **emblem** (about 200×118) that is a mini-diagram of the chapter
- the chapter counter `02 / 08` in mono accent
- the **title** (about 30 px, extra-bold, hard shadow) revealed with an animation specific to that chapter
- the subtitle
- progress dots, with the current one stretched

**Each chapter gets its own transition**, designed around its concept. Examples from the series:
- *Methods / options*: the board swings in from the right at -9°, and the title letters fly in on a spiral.
- *A second layer (MFA)*: the board rises from below as a second layer, and the title is revealed by a glowing scan line.
- *A three-part structure (JWT)*: three vertical strips drop in (header · payload · signature), and the title letters scramble through base64 characters before settling.
- *Time-based (sessions)*: a conic clock-sweep mask with a glowing hand, and letters flip down on the X axis.
- *Rows (RLS)*: six bands slide in from alternating sides, and the title grows inside a pill with a check mark.
- *Defense*: the board slams down from the top with a hazard-stripe edge, a bounce and a shake, and the letters drop in from 2.6× scale with a squash.
- *Capture / record*: the board rotates in like a tilted slate.
- *Closing*: an iris opens from the center with a glowing ring.

For a new topic, invent transitions in the same spirit: a strip for each part of a structure, a sweep for anything about time, a slam for anything about protection. Pair each one with its own SFX "look", described in Step 6.

---

## Step 5 — Interactive web version

The same component powers the web page. Outside render mode it renders:

- **A phone frame** with a deck: play/pause, ±1 frame, previous/next chapter, restart, sound toggle, and a scrubber split into chapter segments.
- **Hotspots** (`hotspotsAt(t)`): invisible tappable boxes over the pieces of the current scene, with none under title cards. Tapping one pauses the video and opens an **info sheet** that explains the piece in 2–3 lines, with a "Continue" button. Give each hotspot an `aria-label` such as "Explorar: Programa de captura".
- **A ghost pointer**: a hand cursor that "taps" items during guided demos and is part of the video too.
- **An explore panel** that changes with the chapter, defined in an `EXPLORE` map. Kinds: a `hint`, `options` (radio buttons such as Accelerometer / Gyroscope, or Walk / Simulate fall, which jump to the matching moment), or an `action` (e.g. "Send an MQTT message"). Number keys select the options.
- **Keyboard**: Space plays or pauses, ←/→ steps one frame, Shift+←/→ jumps a chapter, R restarts, M toggles sound, Esc closes the sheet.
- **Reduced motion**: turn the boil off with `m = 0`.

For publishing, bundle with esbuild into an IIFE whose externals map to globals: React, ReactDOM, `Motion` and `LucideReact`, loaded from cdnjs or jsDelivr with pinned versions. Compile Tailwind for only the classes the file uses, inline the CSS, and embed the audio as an MP3 data URI. Give the page a short title and a description.

---

## Step 6 — Music, SFX and mix

Generate everything with deterministic Python (numpy + scipy, fixed RNG seed), output as 48 kHz stereo.

- **Music**: 96–100 BPM, light and curious. A warm detuned pad, a wooden marimba melody, kick, shaker and a soft bass over a simple loop (e.g. Dm–Bb–F–C). **Drop the drums under each title card** so the voice sits in a clearing; a short break works well at a dramatic moment such as the fall.
- **SFX from the timeline**: a pop for each entrance, a thud for drops, a whoosh for packets, ticks for typing, a stamp, a chime for success, a buzz for errors. Each card style gets its own transition sound (swing, scan, slam, sweep, iris and so on). Read the event times from the same constants the component uses, so picture and sound can't drift apart.
- **Levels**: music at about -23 dB RMS and SFX at about -25 dB RMS, with a light reverb. The card voice is normalized to about -19 dB RMS, placed 0.30 s after the card starts, with 20 ms fades. Duck the music by about 7 dB from 0.15 s before the voice to 0.35 s after, with a 0.12 s smoothed envelope. Use a soft `tanh` limiter with the peak at or below -1 dBFS, a 0.6 s fade-out at the end, and a high-pass at 35 Hz on the music.
- **Leave space for the creator's narration**, recorded later, so the music stays low throughout.
- Export a WAV for editing and an MP3 for the web page.

You can't listen to the result. Check RMS, peaks and the timestamps where the voice starts versus where the card lands, and tell the user plainly that the audio was checked by numbers, not by ear.

---

## Step 7 — Check, render, encode

**Check before the full render.** The agent can't see the video playing, so it has to look at frames.
1. Take screenshots of a dozen key moments with Playwright at 1080×1920 (`?render=1`, `__smSeek(round(t*12))`, then wait two requestAnimationFrames) and tile them into a contact sheet, 6 per row at 360×640. Look at them before rendering everything.
2. Checklist:
   - Labels overlap anything?
   - Anything hidden behind a character or another object?
   - Text inside the safe zones and legible at phone size?
   - Typed text shows only part of its letters at the start (not the full word on frame one)?
   - Each name tag stays with its owner?
   - A removed element is gone from the scene, its hotspots, its info sheets, the panel, the captions and the script?
   - The closing shows only the brand and slogan?
   - The voice starts after the card lands and ends before it leaves?
   - No console errors?
3. Run a UI test at 390×844: no horizontal overflow, every button and option works, the info sheets open and close, and the scrubber moves.

**Render**: Playwright with 4 parallel pages, one frame at a time with `__smSeek(f)`, two requestAnimationFrames, then a JPEG screenshot at quality 94 (`f_0000.jpg`). A 2D cut-out scene needs no GPU and renders comfortably in a cloud container.

**Encode**:
```bash
ffmpeg -y -framerate 12 -i frames/f_%04d.jpg -i audio.wav \
  -vf "fps=24,format=yuv420p" -c:v libx264 -crf 18 -preset slow \
  -c:a aac -b:a 192k -ar 48000 -shortest -movflags +faststart topic_9x16.mp4
ffprobe -v error -show_entries format=duration:stream=width,height,r_frame_rate topic_9x16.mp4
```
Confirm the duration equals `TOTAL / 12`, the resolution is 1080×1920 and the frame rate is constant.

---

## Step 8 — Deliver and iterate

**On delivery**, write a few lines:
- what the video is (duration, chapters)
- the files
- the interactive page
- what was verified and what wasn't (e.g. "audio checked by numbers, not by ear")

**On each round of feedback**:
- Apply every requested change everywhere it lives: the scene, captions, hotspots, info sheets, the explore panel, SFX timing, the script, and the brief if it changed a standing decision.
- Rebuild the whole package: page republished at the same URL, MP4, WAV, JSX and script.
- **Try to keep scene lengths stable.** If the creator has already recorded narration, changing a window breaks it. If a length must change, say which windows moved.
- When the user corrects a fact ("the Raspberry Pi is the broker; it listens and stores in Supabase"), redraw the flow to match exactly. Don't just relabel it.
- Report the changes as a short list grouped by area, plus any narration lines that changed.
- Keep a backup of the previous version of each source part before large edits.

---

## Social copy and messages (on request)

Write in the video's language and match the platform:
- **Instagram**: a hook question with an emoji, 2–3 short paragraphs that tell the flow, one honest clarification, the slogan, then 6–9 hashtags.
- **LinkedIn**: a question hook, one framing sentence, the flow as a numbered list, then "a point people often confuse: …", an honest disclaimer where relevant ("an educational example, not a medical device"), a closing question to the reader and 5–6 hashtags.
- **TikTok**: an on-screen hook for the first 2 seconds, a 2–3 line caption with the flow as arrows (A → B → C), and hashtags.
- **WhatsApp / community post**: a friendly opener, the creator's motivational line (e.g. "Todo lo que te imagines lo puedes crear"), the origin of the project ("un proyecto de la U"), then the links on their own lines with emoji labels.

Leave out series numbering and internal jargon unless asked. Include the project's origin when the user mentions it. Never overclaim results.

---

## 3D variant (when the brief asks for it)

Keep the same pipeline: script → voice → deterministic `seek(t)` → frames → ffmpeg.
- **Scene**: Three.js with an orthographic isometric camera for machines and a perspective camera for character moments, plus ink outlines (an inverted hull), flat shadows and paper grain.
- **Characters**: build them from a few primitives with hand-made joints, and drive the mouth from audio amplitude. Animated organic humans are out of reach with code alone.
- **Lessons from a 3D pigeon explainer**: check that no object sits in front of the subject (an easel leg, a hidden mini-model), that boxes in nested diagrams are centered, and that drop irrelevant data cards. When an effect is removed, remove it from every scene, not just the first.
- **Render time**: software WebGL is slow without a GPU, so render locally if the user has one.
