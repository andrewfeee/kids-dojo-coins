# Dojo Coins – kids' jobs board for the Samsung TV

A single file (`index.html`, about 117 KB). Everything is inside it: the app, the art, the sounds and both default photos. It works offline, needs no build step, and saves to the browser's localStorage.

## What it does
- Weekly board, Monday to Sunday, with a Morning ☀️ and an Afternoon 🌙 job for each kid each day. Today's column is highlighted. Bookings (for example 🎾 Tennis 8:30–9:30am) also show in the morning or afternoon cell, sorted by time, with am/pm. Long titles wrap onto a second line in the week cell. Times before 12:00 are morning; 12:00 and later are afternoon. Bookings are not ticked and do not earn coins.
- Tick a job (OK/Enter on the remote, or tap) to earn 1 coin. That plays the celebration: the kid's face on a little runner jumps, hits a ? block, a coin pops out, flies over and lands on their coin pile, then confetti and a "Super star, Charlie!" banner. Press OK or Back to skip it.
- Each kid's coins for the week show as a growing pile with a number, plus an 🏆 all-time total.
- **+1 Bonus** gives a coin for anything that isn't on the board.
- **Undo** reverses the last coin. Choosing a job that's already ticked asks whether to untick it.
- **Kids:** Charlie, Pip and Jack by default, with a compact layout so all three fit on a 1080p screen.
- **Week view always opens first.** **Month** is a secondary button: the month view is a Mon–Sun grid with today highlighted. Each day shows a dot for each kid with ☀/☾ ticks for the morning and afternoon jobs plus the coins earned that day, and a 📅 mark if that day has bookings. Use ‹ Prev / Next › / Today to move between months. Choose a day to see its jobs and bookings; this week's jobs can be ticked or unticked from there. History is kept in a date log, so past months stay visible after the weekly reset.
- **Settings** (⚙): kid names, photo upload, colour, jobs for each day and slot, reset to example jobs, copy jobs to the other kids, add or remove kids (up to 4), bookings (one-off on a date, or weekly on a weekday, for one kid or the whole family), sound on/off, auto-reset each Monday (on by default), start a fresh week now (all-time totals are kept), erase everything.
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

## Using a real photo without publishing it
The public app only ever contains the stock photos. To put a real photo on a device:
- **Phone/laptop:** go to Settings → Choose photo.
- **Setup link:** opening `…/index.html#setup=Charlie~<base64 jpeg>` (optionally with `|bookings~<base64 json>`) saves those photos and bookings into that device's browser storage, then removes them from the address bar. The part after `#` is never sent to the web server.
- `cd private && python3 make_private.py Jack=photos/jack.png [Charlie=photos/charlie.jpg] [Pip=photos/pip.jpg]` (git-ignored, never published) creates:
  - `private/<name>.jpg` face crops
  - `private/index-private.html`, with the real photos embedded and stock photos for any kid not given
  - `private/setup.html` and `private/setup-link.txt`, one link that sets all the given photos (and any private bookings) at once
- **To get the photos onto the TV:** on a home computer, run `python3 -m http.server 8080` inside `private/`. On the TV, open `http://<computer-ip>:8080/setup.html` once.

## Limitations
- **Data is stored per device and per browser.** Ticks made on a phone won't show on the TV and vice versa. Use one main device (the TV) or just accept the separate tallies. Syncing would need a small backend, such as a free Firebase/Supabase project.
- Uploading a photo on the TV usually isn't possible because the TV browser has no file picker. Set photos up on the device the kids actually use. On the TV, the easiest fix is to replace the photos in `src/`, run `python3 src/build.py`, and re-upload.
- Typing names and jobs on the TV works through the on-screen keyboard, but it's slow. It's easier on a laptop if the TV isn't the main device.
- Sound needs one key press or tap first (browser autoplay rule). Older Samsung browsers might not play WebAudio at all.
- Clearing the TV browser's data wipes the board. There's no export or backup yet.
- It's been tested in desktop Chrome (headless) at 1920×1080, at 960×540 (the size some TV browsers report) and at phone size. It hasn't been tested on a real Samsung TV. The code avoids newer JS/CSS features so that roughly 2018+ Tizen models should cope.

## Files
- `index.html`: the whole app (this is the only file you need)
- `src/app.html`: source with avatar placeholders; `src/build.py` embeds the photos in `src/` into `index.html`
- `src/test_screens.py`: Playwright smoke test that writes the screenshots
- `screens/`: screenshots
