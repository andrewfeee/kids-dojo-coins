# Dojo Coins v4 – kids' jobs board for the Samsung TV

A single file (`index.html`, about 140 KB). Everything is inside it: the app, the art, the sounds and the default photos. It works offline (only the optional setup code needs the internet), needs no build step, and saves to the browser's localStorage.

## What it does
- **One main screen, no clicking through.** Days run across, kids run down (Charlie blue, Pip pink, Jack yellow), and every day cell is split into ☀️ Morning and 🌙 Afternoon. Each half shows that kid's bookings (emoji, title and time, e.g. 🎾 Tennis 8:30–9:30am) and the job with its tick. Whole-family bookings appear once, in a 👪 Family band along the top. Today's column is outlined in gold.
- **Mon–Fri and Sat–Sun pages** keep the text big enough to read from the couch. The page holding today opens first. Press ▶ on the remote past Friday to reach the weekend, or ◀ past Saturday to go back, or use the Mon–Fri / Sat–Sun buttons. Prefer everything on one screen? Settings → Main screen → All 7 days (smaller text).
- Tick a job (OK/Enter on the remote, or tap) to earn 1 coin. That plays the celebration: the kid's face on a little runner jumps, hits a ? block, a coin pops out, flies over and lands on their pile, then confetti and a "Super star, Charlie!" banner. Press OK or Back to skip it.
- **🏆 Rewards** is a separate display with each kid's photo, coins this week, their growing coin pile, the all-time total and **+1 Bonus**. Open `…/#rewards` on a second screen or tab and it follows ticks made on the main screen (same browser), playing the coin animation as they land.
- **Undo** reverses the last coin. Choosing a job that's already ticked asks whether to untick it.
- **The week view always opens first.** **Month** is a secondary button: the month view is a Mon–Sun grid with today highlighted. Each day shows a dot for each kid with ☀/☾ ticks for the morning and afternoon jobs plus the coins earned that day, and a 📅 mark if that day has bookings. Use ‹ Prev / Next › / Today to move between months. Choose a day to see its jobs and bookings; this week's jobs can be ticked or unticked from there. History is kept in a date log, so past months stay visible after the weekly reset.
- **Settings** (⚙): kid names, photo upload, colour, jobs for each day and slot, reset to example jobs, copy jobs to the other kids, add or remove kids (up to 4), bookings (one-off on a date, or weekly on a weekday, for one kid or the whole family), 📺 TV setup code, main-screen layout, sound on/off, auto-reset each Monday (on by default), start a fresh week now (all-time totals are kept), erase everything.
- Remote controls: arrow keys move between the big buttons, OK selects, and Back (Samsung key 10009) or Esc closes settings and pop-ups.

## Getting it onto the Samsung TV (simplest first)
1. **Netlify Drop** (free, about 1 minute): on a computer, open https://app.netlify.com/drop and drag the `kids-dojo` folder (or just `index.html`) onto the page. You get a link like `https://random-name.netlify.app`. Without an account the link expires after about an hour. A free account makes it permanent and lets you rename it, e.g. `ferrier-dojo.netlify.app`.
2. **GitHub Pages** (free, permanent): make a repo, upload `index.html`, then go to Settings → Pages → Deploy from branch `main`. The URL is `https://<user>.github.io/<repo>/`. Note that the URL is public, though no one will find it unless they're given the link.
3. **Local network, nothing online:** on any always-on PC or Mac on the home Wi-Fi, run `python3 -m http.server 8080` in this folder. On the TV, open `http://<pc-ip>:8080/`. This only works while that computer is on.

Then on the TV: press Home, open **Internet** (Samsung's browser), go to the URL, and press OK. Add it to Bookmarks, or use "Add to Home" or "Pin to Home" where the model offers it so it appears as a tile on the home screen. To go full screen, use the browser menu → Full screen if it's offered.

## Photos
The default avatars are free stock photos, cropped to the face and embedded as base64:
- Charlie: "Portrait of a Happy Boy" by **Bruno Curly**, https://www.pexels.com/photo/13614367/
- Pip: "Joyful Child with Ice Cream Smudges Smiling" by **Manda ANDRIA**, https://www.pexels.com/photo/31402278/
- Jack: "Portrait of Young Boy in Blue Shirt" by **Aibek Skakov**, https://www.pexels.com/photo/28712540/

All three are under the Pexels Licence (free to use and modify, no attribution required; credited here anyway). To use a real photo of your kid, go to Settings → Choose photo. It's auto-cropped to a square and stored only on that device.

All the art (character, block, coins, scenery) and the sounds (WebAudio synth chime) are original. No Nintendo assets are used.

## Family photos and bookings without publishing them
The public app only ever contains the stock photos and no family bookings.
- **📺 Setup code (easiest on the TV):** the first time the app opens it offers *Enter code* (also in Settings → TV setup code). Type the 8-character code (like `ABCD-2345`) on the big on-screen keypad with the arrows and OK. The app fetches `d/<id>.bin` from this same site and unlocks it in the browser (AES-256-GCM, key from PBKDF2-SHA256 with 250,000 rounds). The file is encrypted and its name gives nothing away; without the code it's unreadable. The photos and bookings are then saved on that device only. After an update, Settings → *Update from code* fetches it again.
- **Setup link:** opening `…/index.html#setup=Charlie~<base64 jpeg>` (optionally with `|bookings~<base64 json>`) still works. It saves those photos and bookings into that device's browser storage, then removes them from the address bar. The part after `#` is never sent to the web server.
- **Phone/laptop:** Settings → Choose photo.
- `cd private && python3 make_private.py [Jack=photos/jack.png] [Charlie=…] [Pip=…]` (git-ignored, never published). With no arguments it uses whatever is in `private/photos/` named `charlie.*`, `pip.*` or `jack.*`. It creates:
  - `private/tv-code.txt`, the TV code. It is kept on every re-run, so the code never changes; `--new-code` issues a fresh one.
  - `publish/d/<id>.bin`, the encrypted photos + bookings to upload next to `index.html`
  - `private/index-private.html`, `private/setup.html` and `private/setup-link.txt` (the long-link alternative)

## Limitations
- **Data is stored per device and per browser.** Ticks made on a phone won't show on the TV and vice versa (a #rewards tab in the same browser does follow along). Use one main device (the TV) or just accept the separate tallies. Syncing would need a small backend, such as a free Firebase/Supabase project.
- Uploading a photo on the TV usually isn't possible because the TV browser has no file picker. Set photos up on the device the kids actually use. On the TV, the easiest fix is to replace the photos in `src/`, run `python3 src/build.py`, and re-upload.
- Typing names and jobs on the TV works through the on-screen keyboard, but it's slow. It's easier on a laptop if the TV isn't the main device.
- Sound needs one key press or tap first (browser autoplay rule). Older Samsung browsers might not play WebAudio at all.
- Clearing the TV browser's data wipes the board. There's no export or backup yet.
- The setup code needs a browser with WebCrypto on an https page (GitHub Pages is https). Very old TV browsers without it can use the setup link instead.
- It's been tested in desktop Chrome (headless) at 1920×1080, 1280×720, 960×540 (the size some TV browsers report) and at phone size; the test checks that no booking or job is clipped on either page. It hasn't been tested on a real Samsung TV. The code avoids newer JS/CSS features so that roughly 2018+ Tizen models should cope.

## Files
- `index.html`: the whole app
- `d/<id>.bin`: the encrypted family bundle for the setup code (optional)
- Source (not in the published repo): `src/app.html`; `src/build.py` embeds the stock photos and writes `index.html` and `publish/`; `src/test_screens.py` is the Playwright test that also writes the screenshots.
