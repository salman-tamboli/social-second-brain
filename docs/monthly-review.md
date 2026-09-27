# Monthly Stale Review — Workflow

**What it does, in plain words:** on the 1st of every month, this job looks
through the whole vault and puts together a tidy suggestion list of notes
that *might* need attention — grouped by topic — then asks the owner what to
do about each group.

- **Schedule:** 1st of every month ~10:00 AM IST
- **Delivered to:** the owner's main chat (a message, not an email)
- **It never changes anything.** It only suggests. Deletion or archiving
  happens only for items the owner explicitly approves, one by one.

---

## 1. The workflow, step by step

### Step 1 — Scan the vault
Read every row in the 📥 Inbox database (all columns), plus the topic pages
under Areas and the Archive page.

### Step 2 — Flag candidates
A note becomes a *candidate* if any of these are true:

| Signal | Meaning |
|---|---|
| **Untouched 3+ months** | Date Extracted is older than 3 months and the note was never filed into a topic area |
| **Thin note** | Title ends with "— rewatch to extract", or the body is an "unavailable" stub |
| **Dead source** | The Source URL no longer opens (deleted post, 404) |
| **Near-duplicate** | Two or more notes covering essentially the same content |

### Step 3 — Group by topic
Organize the candidates under their Category headings (Tech, AI, Cooking,
…), so the owner can decide per topic instead of item-by-item if they want.

### Step 4 — Present the suggestions
Send the owner a message like:

```text
Monthly vault review — 2026-10-01

I found 6 notes that might need attention. Nothing has been changed.
Tell me which ones to delete/archive, or say "leave them all".

TECH (2)
- "Python in 60 seconds — rewatch to extract" (saved 2026-09-27, thin note)
- "Super Grok free trick — rewatch to extract" (saved 2026-09-27, thin note)

COOKING (1)
- "Dosa batter recipe" — source link is dead (404)

AI (3)
- "AWS Bedrock explained" and "Bedrock AI overview" look like near-duplicates
- ...
```

### Step 5 — Wait for the owner
Do nothing further until the owner replies. When they approve specific
items, act **only** on those items.

---

## 2. Hard rules (these never bend)

1. **No deletion, archival, or modification happens during the review.**
   The review's only output is the suggestion message.
2. Later cleanup acts **only** on items the owner explicitly approved, by
   name. "Clean up the thin ones" is not approval — the owner must confirm
   the specific items (or explicitly say "all items in group X").
3. If there are **no candidates**, say so briefly ("Vault looks healthy —
   no stale candidates this month.") instead of inventing some.

---

## 3. The original instruction block (sanitized)

```text
Monthly second-brain stale review. 1st of every month ~10:00 AM IST.
Delivered to the owner's main chat.

WORKFLOW
1. Read all rows in the Inbox database (YOUR_INBOX_DATABASE_ID): Name,
   Platform, Category, Date Extracted, Source.
2. Flag candidates:
   - Untouched 3+ months (old Date Extracted, never filed into an Area)
   - Thin notes ("-- rewatch to extract" titles, "unavailable" stubs)
   - Dead sources (Source URL returns 404 / deleted)
   - Near-duplicates (same content, multiple notes)
3. Group candidates by Category.
4. Message the owner: grouped candidate list with a one-line reason per
   item, plus the explicit statement that nothing was changed. Ask which
   items (if any) to delete or archive.

HARD RULES
- The review NEVER deletes, archives, or modifies anything.
- Later cleanup touches ONLY items the owner explicitly approved by name.
- A general "clean up" instruction is not approval for specific items.
- If no candidates exist, report "vault healthy" briefly.
```
