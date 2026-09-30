---
name: drama-song-ad
description: Make a complete drama song ad, from nothing to the finished video. A seven-to-ten-minute long-form ad (a VSL) sung in the first person, told as a drama - the hero falls, then rises. One skill does everything - intake, three story arcs, a twelve-stage outline, the sung script, the song (Suno V5.5), a word timing map, the shot plan, character sheets, shot sheets, video clips (Seedance 2.0) and the final edit. Always 9:16, always 1080p, 3D animated feature look by default. Every generation is described first and runs only after the user approves it. Use when the user says "drama song ad", "song ad", "song VSL", "singing VSL", "mini-drama song ad", or brings a product (usually a supplement) and wants a long story ad sung as a song and turned into a video. Works with the MaxFusion AI MCP, any other generation tools the user has, or by hand with the user running the tools themselves. Uses local faster-whisper and ffmpeg for timing and the edit.
---

# Drama Song Ad

A drama song ad is a sales letter sung as a song. One narrator tells the story of their own fall and rise in the first person. The product shows up only when a close, trusted mentor brings it, about halfway through. The pitch is only the last sixty to ninety seconds. Every shot shows the exact line being sung.

This skill takes the user from nothing to the finished video.

---

## Rules

1. **Say it, then wait for a yes.** Before every generation (song, character sheet, shot sheet, clip), show what will be made and the full prompt, then wait for the user to approve. An instruction like "and then generate it" does not replace this. On a re-run, show only what changed.
2. **Never re-generate on your own.** If a result has a problem, report it, suggest a fix, and wait.
3. **Choices are made with cards.** Use `AskUserQuestion`: two to four options, each with a one-line description, the recommended option first and marked "(Recommended)". The user can always pick "Other".
4. **Fixed format.** Always 9:16. Always 1080p. No format or resolution questions.
5. **Default look: 3D animated feature film.** Use it unless the user asks for another look. Describe the look in words; never name a studio.
6. **Generate only with the tools chosen in Stage 00.** On MaxFusion: music `maxfusion_create_music` (Suno V5.5), images `maxfusion_generate_image` (`gpt-image-2`), video `maxfusion_generate_video` (`seedance-2.0`, never 2.5), uploads `maxfusion_upload_asset`. On other tools: the closest match the user has for each job. In manual mode: hand the user each prompt and guide them through running it. Local tools where needed: faster-whisper for word times, ffmpeg for cutting.
7. **On MaxFusion, one new project per ad**, named `Drama Song Ad – <Product>`. Every generation goes into it. On other tools, keep every result for this ad together the way that tool allows.
8. **Never change clip speed.** No speed-up, no slow-down, no stretching. Clips are only cut.
9. **No captions, end cards, badges or buttons unless the user picks them** in the shot plan (Stage 6). Not every ad has an offer or needs graphics.
10. **Soft claims only.** "Supports healthy…", never "cures", "kills" or "fixes". No disease claims.
11. **No cost estimates.**
12. **Plain words.** Write every script line, prompt and message in simple, everyday language.
13. **No line opens with "Okay".** If you have a humanizer skill, run it over the script before the script gate.
14. **Files, not chat.** Scripts and plans are saved in the run folder. Give the user the link and a short note of what changed. Do not paste a full script in chat unless asked.

**Run folder:** `drama-song-ad-<product>/` (in the working directory) holds `brief.md`, `arc.md`, `outline.md`, `script-v<n>.md`, `song/`, `lyric-timing-map.md`, `shot-plan.md`, `asset-ids.md`, `refs/`, `clips/`, `edit/`.

---

## Stage 00 — Check the tools

Do this before anything else.

1. **Look for the MaxFusion AI MCP** (tools named `maxfusion_*`). If it's there, use it for every generation and go to "Where to start".
2. **If it isn't there, say:**
   "I see that you don't have a MaxFusion account. Do you want me to connect any other MCP so I can help you generate the images, the videos, the song, and so on?"
3. **If they want to connect an MCP:** help them connect it, then use it.
4. **If they say no, say:**
   "If you don't connect, you'll need to take my output and put it into tools like Suno and others yourself to create the materials. Is that something you want to do, or do you want to connect?"
5. **Then follow what the user chooses:**
   - **They have API keys and want specific tools:** use those tools, the way the user asks.
   - **They have other tools available:** use whatever tools they have.
   - **They have no tools:** manual mode. Give them each output ready to paste (the song prompt, every image and video prompt, the files to attach and in what order), tell them which tool to paste it into, and guide them step by step. Ask them to send back each result (song, images, clips) so the next stage can use it.

Every rule and gate in this skill stays the same in every mode. In manual mode, "approve before generating" means the user approves the prompt before they run it.

---

## Where to start

First card: **"What do you already have?"**

| Option | One-liner | Start at |
|---|---|---|
| Nothing yet (Recommended) | We build the story, the script and the song together. | Stage 0 |
| A finished script | We check it against these rules, then make the song. | Stage 3 check, then Stage 4 |
| A finished song | Upload it; we time it and go to the visuals. | Stage 5 |
| A song and a shot plan | We time the song and review your plan. | Stage 5, then Stage 6 |

A script or plan the user brings is still checked against this skill. Point out problems once, then follow the user's decision. A character image the user brings replaces that character's sheet.

---

## Stage 0 — Intake

Ask in one plain message:

- **Product:** name, format (softgels, capsules, powder), how many a day.
- **What it does:** the one-line promise, the ingredients, and how it works in plain words.
- **Sub-avatar:** gender, age, race or cultural world, relationship status, the main physical problem, and the private fear behind it.
- **Offer (if there is one):** discount, guarantee, scarcity line, call to action.
- **Off-limits:** claims legal won't allow, topics to avoid.
- **Brand assets:** product photos, logos, packaging.

If the user has no sub-avatar, suggest three with a card (one line each: who, age, problem, fear).

Then one card for **music genre** (options from the genre list in Stage 4; recommend a genre where the words are easy to hear).

The narrator's voice matches the sub-avatar (a woman's story is sung by a woman). The look is the 3D animated default unless the user asks for another.

Save everything to `brief.md`.

---

## Stage 1 — Three story arcs

The sub-avatar decides everything; no arc is pitched before it is set.

Pitch three different arcs. Each arc is a short block:

| Field | What to write |
|---|---|
| Type | Revenge, reconciliation, or another shape that fits |
| Opening line | The first sung sentence: a humiliation, specific and shocking |
| The partner | Who they are and what they say or do |
| The betrayer | The closest person possible (best friend, sibling, godparent). A reconciliation arc may have none; the enemy is shame |
| The deeper wound | What makes it worse right after the opening |
| Failed fixes | What the hero tried, including friends' advice and a dismissive doctor |
| The mentor | Close (family or near-family), with a visible, credible title (therapist, doctor, clinic owner) and their own proof |
| The truth | The "It's not X, it's Y" line that breaks what the hero believed |
| Dream picture | What the hero wanted from the start, and how the win gives it to them in the same place, in front of the same people |
| Key word | One word tied to how the product works, repeated until it carries a second meaning |

Ask with a card which arc to develop (plus "Mix elements"). Refine it until the user approves. Save to `arc.md`.

⛔ **Gate:** the user approves the arc.

---

## Stage 2 — Twelve-stage outline

Map the arc onto the twelve stages, one or two lines each, with its share of the runtime.

| # | Stage | Runtime | What must happen |
|---|---|---|---|
| 1 | Ordinary world | first few seconds | A glimpse of what is about to be lost |
| 2 | Humiliation (the opening) | 0–5% | The first line shows stakes that are already bad |
| 3 | The wound gets worse | 5–15% | Bad turns worse right away; overheard words or "they all knew" |
| 4 | Frozen | 15–20% | The hero doesn't fight back; they act normal |
| 5 | Seeing it too | 20–25% | The hero looks at their body and agrees with the insult |
| 6 | Failed fixes | 25–35% | Gym, diets, pills, friends' advice, the dismissive doctor. Rock bottom |
| 7 | The mentor | 35–42% | Close, credible, the complete version of the hero |
| 8 | The gift | 42–50% | The truth first, then the product as a physical object |
| 9 | Doubt | about 50% | The hero doesn't believe it, slowly trusts the mentor, often keeps it secret |
| 10 | The climb | 50–70% | Week one to week six, small concrete changes that others notice, each one answering the insult |
| 11 | The win | 70–85% | Same place, same witnesses; the hero gets the dream picture |
| 12 | Coming home | last 10–15% | Direct address ("If you're…"), how it works in one or two lines, the offer if there is one, and a last line that calls back to the opening |

Save to `outline.md`.

⛔ **Gate:** the user approves the outline.

---

## Stage 3 — The script

**Length:** seven to ten minutes sung is about 1,100 to 1,500 words. Aim for about 1,200. Words are sung at about 2.2 per second at mid-tempo (about 1.8 for slow genres, 2.5 for fast pop).

**Format:** section headers in brackets, for example `[Intro, spoken over soft keys]`, `[Verse 1]`, `[Chorus 1]`, `[Bridge]`, `[Outro, spoken over the music]`. Sections follow the story, not pop song form.

**Voice**
- First person, past tense, one narrator who matches the sub-avatar.
- Other characters speak only as quoted lines inside the narration.
- Everyday speech that fits the sub-avatar's world ("ain't", "didn't say nothing") where it's natural.

**Lines**
- Short. One idea per line, most lines under eight words. Each line reads like a caption.
- **No rhymes.** Lines don't rhyme on purpose; rhymes sound catchy and silly.
- Literal and plain. No metaphors, figures of speech or wordplay, with two exceptions only: the key word that carries a second meaning, and plumbing words for how the product works (blocked, backed up, drain, flush, pools).
- Specific numbers and details: ages, years married, times, days, pounds, week numbers.
- Physical objects carry the feeling (a ring, a photo, a phone on the nightstand, a dress that won't zip) and come back later.
- Every painful point is said by someone else as a quote.
- Clear turning lines between sections ("Here's what nobody tells you").
- Counting numbers are spelled out as words. Brand names and web addresses are written the way they should be sung ("brand dot com").

**Chorus**
- Optional. A reconciliation arc works well with a short repeated chorus that states the wound, sung two or three times, then turned around at the win. A revenge arc can go without a chorus and let the key word do that job.

**How it works (the mechanism)**
- Plumbing words: blocked, backed up, drain, flush, pools.
- One enemy behind many symptoms.
- Explain why the failed fixes failed ("you can't burn waste").
- Keep it short; the pain is emotional first.

**The pitch (last sixty to ninety seconds)**
- Direct address with repetition ("If you're… if your… if your doctor says…").
- The product name, what it supports, how many a day.
- If there is an offer: the discount, the guarantee turned around ("Thirty-day money-back guarantee. But six weeks in, you won't be sending it back."), scarcity, "Link below."
- The last line calls back to the opening line.

**Self-check before showing the script:**

- [ ] The opening line is a humiliation, in the first sentence
- [ ] The wound gets worse before anything gets better
- [ ] The hero freezes; no angry outburst
- [ ] The failed fixes include friends' advice and a dismissive authority
- [ ] The mentor is close, has a visible credible title, and their own proof
- [ ] The truth comes before the product
- [ ] The product isn't named before the mentor, or before about halfway
- [ ] The hero doubts it
- [ ] The climb goes week by week, others notice, and it answers the insult
- [ ] The win happens in the same place, with the same witnesses, and gives the dream picture
- [ ] The pitch is sixty to ninety seconds and ends on a callback to the opening
- [ ] No rhymes; no metaphors beyond the two exceptions
- [ ] Claims are soft
- [ ] No line opens with "Okay"; the humanizer pass is done (if available)

Save to `script-v<n>.md`.

⛔ **Gate:** the user approves the script.

---

## Stage 4 — The song

On MaxFusion: `maxfusion_create_music`, Suno V5.5, **Auto duration**, `project_group_id` = the run project. One call gives two takes. On other tools or by hand: Suno (or the music tool the user has), same prompt, auto length.

**Make it in two halves.** A seven-to-ten-minute song doesn't come out of one call. Split the script at a section break near the middle, make each half with the same style prompt, then join them in the edit with a short crossfade on an instrumental gap. The second half's prompt says it continues the same song (same voice, key, tempo).

**Genres** (the Stage 0 card uses these):

| Group | Genres (tempo) | Notes |
|---|---|---|
| Words easy to hear — best | Soul / R&B ballad (70–100) · Upbeat R&B (100–120) · Country / country-pop (90–120) · Gospel-soul (70–100) · Acoustic / singer-songwriter (80–110) · Musical theatre (varies) | Clear words, room for a long story |
| Words get buried — avoid | Dance-pop · House · EDM · K-pop · Reggaeton | Busy music stretches and hides words |

**Prompt template** (the vocal-start line goes first):

```
The song opens with the vocal. The very first sound at 0:00 is her voice singing the first word. Zero seconds of instrumental before the vocal. Style: <genre, feel, key instruments, mood>, <BPM> BPM. <Voice: gender, age feel, tone, delivery>, crisp enunciation, every single word understood, no vocal runs that stretch or blur words. Sung in English. Sing every line exactly once, in order, top to bottom. Do not add ad-libs, backing chants or extra words. Short instrumental ending after the last line.

Use these exact lyrics:

[Verse 1 - vocal starts at 0:00, no intro]
<lines>
[Chorus 1]
<lines>
...
```

- If the script has a chorus, keep the `[Chorus]` sections exactly as written; the "exactly once" line then means each written line, in order, including the written chorus repeats.
- Spoken intro or outro sections are marked in their headers ("spoken over soft keys").
- **Known problems:** an instrumental intro (fix: vocal-start line first); rushed or blurred words (fix: slower tempo, shorter lines); repeated or invented lines (fix: the "exactly once" rule); drifting into another language (fix: "Sung in English").

⛔ **Gate:** the user listens and picks one take for each half. Record the audio ids in `asset-ids.md`.

---

## Stage 5 — Timing map

Every shot is placed on the exact seconds its line is sung.

1. Download the chosen takes to `song/` and join the halves with ffmpeg (short crossfade on an instrumental gap) into `song/song.mp3`.
2. Get word times with local faster-whisper:
   ```python
   from faster_whisper import WhisperModel
   m = WhisperModel("medium.en", device="cpu", compute_type="int8")
   segs, _ = m.transcribe("song.mp3", word_timestamps=True, language="en")
   ```
3. **Times from Whisper, words from the approved script** (Whisper mishears names).
4. Write `lyric-timing-map.md`: one row per line with start, end, lyric and outline stage. Mark instrumental gaps.
5. Check: the vocal starts at 0:00, every line is sung once in order, nothing is added. If not, go back to Stage 4.

---

## Stage 6 — Shot plan

One shot sheet per time slot. Each sheet is one image with four panels and becomes one video clip. Seedance 2.0 clips run 4 to 15 seconds, so **every slot is 15 seconds or less**. A seven-minute song needs about 35 to 40 sheets.

Table in `shot-plan.md`: sheet, slot (start–end), lyrics, what each of the four panels shows (each panel with its own time and line), characters.

**Rules**
- **Lyric lock:** every panel is tied to the line sung during its seconds and shows what that line says. A panel that doesn't match its line is fixed before anything is made.
- **Story locks:** write down the continuity rules the story needs, and repeat them in every prompt they affect. Examples: who is on which side of the bed and where the camera is; an object that must stay the same (the same cake, the same ring on the same finger); something that must not happen before a certain point (he never photographs her until the graduation).
- **No lip sync.** Characters act the story; they don't sing to the camera.
- **Show the literal line.** Grounded, specific actions, objects, places and faces.
- **Screens face the character, never the viewer.** Show screen content only in an over-the-shoulder shot or a close-up of the hand and phone filling the frame, and cut between the character's face and that close-up.
- **Normal objects used the normal way.** A bill is an email or bank notice, a deadline is a calendar or clock. No magic objects or floating symbols, except simple glowing flow lines inside the body when the mentor explains how the product works.
- **Variety:** no location twice in a row (callbacks excepted), no camera angle twice in a row, a physical action in every panel.
- **Brands appear inside the world** (packaging, the bottle on a counter, an app screen).
- **Callback sections** (an outro that repeats earlier moments) can be cut from approved clips instead of new sheets.

**Captions and end cards:** at this gate, ask one card: **"Add captions, end cards or offer graphics?"** Options: "None (Recommended)", "Captions", "Offer graphics (badge, button)", "Both". Only if the user picks them are they planned (and the panels leave space for them). Otherwise the ad has none.

⛔ **Gate:** the user approves the shot plan.

---

## Stage 7 — Character sheets and brand refs

**Who needs a sheet:** the hero **before** and **after** the change (two sheets, same person), a younger hero if there are flashbacks, the mentor, the partner, the betrayer, and anyone who appears more than once. A user's own character image replaces that sheet.

**Look description** (reused word for word in every image and clip prompt):
"3D animated feature film, stylized CGI in the look of a modern big-studio animated movie: soft subsurface skin, big expressive eyes, appealing rounded shapes, cinematic lighting, highly polished render."
(If the user asked for another look, write its description here once and reuse it.)

**Character sheet prompt** (`gpt-image-2`, 16:9):

```
<Look description> character sheet. One character shown four times on a clean light-gray background: close-up face portrait, full body front view, full body three-quarter view facing left, full body three-quarter view facing right. Neutral expression.
Character: <age, look, skin, hair, eyes, body, distinguishing details, outfit>. Same exact character in all four views, consistent face, hair, outfit and proportions. No text, no logos.
```

For the "after" sheet, attach the approved "before" sheet and say: "the same person as the attached sheet, same face; only <what changed: less swelling, slimmer face, the ring fits> is different."

**Brand refs:** upload product photos, logos and packaging (on MaxFusion with `maxfusion_upload_asset`; otherwise the way the user's tool takes reference images). Look at each file first. Put white or transparent logos on a dark solid background before upload.

⛔ **Gate:** the user approves each sheet. Approved ids go in `asset-ids.md` and are reused in every later prompt.

---

## Stage 8 — Shot sheets

Make **one sheet first as a test**, get approval, then the rest.

**Prompt** (`gpt-image-2`, 9:16):

```
Storyboard sheet, 9:16 image split into a 2x2 grid of four equal panels with thin white gutters, read left-to-right, top-to-bottom. Every panel is a frame from the same scene: <look description>. <Character> is exactly the character from the attached character sheet (<key traits>). [Other characters, same words every time.] Realistic proportions: normal-sized hands, phones and cups. Correct anatomy in every panel: exactly two arms and two legs per person, no extra or missing limbs. Any logo or product is copied exactly from its attached reference image.
Setting: <one place, one light>.
[Story locks that apply to this sheet.]
Panel 1 (top-left), <camera position and angle>: <one clear action> ("<lyric line>").
Panel 2 (top-right), ...
Panel 3 (bottom-left), ...
Panel 4 (bottom-right), ...
```

- Every panel says where the camera is (behind, over-the-shoulder, close-up of hand and phone, front at eye level, top-down, low) and one action.
- Screen content only in over-the-shoulder or hand-and-phone panels; otherwise "the screen is never visible".
- Avoid poses that break limbs (legs over armrests, crossed arms over bodies); prefer simple standing or seated poses.
- References: the character sheets for whoever is in the sheet, plus only the brand refs that sheet needs.

⛔ **Gate:** the user reviews each sheet (or a batch).

---

## Stage 9 — Clips

On MaxFusion: `maxfusion_generate_video`, `seedance-2.0`, `resolution: 1080p`, `aspect_ratio: 9_16`, `ref_image_mode: ingredients`, `project_group_id` = the run project. References: `[shot sheet, character sheet(s), brand refs]`. On other tools or by hand: a video model that takes a storyboard image plus character images as references (Seedance 2.0 if available), 9:16, 1080p.

- **Duration** = the slot rounded **up** to a whole second. The edit cuts it to the exact slot.
- Make one or two test clips first, then the rest in batches.
- **Silent.** The song goes on in the edit.

**Prompt:**

```
9:16 <look description> scene. @image1 is a storyboard to follow, not footage. It never appears in the video. Play its four panels in order as full-frame shots, cutting between them like a film edit where the camera angle changes. Never show the grid, gutters, or multiple panels; every frame is a single full-screen image. @image2 is the character sheet: <character> must match it exactly. [Story locks.] Correct anatomy, normal proportions; screens are only shown where the panel shows them. Audio: silent, no music, no voices.
0.0-X.Xs: panel 1, <action>.
X.X-Y.Ys: panel 2, <action>.
...
The final video never shows @image1 or any reference image, storyboard, grid, white gutter or panel layout. Every frame from the first to the last is newly rendered, full-screen footage.
```

- The sheet-never-on-screen line is always said twice: at the start and at the end.
- Panel times inside the clip follow the lyric times (seconds from the start of the slot).
- Describe screens and effects literally ("the phone screen shows the same photo"), never with technical jargon.
- Brand refs are named in the text: "(the bottle exactly as @image3)".

⛔ **Gate:** the user reviews the clips; only the clips they name are redone.

---

## Stage 10 — Edit

Frame-accurate cut to the song with local ffmpeg.

- Download every clip to `clips/clipNN.mp4`.
- Cut points = `round(time × fps)` on the lyric times. Per clip: `trim=start_frame=S:end_frame=S+N,setpts=PTS-STARTPTS,fps=<fps>,scale=1080:1920,setsar=1`, then `concat`.
- The song is the only audio. Output length = song length. libx264 crf 18, aac 192k, `+faststart`.
- Add captions or graphics only if the user picked them in Stage 6.
- Save `edit/<product>-drama-song-ad-v<n>.mp4`, a new version number for every change, and send it to the user.

**Check every clip before sending:**
1. **Storyboard showing** — clips can open on the 2x2 sheet for up to about 1.5 s. Step through the first 40 frames and start after the last grid frame.
2. **Frozen start** — the first half second barely moves. Check frame differences and skip those frames.
3. **Fill cut time from neighbouring clips** — the clip before plays a little longer or the next one starts a little earlier. The song and total length never change. Never slow a clip down or add frames.
4. If a gap can't be filled at normal speed, tell the user and ask.

⛔ **Gate:** the user reviews the final video.

---

## Common problems and the rule that prevents them

| Problem | Prevention |
|---|---|
| Script sounds like a poem or jingle | No rhymes; literal lines; the two metaphor exceptions only |
| Product shows up too early | Not before the mentor, not before about halfway |
| Pitch takes over the story | Pitch is only the last sixty to ninety seconds |
| Song starts with an instrumental | Vocal-start line first in the prompt |
| Words rushed or blurred | Clear-words genre, slower tempo, shorter lines |
| Song too long for one call | Two halves, joined in the edit |
| Shots don't match the words | Timing map and lyric lock on every panel |
| Story details change between shots | Story locks repeated in every prompt they affect |
| Hero looks different before and after | Separate before and after sheets of the same person |
| Lip sync looks wrong | No lip sync |
| Monitors facing the viewer, backwards phones | Over-the-shoulder or hand-and-phone shots only |
| Giant hands, extra limbs | Proportion and anatomy lines; simple poses |
| Storyboard or frozen frames in clips | Stage 10 checks, filled from neighbouring clips |
| Captions or cards nobody asked for | Only if picked in Stage 6 |
