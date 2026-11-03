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
19. Check the model name in Settings against the models listed in Google AI Studio. I could not verify `gemini-3.8-flash` from here, so change it if Google lists another.

## If something goes wrong
- **"Could not load ..."**: the rules were not published, or your email is not in them (step 11).
- **Sign-in popup closes or errors**: the GitHub domain is missing from Authorized domains (step 9).
- **Blank page**: a quote or comma was removed in `firebase-config.js`.
- **AI buttons do nothing**: the Gemini key or model name (steps 18 and 19).

Fatimah signs in with her own Google account. She sees Today, Scoreboard and Decisions, and can update Decisions only.

## Added later: Tilly, searching and suggestions
- **Tilly** is the assistant. Use the **Tilly** button at the top on any tab, or the Ask Tilly tab. It needs the Gemini key in Settings.
- **Morning event search.** The first time you open the app each day, Tilly searches the web for events and lists them under Events as suggestions. Nothing is added until you press Add to events. It only runs when someone with edit access opens the app.
- **Finding contacts and new sponsors.** Use Find contact details with Tilly inside a sponsor, and Find new sponsors on the Sponsors tab. Always check the source link before using anything.
- **Suggestions tab.** Fatimah can write suggestions there. For this to work she must be on the rules list, and you must republish the updated `firestore.rules` (Firestore Database, Rules tab, paste, Publish).

## Giving Fatimah more access
Open `firebase-config.js`. Three lists decide what each person can do:
- `editors`: everything (you).
- `contributors`: add and change sponsors, contacts and events, answer decisions and write suggestions. They cannot delete, and they do not see Tilly, the plan, the Proposal Kit, Deals, Balance or Activity.
- `viewers`: Today, Scoreboard, Decisions and Suggestions only.

Put Fatimah's Google email in `contributors`. Then open `firestore.rules` and replace `PASTE_FATIMAH_EMAIL@gmail.com` with the same email, copy the whole file into Firestore Database, Rules tab, and click Publish. If you use `viewers`, replace `PASTE_VIEWER_EMAIL@gmail.com` the same way.

## Optional: a Groq key for higher free limits
1. Go to console.groq.com, sign in, open API Keys and create a key.
2. In the app, open Settings and paste it into "Groq API key". Leave the model blank. Save.
3. Briefs, drafts, pasted updates and questions now use Groq. Anything with "search the web" ticked, and the event and contact finders, still use Gemini. If Groq is busy, Tilly tries Gemini.

## Audience and terms (Proposal Kit tab)

The Audience box holds the figures and named followers sponsors are told about, and the Terms box holds the payment, cancellation and usage terms. Edit either one and Tilly uses the new wording in every draft. Paste more followers into the Audience box and use Sort with Tilly to keep only organisations and stated roles.

## Prices and the quote builder (Proposal Kit tab)

Placement prices are Fatimah's card prices. Package prices are "from" prices: the card prices of what the package contains, plus any add-on, plus 10%, rounded to ₦5,000. Production (photographers, videographers, sound, equipment, travel) is quoted to brief at cost plus 10%, so those rows carry no number. How the prices are built explains the rule in plain words. The Quote builder adds up quantities, the production cost and the 10% production fee, before VAT and withholding tax, and copies the result. Tilly quotes only prices from the rate card.

## Who we do not approach

TLLJ does not work with alcohol, tobacco or gambling brands, or alcohol-led events, so none are on the sponsor list. Tilly will not suggest them either.

## Attaching files to a sponsor

The "Sponsor in focus" section on Today has a file box for each sponsor. Files go into the same database as everything else, so there is nothing to set up and no card is needed. Each file can be up to 700 KB (a PDF or Word dossier is usually well under that). Only editors can upload and remove. Everyone with access can download.

## Create a proposal, export and check-ins

- **Create a proposal** (top of the Proposal Kit): choose the sponsor and a template, tick what they are buying, add the production cost if there is one, and press Generate proposal. The sponsor's name, contact, audience figures, price lines and all terms are filled in; anything still in [brackets] is listed. Fill the rest with Tilly, save the result to the sponsor or save it as a new template. From a sponsor, press Create a full proposal.
- **Export**: the Export button in the top bar downloads every tab as one Excel file (one sheet per tab) or one CSV.
- **Suggested next steps** can be dismissed one by one with the × or all at once. Show dismissed again brings them back.
- **Next target**: set how long it runs in days, weeks or months.
- **Daily check-in** (Ask Tilly) writes a short note for Fatimah. **Follow-ups** have a What to say button, and reminders also announce follow-ups due in the next two days.
- **Activity** now shows sponsor work only: emails sent, replies, calls, proposals, stage moves and which live conversations have gone quiet.

## Partnerships mode

Use the toggle above the tabs to switch between Sponsorships and Partnerships. The choice is remembered on that device.

- **Partners**: press invitations, media partnerships and collaborations. Each has *We give* and *We get*, one of five stages (idea, approached, terms agreed, delivering, wrapped up), an optional link to an event (dates, accreditation, who attends), a contact, and one next step.
- **Templates**: a media-partner offer and a collaboration proposal, filled from the partner. Missing details stay in [brackets] and are listed. Nothing is sent from the app.
- **Wrap-ups**: what each side delivered and what it was worth to TLLJ (1 to 5), and whether you would do it again.
- **Follow-ups** belong to a mode (Sponsorships, Partnerships or both). **Ask Tilly** and the brief follow the mode you are in. Export adds a Partners sheet.

## Packages and "What happened?"

- **Packages:** inside each partner, "We give" and "We get" are lists of packages. Each has a name, the detail, a date and a tick for delivered or received. The ticks feed the wrap-up automatically.
- **What happened?** On Today, in both modes, anything past its date asks for an outcome: events that have ended, sponsors and partners whose next step date has passed. Log the result and the next step (or tick "Nothing further needed"). Sponsor outcomes go into the outreach log, partner outcomes into the partner, event outcomes into the Events tab.
- Search and Activity show only what belongs to the mode you are in. Events are shared by both modes.

## Paste an email, Review and the calendar file

- **Paste an email** (Partners and Today, Partnerships mode): paste a reply or invitation. Tilly pulls out the partner, what we give, what we get, dates and the next step. Every field is editable and nothing is saved until you press Save. It can add to an existing partner.
- **Review** (both modes): *Meeting* is one screen for Fatimah showing what moved, what is stuck and the decisions needed. *Weekly* shows sponsors and partners side by side. Both can be copied as text and use the period you choose. Partner questions for Fatimah go in "Needs a decision from Fatimah".
- **Calendar file:** downloads every dated next step, follow-up, package due date and event as an .ics file with a 9 am reminder. Open it on your phone and choose Add All. Importing it again updates the same entries instead of duplicating them. A partner also has its own Add to calendar button.

## Templates, events and duplicates

- **Templates** (Partnerships): Media-partner offer, Collaboration proposal, Press access and coverage request, and Coverage follow-up. Use "Add a template" to write your own with placeholders such as {name}, {first}, {topic}, {dates}, {give}, {get}, {delivered}. Custom templates can be edited or deleted.
- **Events from a partner:** choose "+ Add a new event" in a partner's Event list, or in Paste an email. A name is enough; add the dates and place later under Events. Undated events are flagged in Review.
- **No duplicates:** a partner whose next step already has an open follow-up is not repeated under "Needs a move"; "Add a follow-up" will not create a second one for the same date; a pasted email for an existing name must be added to that partner; events with the same name are linked instead of created again.
- The mode toggle now sits in the header, and the tabs stay on one line (they scroll sideways on a phone).

## Coverage and moving between modes

- **Coverage** (both modes): log each published piece with its link, where it ran, the date, reach and who it was for. Choosing a package ticks it as delivered. Coverage shows under the partner, in wrap-ups, in Review, in search and in the export, and the "Coverage follow-up" template fills in the links.
- **Move to Sponsorships / Move to Partnerships:** a button in the partner window and in the sponsor window. The contact, notes, follow-ups, coverage and history come with it. A sponsor with a deal record cannot be moved. Undo brings it back.

## Next moves, one-tap logging, packs and search

- **Today** opens with a greeting and your five most urgent moves (overdue and due follow-ups, outcomes to log, next steps, package dates, plan steps). The full lists stay below. Items already in the top list are not repeated under "What happened?".
- **Follow-ups** have Sent, Replied and No reply (+3 days). They log on the sponsor (outreach log) or the partner (outcomes) and tick the follow-up done, except No reply, which moves the reminder.
- **Press /** anywhere to search partners, sponsors, contacts, events, coverage, follow-ups and decisions.
- **Partner packages:** type or pick from the list. Picking a rate-card package fills in what it includes. When a package is ticked delivered, an "Add the link" button logs the coverage.
- **Pitch pack and Coverage report** (Review and Coverage tabs): open the print window and choose Save as PDF. Internal notes are never printed.
- **Decisions:** archive single decisions or all answered ones; show archived to restore.

## Version 35: times, places, tabs
- **Times.** Events have a start and an end time. Partner and sponsor next steps, follow-ups and packages each have an optional time beside the date. Times show wherever the date shows, in Next moves, the weekly review and the calendar file. A dated item with a time lands in your calendar at that time with a 30-minute reminder. Without a time it stays an all-day entry.
- **Places.** Open the Events tab and scroll to Places. A place is added when you save an event with a place. It is also suggested when you type a place on the next event. Mark each place Invited, Going, Been or Considering, add the area and a note. Search finds places too.
- **Tabs.** The tabs are centred with a soft pill around each one. The current tab is filled.
- **Pasting an email.** The preview now has a time box beside the date. It fills in when the email gives a time.
- **Added from your emails.** ART X: the Tokini slot on Sat 7 Nov (3pm to 4pm, 20 minutes) is the next step, and the Das or Fall interview is noted as pending. Affinity Gallery is a new partner with the materials marked received, an Affinity Gallery exhibition event (5 Nov to 31 Dec) and a place.
