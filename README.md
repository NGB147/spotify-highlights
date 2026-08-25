# Spotify Highlights — working prototype

Prototype of the AI feature proposed on slide 10 of the Group 3 Digital Product Management deck:
**AI podcast chapters and smart recaps.**

Single static page, no build step, no dependencies, no API keys. Works offline once loaded
(the only network call is the Google Fonts stylesheet).

---

## What it demonstrates

| Slide 10 pillar | In the prototype |
|---|---|
| Auto-chapter detection | "Generate Highlights" runs a staged pipeline, then the flat grey waveform becomes a colour-segmented, chaptered timeline. Every chapter is clickable and seeks the player. |
| Personalised audio recap | Three listener profiles rewrite the same episode's recap. "Play recap" speaks it aloud using the browser's speech engine. |
| Smart skip learning | Detected intros and ad reads with per-segment toggles. With auto-skip on, playback jumps past them and the minutes-skipped counter climbs live. |
| Smarter follow-on picks | Recommendations at segment level, with the reason each one surfaced. |

The **"Spotify today" / "With Highlights"** toggle at the top is the comparison slide — same
episode, no chapters, publisher blurb only. Use it to open and close the demo.

Three fictional episodes are included so the demo does not look like a one-episode trick.
All shows, episodes and listening data are invented; nothing is scraped from real podcasts.

---

## Deploying

### Option A — Netlify Drop (fastest, ~30 seconds)
1. Go to https://app.netlify.com/drop
2. Drag the **whole folder** onto the page.
3. Rename the site under **Site configuration → Change site name** (e.g. `spotify-highlights-g3`).

### Option B — GitHub + Netlify (better for the professor, shows version history)
```bash
cd spotify-highlights
git init
git add .
git commit -m "Spotify Highlights prototype — DPM Group 3"
git branch -M main
git remote add origin https://github.com/<your-username>/spotify-highlights.git
git push -u origin main
```
Then in Netlify: **Add new site → Import an existing project → GitHub → pick the repo.**
Leave the build command empty and set the publish directory to `.` (a `netlify.toml` in this
folder already does that for you). Every push redeploys automatically.

---

## Running the demo in class (about 3 minutes)

1. Open on **"Spotify today"**. Point at the 107-minute episode with a two-line description.
   *"This is the problem. You cannot tell if any of this is worth an hour."*
2. Switch to **"With Highlights"** → click **Generate Highlights**. Let the pipeline run;
   it names the three real steps (transcription, boundary detection, summarisation).
3. Click a chapter — the player jumps. Point out that ad reads are marked in amber, not hidden.
4. Open **Recap**, switch the listener profile, and show the recap rewrite itself. Hit
   **Play recap** — turn the volume up, it speaks.
5. Open **Smart skip**, press **Play**, and let it run a few seconds — the auto-skip toast
   fires and the minutes-skipped counter moves. Playback is at 60× so this is quick.
6. Scroll to the metrics panel to close on what the feature is meant to move.

Keyboard: **Space** plays/pauses, arrow keys scrub the timeline when it has focus.
**Reset** clears everything for the next run — press it before the professor tries it.

If the venue has no audio, skip step 4's playback; the written recap makes the same point.

---

## Honest notes, in case you are asked

- The AI output is **pre-computed, not generated live.** Chapters, summaries and recaps were
  written to be realistic, and the pipeline animation is a simulation of latency. This is a
  deliberate prototyping choice: it demos the same interaction without a live API key, a
  network dependency, or a model failing in front of an audience. Say this if asked — it is a
  stronger answer than pretending otherwise.
- Metrics in the bottom panel are **illustrative pilot targets**, not Spotify's reported figures.
- The recap voice is your browser's built-in speech synthesis. Production would use a
  synthesised host voice.

Not affiliated with or endorsed by Spotify. Built for classroom use only.
