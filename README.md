# Kerala Frozen — Field Visit Tracker

A one-file web app for a Hannover → Frankfurt sales run. Shows the shop route on a map, detects when you arrive at a shop by GPS, pops a visit form for your products, lets you skip with a reason, and exports everything to Excel.

**Products tracked:** Beef Cutlet, Kappa Biriyani, Chicken Biriyani, Beef Biriyani, Beef Pickle.

## Put it online (GitHub Pages)

1. Create a new GitHub repository (e.g. `kerala-route`).
2. Upload **all of these files into the same repo folder**: `index.html`, `manifest.json`, `icon-180.png`, `icon-512.png` (and this `README.md`).
3. Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: **main**, folder **/(root)** → Save.
4. After ~1 minute your app is live at `https://<your-username>.github.io/<repo>/`.
5. Open that link **on your phone** and tap **Start GPS** → **Allow** location.

GitHub Pages serves over HTTPS, which the browser requires before it will share GPS.

## Install on iPhone (add to Home Screen)

This is a web app, so it installs through Safari — not the App Store.

1. Open your GitHub Pages link **in Safari** (must be Safari, not Chrome, for this to work).
2. Tap the **Share** button (the square with an ↑ arrow, at the bottom).
3. Scroll down and tap **Add to Home Screen**.
4. Name it (e.g. "Kerala Route") and tap **Add**.
5. A "Kerala Route" icon now sits on your home screen and opens **fullscreen**, like a normal app.

**Two iPhone settings that matter for GPS:**

- **Precise Location must be ON.** First time you tap Start GPS, choose **Allow While Using**. Then check **Settings → Privacy & Security → Location Services → Safari** (or the web app) → **Precise Location = ON**. Without it, iOS gives a coarse position and the arrival pop-up won't trigger accurately.
- **Stop the screen from sleeping.** The arrival alert only fires while the app is on screen, so during the trip set **Settings → Display & Brightness → Auto-Lock → Never** (or a long time), or keep the phone in a car mount. Turn Auto-Lock back to normal afterwards to save battery.

Android is similar: open the link in Chrome → menu (⋮) → **Add to Home screen / Install app**.

## How to use on the day

- **Start GPS** — the status bar shows the next shop and how far away you are; your position is the blue dot.
- **Arrive** — within ~130 m of a shop the visit form pops automatically (banner + vibration; a notification too if you allowed it). If it doesn't fire, tap **📍 I'm here / Log** on the shop's card.
- **Log the visit** — tick the products the shop wants, set quantities, pick an outcome (Ordered / Interested / Not now), add notes, **Save**.
- **Skip** — tap **⤼ Skip** and choose a reason (Closed, No time, Owner away, Not interested, Already supplied).
- **🎯 Target** — centres the map on a shop and makes it the active one.
- **⬇ Excel** — downloads `kerala_visits.xlsx` with every shop, status, products + quantities, outcome/skip reason, notes and timestamps.

Your entries are saved on the phone (survive refresh). Export at the end of the day.

## Known limits (web app, no backend)

- **Foreground only.** GPS arrival works while this page is open and the screen is on. A locked or backgrounded phone won't alert you — that needs a native app. Keep the page open (a co-driver holding the phone is ideal).
- **GPS radius** is ~130 m so it triggers reliably in town; tighten `ARRIVE_M` in `index.html` if you want it closer.
- **Excel is one-way** (export). Live sync back into a shared Excel/Google Sheet needs a backend — can be added later.

## Editing the shop list

The shops are the `STOPS` array near the top of the `<script>` in `index.html`:
`[id, name, city, tier, address, phone, hours, lat, lng]`. Edit there, or ask to have it generated from the spreadsheet.
