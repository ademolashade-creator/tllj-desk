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

Fatimah signs in with her own Google account. She sees Today, Sponsors, Pipeline, Contacts, Events, Activity (Scoreboard and Decisions) and Review, and can update Decisions only.

## Added later: Tilly, searching and suggestions
- **Tilly** is the assistant. Use the sparkle icon at the top right on any tab, or the speech-bubble icon for the Ask Tilly page. It needs the Gemini key in Settings.
- **Morning event search.** The first time you open the app each day, Tilly searches the web for events and lists them under Events as suggestions. Nothing is added until you press Add to events. It only runs when someone with edit access opens the app.
- **Finding contacts and new sponsors.** Use Find contact details with Tilly inside a sponsor, and Find new sponsors on the Sponsors tab. Always check the source link before using anything.
- **Suggestions tab.** Fatimah can write suggestions there. For this to work she must be on the rules list, and you must republish the updated `firestore.rules` (Firestore Database, Rules tab, paste, Publish).

## Giving Fatimah more access
Open `firebase-config.js`. Three lists decide what each person can do:
- `editors`: everything (you).
- `contributors`: add and change sponsors, contacts and events, answer decisions and write suggestions. They cannot delete, and they do not see Tilly, the plan, the Proposal Kit, Deals, Balance or Activity.
- `viewers`: Today, Activity (Scoreboard and Decisions), Review and Suggestions only.

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

## Version 36: Contributors, approvals, team
- **Contributors mode.** The third button in the header. **People** holds writers, photographers, videographers and stylists, each with a status (New, Contacted, Test sent, Active, Keep on file, Declined). **Import a list** takes a CSV file or pasted rows. **Who for this brief?** ranks people for a piece.
- **Assignments.** One piece from pitch to publication: invite several people to pitch, choose one, draft a "not this time" note for the others, and add the brief, draft and published links. Setting the stage to Published logs the piece in Coverage. Agreed fee and Paid are visible to Sade and Fatimah. Praise sees paid or unpaid.
- **Approvals.** Outreach, briefs, proposals and pieces move from Draft to With Fatimah, then Approved, Changes asked or Declined. Fatimah answers from the email or from the Approvals page. Sade sends once it is approved. **Needs you** sits at the top of Today in every mode. **Copy WhatsApp note** and **Record her answer** cover answers given outside the desk. **Check the style** flags em dashes, banned words and "TLLJ" in external copy.
- **Team.** Settings, Team: add or remove people. Everyone listed can own a step, sponsor, partner or task.
- **Roles.** Sade has full access. Fatimah sees all three modes and answers approvals. Praise adds and updates everything but cannot delete, change settings or see fee amounts.
- **Push to Praise.** Activity page. Collects every change since the last push for the trackers, with Copy and Email.
- **Everything about one name.** In a partner, sponsor or person window.
- **Back up now.** Settings. Downloads every record as a file.
- **Google Calendar.** Assignment due dates have an Add to Google Calendar link.

### Email setup (optional)
Without setup, Send opens a Gmail compose window (or your mail app) with the text filled in. For one-click approvals and sending from the desk:
1. Open script.google.com, create a project, paste `Code.gs` and `appsscript.json` (Project Settings, show the manifest).
2. Fill in CONFIG at the top: a long secret phrase, your Firebase project ID, the desk link and the three addresses.
3. Deploy, New deployment, Web app. Execute as Me. Access: Anyone. Authorise when asked.
4. In the desk, Settings, Email: choose the Apps Script mailer, paste the web app URL and the same secret phrase.
5. Run `setupTriggers` once in the script for the 7:30 am daily digest (Lagos time).
Zoho: choose **My mail app** to open Zoho Mail from the desk, or paste a Zoho Flow webhook URL and choose the Zoho Flow route. The webhook receives to, cc, subject, text and html. Approval buttons in an email need the Apps Script URL.

### Access (rules and config)
Publish `firestore.rules` in Firestore, Rules. Copy the lists from `firebase-config.js` into your own config file. Each TLLJ address needs a Google account with a verified email to sign in.

## Hiding a sponsor for a while (v37)

Open a sponsor and use **Hide for now**. Pick 1 week, 1 month, 3 months, until 4 January 2027, or any date, and add a reason. The sponsor leaves every list, the Scoreboard counts and its follow-ups until that day. Search still finds it, and **Hidden for now** (on Sponsors and Pipeline) lists everything hidden, with **Show now**. A week before the date, Today shows it under "Returning within a week". On the date it comes back with a card on Today: **Got it**, or **Hide 30 more days**.

## Sent mail log and push notifications (v38)

**Sent mail.** Activity, at the top, lists every email sent from the desk: date, recipient, subject and what happened. "Sent by the mailer" means the Apps Script mailer sent it. "Opened in your mail app" or "Opened in Gmail" means the desk opened the draft and you pressed Send there, so check your Sent folder to be sure.

**Push notifications (free Firebase plan).** Everyone with desk access opens Settings, then Notifications, then Turn on for this device. It needs two values in firebase-config.js: `messagingSenderId` (inside the firebase block) and `vapidKey` (the web push key from Firebase, Project settings, Cloud Messaging, Web configuration). The Apps Script in Code.gs does the sending: the daily digest, Fatimah's answers, and a draft waiting for Fatimah. On iPhone, add the desk to the Home Screen first. Run `testPush` in Apps Script to send yourself a test.

## Editor's approval (v39)

Every sponsor has an **Editor's approval** (Not yet reviewed, Approved, Approved with conditions, Not approved) and an **Editor's note**. Fatimah and Sade set them in the sponsor window or in the Sponsors table. Praise sees them and cannot change them. Pipeline cards show a pill once a sponsor is reviewed, and Pipeline has a filter for it.

## List update of 4 November 2026 (v40)

The first time Sade opens the desk after this update, it applies Fatimah's notes once: Big dream is now Aspirational, new sponsors are added (cars, aviation, hotels, a members' arts society, tourism boards, banks), Ikoyi Club, AnapJets and Coca-Cola are moved down with her reasons in the Editor's note, Mìlíkì is marked Declined, CANEX comes off the plan, and Afreximbank is hidden until 4 January 2027.

## v41: your own types, statuses and stages, and a clearer People page

- **Add your own contributor types.** On People, under "Types of contributor", type a name (for example Illustrator) and press Add type. It appears in the filter, in the Add a person form and in "Who for this brief?". You can also type a new type while adding or editing a person.
- **Add your own statuses for people.** Under "Statuses a person can have", add one (for example Looking for photographers). It appears as a filter button and in the person's Status list.
- **Add your own stages for assignments.** On Assignments, under "Stages a piece can be in", add one (for example Looking for a stylist). Two are ready for you: Looking for a writer and Looking for a photographer. Types of piece (Article, Photography, Video, Styling) can be added to in the same way.
- **Removing.** A type, status or stage you added shows a small x when nothing uses it.
- **People are grouped by where they are with us.** Active, Test sent, Contacted, New and your own statuses are open, with each person's types, strengths, email, phone and a short note visible. Keep on file and Declined are folded away until you open them. Searching or filtering opens everything.
- **Email button on each card** for anyone with an email address.
- Upload `index.html`, `sw.js` and `GUIDE.md`. Nothing changes in Firebase, Apps Script or the config.

## v43: CANEX is back, as a networking event

- **CANEX WKND 2026** (5 to 8 November, Lagos) is on Events again, with Fatimah and Praise registered for networking only. There is no press pass and no media-partnership pitch this time.
- **Afreximbank** stays hidden until 4 January 2027. Its notes now say the approach waits for January and to write down who they meet at CANEX.
- Runs once, the first time you open the desk as owner after the upload.

## v44: Met someone, call log, Documents, week in review, bigger buttons

- **Met someone.** The round button at the bottom right of every screen. Type a name, pick or type the company, write what they said, choose a follow-up and press Save. It saves the contact, notes the meeting on the sponsor and sets the follow-up. A company that is not on your list becomes a new lead. Hidden sponsors, such as Afreximbank, can still be picked. Fatimah can use it too; her follow-up becomes the sponsor's next step.
- **Log a call.** Open a sponsor and press Log a call, or use the button on Today. Pick how it went, say who you spoke to, set the next step and date, and Save. Said no marks the sponsor Declined.
- **Documents.** A new tab for everyone with desk access. Add files (up to 700 KB each); the sponsor is found from the first word of the file name. Files stay in your private database, never on the public website.
- **Week in review.** On Today, press Week in review (it is also a banner on Fridays). It writes a short message for Fatimah from what you logged and what is coming. Edit it, then press Email Fatimah or Copy.
- **Bigger buttons on Today.** Each next move has its own buttons: Done, Sent, Replied, No reply and Snooze for follow-ups; Open, Log a call and Snooze for sponsors. They are large on a phone.
- Upload `index.html`, `styles.css`, `sw.js` and `GUIDE.md`. Nothing changes in Firebase, Apps Script or the config.


## v45: what changed

- **Top right:** Approvals (highlighted), then icons for Search, Tilly, Ask Tilly and Documents. The three dots hold Suggestions, Export, Settings and Sign out. The moon or sun beside the title switches dark and light. Hover over anything to see what it is.
- **Tabs:** Documents and Ask Tilly left the tab bar. Scoreboard and Deals now sit inside Activity. Decisions is back in the tab bar and turns red for Fatimah when a decision waits for her.
- **Sponsors:** the list is compact. Status, Editor's approval and Editor's note come first. The coloured dot is the chance (press it to change). The small box is the score. The pencil opens all fields, the crossed eye hides a sponsor for a while, and the cross removes it. The Owner column is gone.
- **Sponsoring focus** moved from Today to the top of Sponsors. Under it sit 30 research questions. Add, edit, hide or delete any of them. Use the Short list for a quick pass. Tilly can draft an answer (check it and its source). When every question is answered, Generate proposal opens the Proposal Kit on that sponsor.
- **Roadmap:** week one starts Monday 2 November. Week labels follow the start date.
- **People:** Keep on file is open; Declined stays closed.
- **New sponsors:** Polo Avenue and L'Occitane were added once, with first-pass notes to check at the source.
- **Research a sponsor:** at the top of Sponsors, type a name and press Research and add. Tilly searches the web and fills the category, why it fits, who to approach, the proposal idea, next step, notes with sources, a score and chance guess, and the web-answerable research questions. Inside Sponsoring focus, Research this sponsor fills only the blank fields and answers of an existing sponsor. Check every source. Needs the Tilly key in Settings.
- **Friday summary:** on Fridays the desk opens it by itself when you open the app. Read it, edit it, then press Email Fatimah, or press Not this week. Nothing is sent automatically, because the desk cannot send while it is closed.
- **People (Contributors):** grouped by type. The first group is open. Keep on file and Declined are no longer default statuses; delete a person you will not use. A short list of questions for new contributors sits under the people.
- **Research questions:** 32 by default. Old sponsor-only research items now sit in the same list under "About this sponsor only".
- **Research a partner** (Partnerships mode) works like Research a sponsor.
- **Fatimah and Tilly:** with her own Gemini or Groq key in Settings, she can use Ask Tilly for questions and Research this sponsor (draft for Sade). Drafts reach you under Suggestions as "Research drafts to approve". Nothing changes until you press Apply.
- Plan steps and sponsor next steps dated before Monday 2 November moved to 2 November.
- **Calendar:** the calendar icon next to the search icon opens your Zoho calendars (read only). They also show on Today (today and tomorrow) and Events (next 14 days). Setup is Part C of SETUP-server.md.
- **Events:** past events leave the list and sit in a closed "Past events" block at the bottom.
- **Hidden sponsors:** listed once, at the bottom of Sponsors. They are not in Pipeline, Moved or Stuck.
- **Pipeline:** labelled Owner, When to approach and Stage, with a count and a + Sponsor button.
- **Today:** Next 7 days is closed until you open it.

## v46: Pitches inbox and calendar card
- **Pitches** (envelope icon, top right): everything that arrives at pitches@, sorted as writer pitch, press release or invitation, with any dates mentioned. Everyone with desk access can read it. Editors mark items Seen or Done.
- **Today** shows "New in pitches@" and a tidier Calendar card. Both open and close with one press.
- Only the sender, subject, date and a short preview are copied, never the whole email. Open pitches@ in Zoho to read and reply.
- Sorting and dates are by keyword, so check the original before acting on a date.

## v47: fixes
- Today no longer shows a sponsor's next step twice when the plan already has the same step. Sponsor next steps now have a tick box that clears only that step.
- Duplicate follow-ups are merged. Removing a sponsor now says exactly what goes with it.
- Suggested next steps can be folded. Contributors Today has overdue, due this week and pitches in collapsible cards.
- Contacts: Import contacts reads a .vcf or .csv from your email client, links matches to sponsors and keeps the rest in an Address book.
- Tell Tilly what happened lives in one place, the Tilly button at the top. The Ask page keeps check-in, brief and questions.
- Tilly's automatic daily event search now runs on Mondays only and asks first. Notes that already mention a sponsor or event skip the AI check.
- Sponsors: a "Research saved" strip lists every sponsor with saved answers. Answers save as you type, so you can switch sponsors without generating a proposal and resume later.

## v49

- Today's next moves now wrap in full instead of cutting off.
- Click anywhere in a date or time box to open the picker.
- Research saved sits at the bottom of Sponsors, above Hidden for now. Each sponsor has Send summary to Fatimah, which works whether or not every question is answered.
- Research this sponsor and Tilly: fill the blanks now ask first. Tilly only fills empty fields.
- Push to approvals appears on research summaries, generated proposals, the check-out report and assignments. It creates the item in Approvals and sends Fatimah the reminder.
- Contacts: wider name, email and phone boxes. Find with Tilly is now the sparkle icon with a hover label.
- Assignments: Type has Add a new type. Contributor lets you pick a person or add a new name.
- Documents gathers saved proposals, research, approvals and assignment links automatically.
- Partnerships and Contributors no longer show the sponsor activity report. The period choice stays.
- Contributors Today: People to contact is gone. Latest changes folds in instead.
- Every card can be folded with its chevron. The desk remembers it per browser.
- Balance no longer flags workload. The label Statuses a person can have is now Status.
- Calendar empty text now says when nothing has synced from Zoho yet.

## v50

- The Friday banner disappears once you send the week or press Not this week.
- Undo is an icon. Hover over it to see what it will undo.
- Add to plan removes the suggestion from Suggested next steps.
- Anything that sends an email now shows it first: you read it, edit it, then press Send. Cancel sends nothing.
- Restoring saved sponsor answers asks first.
- Send summary to Fatimah, on a sponsor in Research saved or on a partner, writes a short summary from everything the desk holds on that name. You edit it, then Send to Fatimah or Save in Approvals only.
- When Fatimah approves a sponsor or partner idea, a card on Today offers Set up next steps. Tilly proposes your steps and the decisions Fatimah needs to take. You tick, edit, then add. Her decisions land on her Decisions tab.
- Push to Praise lists only what moved: sponsor and partner status, new contacts, events, contributors, decisions answered, then next steps in full.
- Partnerships has its own Roadmap. Steps that belong to a partner no longer show in the sponsor Roadmap.
- Search takes you to the page of the result.
- Pitches has a My inbox switch for the owner. It needs Part E in SETUP-server.md.

## v51

- **Pitch labels.** Email addresses and links are ignored when the desk decides whether a message is a pitch, an invitation or a press release. Only the words count, so pitches@ and welcome@ no longer trigger a label.
- **Hold before sending.** In the review window, choose No hold, 30 seconds, 1 minute or 5 minutes. After Send, a bar at the bottom counts down with Undo and Send now. Closing the page during a hold sends nothing; on return the bar offers Send now or Discard.
- **Contacts from your inbox.** On the Pitches page, "Add these senders as contacts" lists the people who wrote in (automatic and newsletter addresses left out). Matches go to their sponsor, the rest to the Address book. "Import contacts from a file" is on the same page. Nothing saves until you press Add.
- **Questions that fit the sponsor.** In a sponsor’s Research questions, "Add questions that fit this sponsor" offers six questions for a foundation, fund, airline, tourism board, club or brand, and asks first. "Hide the standard questions" removes the general list for that sponsor only; it can be shown again.
- **Researched sponsors.** On first load the desk asks before adding: The Osahon Okunbo Foundation, Helios Sports and Entertainment Group, Africa Finance Corporation, Isimi Lagos Polo Club, Ethiopian Airlines, Kenya Airways, RwandAir. It also adds sourced notes to L’Occitane, Mbari Kola, Air France Nigeria and Visit Rwanda. Gaps are written as "Not found".

## v52

- **Sent means sent.** A draft sent from the desk is marked Sent, and its sponsor’s log gets an Email sent line.
- **Contacts and inboxes.** The import buttons are now at the bottom of the email page. When you add senders or import a file, each person has an inbox choice: Pitches, My inbox, Both, or none.
- **Your own question types.** "Add questions that fit this sponsor" opens a window where you choose a type, edit the questions, add a new type with the words that identify it, save it, or remove it.
- **Sponsor pulse on Today.** Replies from your inbox matched to a sponsor (log them with one tap, asking first), meetings that just happened (log the outcome, with an optional follow-up), meetings coming up (a one-page brief), sponsors going cold (no contact logged for 10 days), and the count to 14 December.
- **Invitations.** An invitation with a date in the message has an Add to Events button.
- **Research.** Polo Avenue, emPLE, Zenith, Isimi and four priority sponsors (Leadway, Afreximbank, Coscharis, Lagos State Ministry) have sourced notes added, with gaps marked.
- **Full notes.** Pipeline cards no longer cut a note or next step short.

## v53

- **Link a contact to a sponsor, partner or writer.** In Contacts, every person in the Address book has one choice list: Sponsors, Partners, Writers and contributors, or Add new. Choosing "New sponsor…", "New partner…" or "New writer or contributor…" asks for a name, creates it, and links the contact, so you do not leave the screen.
- **Same choice in the import window.** Each person being imported can be linked to any of the three, or added as new. A new one is named from the company if the file has one, otherwise from the person.
- **Linked people stay visible.** Contacts linked to a partner or writer stay in the Address book with a tag showing where they are linked.

## v54

- **Partner and writer pages show their contacts.** Open a partner or a writer: "Contacts and emails" lists the people linked to them (Edit or Unlink), lets you link a saved contact, and shows their five most recent emails.
- **Link a sender from the inbox.** Every email in Pitches and My inbox has "Link sender": choose a sponsor, partner or writer, or add a new one. The sender is saved as a contact if they were not one already.
- **Replies match partners and writers too.** On Today, "Sponsor pulse" now offers to log a reply for a partner or writer as well as a sponsor, asking first. For partners and writers the reply is added as a dated line in their notes.
