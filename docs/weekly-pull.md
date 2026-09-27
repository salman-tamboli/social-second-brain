# Weekly Content Pull — Workflow

**What it does, in plain words:** every Sunday morning, this job looks at what
you saved on Facebook and Instagram since the last run, turns each new save
into a short distilled note, files it in the 📥 Inbox database, and emails
you a summary.

- **Schedule:** every Sunday ~10:00 AM IST
- **Cap:** max **30 new items per run**, newest first (Facebook + Instagram
  combined). It processes only *unprocessed* saves — it never re-adds old
  ones just to reach 30.
- **Email:** sent to `your-email@example.com` with the exact subject
  `2nd brain content dump done`.

> In the original build this ran as a scheduled task on a personal AI
> assistant, using its built-in connectors for Facebook, Instagram, Notion
> and Gmail. The logic below is tool-agnostic: any setup that can (1) list
> saved items, (2) write to a Notion database, and (3) send an email can run
> it. Tool names from the original build are noted where the logic depends
> on their behavior.

---

## 1. The workflow, step by step

### Step 0 — Load the dedupe tracker
Read the tracker file (see section 5). It lists the IDs/URLs of every item
already processed in earlier runs. Anything on that list is skipped.

### Step 1 — Fetch new Facebook saves
- List saved items, newest first.
- Filter out anything already in the tracker.
- Take up to 30 minus whatever Instagram contributes (30 total across both).

### Step 2 — Fetch new Instagram saves
- List saved posts, newest first.
- Filter out anything already in the tracker.
- Fill the remaining slots up to the 30-item total.

### Step 3 — Distill each item into a note
For every new item, produce:
- **A distilled title** — short, descriptive, in your own words. Never paste
  the full caption or transcript.
- **3–8 bullet points** capturing the useful content (tips, steps, key
  facts, links mentioned).

**Content rules:**
- If the item is **deleted/unavailable** (e.g. a 404): create a stub note
  with the title you can infer and a one-line "unavailable" body. Never
  invent details.
- If the platform returns **no transcript or readable content**: title the
  note normally and append **"— rewatch to extract"** so the owner knows to
  open it manually.
- If the item makes **viral or factual claims you can't verify**: keep the
  note but mark the claim **(unverified)** / add a caution line. Never
  present an unverified claim as fact.
- **Summarize and synthesize.** Never paste full captions or transcripts.

### Step 4 — File each note in the 📥 Inbox database
Every row gets all five columns (see `vault-schema.md`):
- `Name` = distilled title
- `Platform` = `Facebook` or `Instagram`
- `Category` = exactly one of `Tech`, `AI`, `Cooking`, `Kids Learning`,
  `Health`, `Business`, `Career`, `Music`, `Other`
- `Date Extracted` = **this run's date** (not the post's date — save
  timestamps aren't exposed by the platforms, so the extraction date is the
  honest label)
- `Source` = the item's URL

### Step 5 — Update the dedupe tracker
Append every newly processed item's ID/URL to the tracker file so future
runs skip them.

### Step 6 — Email the confirmation
Send one email to `your-email@example.com`:
- **Subject (exact):** `2nd brain content dump done`
- **Body:**
  - Run date
  - Total notes added
  - Facebook/Instagram split
  - Count per category

Example body:

```text
Run date: 2026-10-04
Notes added: 12 (Facebook: 7, Instagram: 5)

By category:
- Tech: 4
- AI: 3
- Cooking: 2
- Business: 2
- Health: 1
```

### Step 7 — Report back
Write a short summary of the run (notes added, split, any stubs or
"rewatch to extract" flags). If a source failed, say which one and what was
skipped — transparent reporting of partial work.

---

## 2. Hard rules (these never bend)

1. **Never modify, move, archive, or delete existing notes.** The job only
   *adds* rows.
2. **Never delete anything without the owner's explicit confirmation** for
   the specific item(s). A general "clean up" instruction is not permission.
3. **Never fabricate** missing content. Unavailable → stub. No transcript →
   "rewatch to extract". Unverifiable claim → marked as such.
4. If the run produces **zero** new items, the email still goes out saying
   zero were added.

---

## 3. The original instruction block (sanitized)

Below is the full instruction text used for the scheduled task in the
original build, with personal values replaced by placeholders. It can serve
as a spec for reimplementation:

```text
Weekly second-brain content pull. Every Sunday ~10:00 AM IST. Fully
autonomous run — the owner does nothing.

WORKFLOW
0. Read the dedupe tracker at hidden_files/processed_reels.json
   ({"processed": ["<id-or-url>", ...]}). Skip anything already listed.
1. List Facebook saved items, newest first; keep only unprocessed ones.
2. List Instagram saved posts, newest first; keep only unprocessed ones.
3. Process up to 30 TOTAL new items across both platforms, newest first.
   Never re-add old items to reach 30.
4. For each item: distill into a title + 3-8 bullets. Summarize, never paste
   full captions/transcripts. Deleted item -> one-line "unavailable" stub.
   No readable content -> title ends with "-- rewatch to extract".
   Unverifiable viral claim -> mark (unverified), never state as fact.
5. Add each note as a row in the Inbox database (YOUR_INBOX_DATABASE_ID):
   Name, Platform (Facebook/Instagram), Category (one of Tech, AI, Cooking,
   Kids Learning, Health, Business, Career, Music, Other), Date Extracted
   (this run's date), Source (item URL).
6. Append all newly processed IDs/URLs to the tracker file.
7. Email your-email@example.com, subject exactly "2nd brain content dump
   done", body: run date, total added, FB/IG split, per-category counts.

HARD RULES
- Only ADD rows. Never modify, move, archive, or delete existing notes.
- Never delete anything without the owner's explicit confirmation of the
  specific item(s).
- Report partial/unverified work transparently; never substitute or invent.
```

---

## 4. What the job needs from each connected service

| Service | Needs to be able to… |
|---|---|
| Facebook | List saved items (newest first) with IDs/URLs; fetch per-item details/transcript where available |
| Instagram | List saved posts (newest first) with IDs/URLs; fetch per-item caption/media info where available |
| Notion | Append rows to the Inbox database with the five columns |
| Email | Send one summary email per run |
| File storage | Read/write the small JSON tracker file |

If any service is disconnected or a login expires, the run must **report
the failure** (which service, what was skipped) rather than silently
pretending it succeeded.
