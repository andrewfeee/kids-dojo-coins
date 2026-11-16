# Dojo Coins v4.3 – kids' jobs board for the Samsung TV

A single file (`index.html`, about 190 KB). Everything is inside it: the app, the art, the sounds and the default photos. It works offline (only the optional setup code needs the internet), needs no build step, and saves to the browser's localStorage.

## What it does
- **One main screen, no clicking through.** Days run across, kids run down (Charlie blue, Pip pink, Jack yellow), and every day cell is split into ☀️ Morning and 🌙 Afternoon. Each half shows that kid's bookings (emoji, title and time, e.g. 🎾 Tennis 8:30–9:30am) and the job with its tick. Whole-family bookings appear once, in a 👪 Family band along the top. Today's column is outlined in gold.
- **Mon–Fri and Sat–Sun pages** keep the text big enough to read from the couch. The page holding today opens first. Press ▶ on the remote past Friday to reach the weekend, or ◀ past Saturday to go back, or use the Mon–Fri / Sat–Sun buttons. Keep going ▶ past Sunday for next week's Mon–Fri, or ◀ before Monday for last week's weekend.
- **◀ / ▶ week buttons** at the top step to the previous or next week (the label shows e.g. *Last week 9–15 Nov*); **This week** jumps back, and so does Back on the remote. Bookings and ticks show for whichever week is on screen; only this week's jobs can be ticked. Prefer everything on one screen? Settings → Main screen → All 7 days (smaller text).
- Tick a job (OK/Enter on the remote, or tap) to earn that job's coins, shown as the small gold number in the chip's corner: Stack dishwasher 5, Pack lunch 7, Sort laundry 2, Feed chooks 6 (weekend mornings), Unpack bag 1 (every afternoon, every kid), anything else 5. Change any job's value, or the default for new jobs and +Bonus, in Settings → 🪙 Coins. A slot can hold several jobs, written `Tidy room + Unpack bag` in Settings; each gets its own tick and value. That plays the celebration: the kid's face on a little runner jumps, hits a ? block, a coin pops out, flies over and lands on their pile, then confetti and a "Super star, Charlie!" banner. Press OK or Back to skip it.
- **🏆 Rewards** is a separate display with each kid's photo, coins to spend, a heap with exactly one coin drawn per coin (coins shrink and the heap widens as it grows), coins this week, the all-time earned total and **+5 Bonus**. Open `…/#rewards` on a second screen or tab and it follows ticks made on the main screen (same browser), playing the coin animation as they land.
- **Undo** reverses the last coin. Choosing a job that's already ticked asks whether to untick it.
- **🛒 Market** (`#market`): kids spend coins. *30 min device time* (25 coins) is bought by one kid; *Movie night* is a group treat where Charlie, Pip and Jack each commit 50 coins, it shows who's in, unlocks with a celebration once all three have committed, and pledges can be taken back until then. Every purchase asks to confirm (OK buys, Back cancels), coins visibly leave the pile, and the purchases list has a parent **↶ Undo purchase**. Items (name, emoji, price, one kid or group and which kids) are edited in Settings → Marketplace.
- **📜 History** (`#history`): every coin in and out with date and time, which job (morning/afternoon) or bonus, purchases, pledges, refunds and undone ticks (shown as reversed entries), with each kid's running balance. ◀ ▶ switch between Everyone and each kid, ▲ ▼ scroll. The weekly reset never clears it.
- **Running animals** (Settings, on by default): every 3–8 minutes a small Jack Russell, cow, bull, chook or horse tries to cross the screen corner to corner through the gaps between the cells, with wrong turns, backtracking and sniffing pauses. It runs *in front* of everything on the board (only pop-ups, Settings and the code keypad sit above it), but clicks and the remote go straight through it to whatever is underneath, and it fades while crossing the focused job; it never takes focus, pauses when the page is hidden and stays off with reduced motion.
- **Kid riders** (Settings, on by default, also covered by Running animals): taking turns with the farm animals, Charlie and Jack ride by on little dirt bikes (spinning wheels, a bounce, a long dirt trail) and Pip gallops past on her horse in a dust cloud. Each has a wobbly oversized bobblehead: the kid's own photo when it's saved on this device, otherwise a cartoon face with their initial. Same rare timing, maze route and in-front layer as the animals, never focusable.
- **Settings** (⚙): kid names, photo upload, colour, jobs for each day and slot, reset to example jobs, copy jobs to the other kids, add or remove kids (up to 4), bookings (one-off on a date, or weekly on a weekday, for one kid or the whole family), 📺 TV setup code, main-screen layout, sound on/off, auto-reset each Monday (on by default), start a fresh week now (balances, purchases and history are kept), coins per job, marketplace items, running animals on/off, erase everything.
- **Remote (D-pad) controls:** every arrow press is handled by the page itself (spatial navigation to the nearest control in that direction, gold focus ring), OK/Enter selects, Back (Samsung key 10009) or Esc closes pop-ups, Settings, Rewards/Market/History and other weeks. Something is always focused, so the remote never falls back to the mouse pointer because focus was lost. The setup-code keypad is a strict grid (▲▼◀▶ between keys, OK types, ⌫ Delete, ✓ Load). On TVs that pass colour keys to web pages: Red = Rewards, Green = week, Blue = Settings (Yellow is left for the browser).

### If the arrows still move a mouse pointer on the TV
Samsung's TV browser decides whether the arrows go to the page or drive its own pointer; a web page can't switch that off. If you see a pointer: (1) press OK once on the page and try the arrows again; (2) on older models press the **Yellow** button (or look in the browser's menu/settings) to switch from *Pointer mode* to *Tab/focus mode*; (3) with a Samsung *Smart Remote*, avoid waving it (motion moves the pointer) and use the ring/arrow keys; (4) pointer mode still works: the gold ring follows the pointer and OK ticks what's under it, and every button is large. The fully reliable fix is installing it as a Tizen web app (Developer Mode + Tizen Studio), where remote keys always go to the app.

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
