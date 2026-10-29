# TLLJ Partnerships Desk: setup guide (no coding needed)

You will do four things: set up Firebase (database and sign-in), edit two small files, upload to GitHub, and load your data. Allow about 30 minutes. It is free at this size.

**Before you start:** the app already works without Firebase. Open `index.html` by double-clicking it and it runs in "Demo mode", saving in that browser only. Use that to look around first if you like.

## Part 1: Firebase

1. Go to https://console.firebase.google.com and sign in with mycashierai@gmail.com.
2. Click **Create a project** (or **Add project**). Name it `tllj-desk`. Continue.
3. Turn **off** Google Analytics. Click **Create project**, then **Continue**.
4. On the project home page, click the **web icon** (`</>`) under "Get started by adding Firebase to your app".
5. Nickname: `tllj-desk`. Leave "Firebase Hosting" unticked. Click **Register app**.
6. You will see a block of code with `apiKey`, `authDomain`, `projectId`, `appId`. Keep this page open. Click **Continue to console** when done.
7. Open `firebase-config.js` in any text editor (Notepad is fine). Copy the four values over the `PASTE_...` placeholders, keeping the quote marks. Put Fatimah's Google email in `viewers`. Save. (These values are not secrets. The rules in Part 2 are what protect your data.)
8. In the left menu choose **Build, then Authentication**. Click **Get started**. Pick **Google**, switch **Enable** on, choose your email as the support email, **Save**.
9. Still in Authentication, open **Settings, then Authorized domains**. Click **Add domain** and enter `YOURGITHUBNAME.github.io`. You can come back to this after Part 3 if you do not know it yet.
10. In the left menu choose **Build, then Firestore Database**. Click **Create database**. Choose the location closest to you (Europe is a sensible pick; it cannot be changed later). Choose **Start in production mode**. Click **Create**.
11. Open the **Rules** tab. Delete what is there. Open `firestore.rules`, replace `PASTE_FATIMAH_EMAIL@gmail.com` with her email, copy everything, paste it into the box, click **Publish**.

## Part 2: GitHub

12. Create a new repository named `tllj-desk`. Public or private both work. If you choose private, GitHub Pages needs a paid plan, so public is simpler. The repo holds no private data because `seed.json` is excluded.
13. Upload these files: `index.html`, `firebase-config.js`, `firestore.rules`, `GUIDE.md`, `README.md`, `.gitignore`. **Do not upload `seed.json`.**
14. In the repo go to **Settings, then Pages**. Under Source choose **Deploy from a branch**, branch `main`, folder `/ (root)`, **Save**.
15. After a minute your site is at `https://YOURGITHUBNAME.github.io/tllj-desk/`. If you skipped step 9, do it now.

## Part 3: First use

16. Open your site and click **Sign in with Google**.
17. On the "No data yet" screen choose `seed.json` (on your computer, kept out of GitHub). Wait for "records loaded".
18. Go to https://aistudio.google.com/apikey and create a key. In the app click **Settings**, paste the key and save. It stays in that browser only. Do this on each device you use.
19. Check the model name in Settings against the models listed in Google AI Studio. I could not verify `gemini-2.5-flash` from here, so change it if Google lists another.

## If something goes wrong
- **"Could not load ..."**: the rules were not published, or your email is not in them (step 11).
- **Sign-in popup closes or errors**: the GitHub domain is missing from Authorized domains (step 9).
- **Blank page**: a quote or comma was removed in `firebase-config.js`.
- **AI buttons do nothing**: the Gemini key or model name (steps 18 and 19).

Fatimah signs in with her own Google account. She sees Today, Scoreboard and Decisions, and can update Decisions only.
