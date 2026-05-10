# Teng Family Japan Trip · August 2026

A simple, mobile-friendly trip companion app for the Teng family's August 2026 trip to Osaka, Kyoto, and Tokyo. Everything lives in a single `index.html` file — no backend, no build step, no logins.

## What's inside

- **Home** — countdown, "up next" card, quick links
- **Itinerary** — day-by-day plans (editable)
- **Flights** — Air Canada AESAK5 (outbound confirmed; return needs date)
- **Hotels** — Hyatt Place Kyoto + two other Expedia bookings (some details TBD)
- **Map** — interactive Leaflet/OpenStreetMap with restaurants & sights, filtered by city/type
- **Add a place** — paste a Google Maps link and save it to the map (stored locally; export to share)
- **Phrases** — useful Japanese with romaji
- **Tips** — money, transit, etiquette, August weather warnings, emergency numbers, currency converter

## Deploy to GitHub Pages (≈10 min)

### 1. Create the repo

Go to github.com → New repository.

- **Name:** `japan-trip` (or whatever)
- **Visibility:** Public (required for free GitHub Pages — but the URL is unguessable unless someone has it)
- **Initialize with a README:** unchecked
- Click **Create repository**

### 2. Upload the files

Easiest path — drag & drop in your browser:

1. On the empty repo page, click **uploading an existing file**.
2. Drag `index.html` and `README.md` from this folder into the upload area.
3. Scroll down, write a commit message ("Initial trip app"), click **Commit changes**.

### 3. Turn on Pages

1. In the repo, go to **Settings** (top right) → **Pages** (left sidebar).
2. Under "Build and deployment" → "Source", choose **Deploy from a branch**.
3. Branch: **main**, folder: **/ (root)**. Click **Save**.
4. Wait ~1 minute. Refresh the page. You'll see a green box with your URL:
   `https://<your-github-username>.github.io/japan-trip/`

### 4. Share with family

Just send them the URL. Tell them to add it to their home screen on their phone for an app-like experience:

- **iPhone:** Safari → Share → "Add to Home Screen"
- **Android:** Chrome → ⋮ → "Add to Home screen"

## Updating the app

### Quick edits in the browser

1. In your repo, click `index.html`.
2. Click the pencil ✏️ icon (top right of the file view).
3. Find the `TRIP = { ... }` section near the bottom of the file. Edit values (dates, hotel names, itinerary items, etc.).
4. Scroll down, write a commit message, click **Commit changes**.
5. The site updates within ~30 seconds.

### Common edits

**Add a new restaurant to the shared list (everyone sees it):**

Find the `seedPlaces:` array and add an object like:

```js
{ name: "Some place", city: "Tokyo", cat: "restaurant", lat: 35.6595, lng: 139.7005, notes: "Saw it on Insta" }
```

Get the lat/lng from Google Maps: right-click anywhere → click the coordinates that appear → they're copied to your clipboard.

**Update the return flight:**

In the `flights:` array, find the second entry (`route: "Tokyo → Toronto (YYZ)"`) and update `date`, `time`, `flightNo`, and change `status` from `"pending"` to `"confirmed"`.

**Fix a hotel address:**

In the `hotels:` array, edit the `address` field for the matching hotel.

## How "Add a place" works

When family members add restaurants through the in-app form:

- They get saved in **localStorage** on that person's device.
- They show up immediately on **that person's** map, marked with a gold star ★.
- **They do NOT sync to other family members** automatically (no backend).
- To share: tap **📤 Export my additions** to copy as JSON, send to Lilly, and Lilly pastes them into `seedPlaces` in `index.html`.

If you want true real-time sync across family later, options are: Firebase (free tier, ~30 min to set up), Supabase, or a Google Sheets backend. Happy to add this if you want.

## What was pulled from Gmail (May 2026)

Confirmed:
- ✅ Air Canada AESAK5 · Toronto → Osaka · Aug 1, 2026 (Booked Jan 13)
- ✅ Hyatt Place Kyoto · Aug 3 check-in · Expedia #72070028447596
- ✅ Osaka hotel · Aug 1 check-in · Expedia #72070027312765 (name not in email body)
- ✅ Tokyo hotel · Aug 5 check-in · Expedia #72070148748999 (name not in email body)

Cancelled (informational):
- ❌ Asakusa View Hotel Annex Rokku · Expedia #72070101281344 (cancelled Jan 17, refunded Jan 19; replaced by #72070148748999)

Not found yet:
- Return flight date/time (likely part of the AESAK5 booking — check Air Canada email or "Manage my booking")
- Specific Osaka and Tokyo hotel names (the Expedia confirmation emails are HTML-only and the booking details weren't in the plaintext)
- Any tour/activity bookings

## Tech notes

- Pure HTML/CSS/JS in one file. Zero build step.
- Map: [Leaflet](https://leafletjs.com/) + OpenStreetMap tiles (free, no API key).
- Fonts: system fonts only.
- All data is in the `TRIP = {...}` object at the top of the `<script>` block. Edit that to customize anything.
- No analytics, no tracking, no cookies. Just localStorage for user-added places.
