# Lift Baseline (home screen app)

Your lifting app, packaged so friends can install it from a link. No app store, no accounts, works with no signal. Each person's data stays on their own phone.

## What's in here

| File | What it does |
|---|---|
| `index.html` | The app (your original, plus setup wizard, backup, install prompt) |
| `manifest.webmanifest` | Name, icon and full screen settings for the home screen |
| `sw.js` | Offline support. Caches the app on the phone |
| `icons/` | Home screen icons (`icon.svg` is the source if you want to edit) |
| `fonts/` | Barlow fonts, stored locally so the app looks right offline |

## Put it online (pick one)

It has to be served over https for install and offline to work. Opening `index.html` straight from your computer will run, but won't install.

**Netlify Drop (2 minutes, no account needed to try)**
1. Go to app.netlify.com/drop
2. Drag this whole folder onto the page
3. You get a link like `something.netlify.app`. Claim it with a free account so it doesn't expire, and rename it in Site settings if you want.

**GitHub Pages**
1. Make a new repo and upload everything in this folder to the top level (not inside a subfolder)
2. Settings > Pages > Source: Deploy from a branch > `main` / root > Save
3. Link shows up in a minute or two: `https://<account>.github.io/<repo>/`

Free GitHub plans only publish Pages from public repos. The code is public that way; nobody's workout data is, because that never leaves their phone.

## What to send your friends

> Open this link in Safari (iPhone) or Chrome (Android): LINK
> Before setting anything up, add it to your home screen. iPhone: Share button, then Add to Home Screen. Android: menu, then Install app.
> Open it from the new icon and answer the setup questions. It builds your workouts.

The "install first" part matters on iPhone: the home screen app keeps separate storage from Safari, so anything set up in Safari first won't carry over. (If someone does it backwards, they can Save backup in Safari and Restore in the installed app.)

## How it works for them

- **Setup wizard** on first open: units, goal, age, gender, bodyweight, days per week (2 to 6), equipment (full gym, home barbell, dumbbells, bodyweight) and best recent sets. It builds 2 to 5 starter routines and sets starting weights from their best sets. Anything without a best set starts light on purpose.
- **Training** works exactly like your version: guided sets, rest timer, plate math, reps-left rating that sets the next weight.
- **Breakdown with AI:** after a workout, Copy summary and paste it into Claude or any AI chat.
- **Backup:** Progress tab > Save backup file. Uses the share sheet on phones, so it can go straight to iCloud Drive, Google Drive or a text to themselves. Restore merges sessions and can also move everything to a new phone.
- **Run setup again** (Routines tab) rebuilds routines without touching their logged history.

## Updating the app later

Change the files, then bump `VERSION` in `sw.js` (for example `lift-v2`) and re-upload. Phones pick up the new version in the background and show it the next time the app is opened. If you skip the version bump, phones can keep showing the old copy.

## Good to know

- Data lives in the browser storage of each phone. Deleting the app icon or clearing website data wipes it, hence the backup button.
- The PRT / PSS test tracking from your version is still there under Routines for anyone who needs it.
