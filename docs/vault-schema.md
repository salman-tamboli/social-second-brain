# Notion Vault Schema

This doc describes the exact structure of the "Second Brain" Notion workspace.
Follow it top-to-bottom to recreate the vault by hand (all clicking, no code).

> Placeholders like `YOUR_...` must be replaced with your own values.
> Counts below (e.g. "21 rows") describe the vault at the time of writing and
> are just an example — yours will start empty.

---

## 1. Root page

- **Title:** `Second Brain`
- **Type:** Notion page (this is the front door of the vault)

### Children of the root page, in order

1. **📥 Inbox** — a database (see section 2). This is where every distilled
   note lands.
2. **Areas** — a heading (or toggle) containing one page per topic:
   - Cooking & Food
   - Health
   - Tech & AI
   - Career & Learning
   - Business Ideas
3. **Archive** — a page that starts empty. Notes the owner approves for
   archiving go here. (Nothing is moved here automatically.)

---

## 2. The 📥 Inbox database

**Type:** Notion table database (full page).

### Columns

| Column name | Type | Allowed values / format | Required? |
|---|---|---|---|
| Name | Title | A short, distilled title of the note (not the raw caption) | Yes |
| Platform | Select | `Facebook`, `Instagram` | Yes |
| Category | Select | `Tech`, `AI`, `Cooking`, `Kids Learning`, `Health`, `Business`, `Career`, `Music`, `Other` | Yes — exactly one |
| Date Extracted | Date | The date the note was created (the run date, not the post date) | Yes |
| Source | URL | Link back to the original reel/post | Yes |

### Views

- **Default table view** — all rows, sorted newest first by Date Extracted.
- **By Platform** — a **board view** grouped by the `Platform` column, so you
  get one column of Facebook notes and one of Instagram notes.

### Example rows (what good entries look like)

| Name | Platform | Category | Date Extracted | Source |
|---|---|---|---|---|
| Make perfect dosa batter at home | Instagram | Cooking | 2026-09-27 | https://www.instagram.com/reel/xxxxx/ |
| Python in 60 seconds — rewatch to extract | Facebook | Tech | 2026-09-27 | https://www.facebook.com/reel/xxxxx/ |
| AWS Bedrock explained (claims unverified) | Instagram | AI | 2026-09-27 | https://www.instagram.com/reel/xxxxx/ |

### Special conventions used in note titles

- If a reel/post was **deleted or unavailable**, the note title says what it
  was about and the body is a one-line "unavailable" stub — details are never
  invented.
- If the platform provided **no transcript or readable content**, the title
  ends with **"— rewatch to extract"** so the owner knows to open it manually.
- If a note repeats a **viral claim that couldn't be verified**, the title or
  body carries an **"(unverified)"** caution instead of stating it as fact.

---

## 3. How to recreate this in Notion (click-by-click)

1. In Notion, create a new page titled **Second Brain**.
2. Inside it, type `/table` and pick **Table view – Full page**. Name it
   **📥 Inbox**.
3. Add the columns from the table in section 2:
   - `Platform` → **Select** property, options: `Facebook`, `Instagram`
   - `Category` → **Select** property, options: `Tech`, `AI`, `Cooking`,
     `Kids Learning`, `Health`, `Business`, `Career`, `Music`, `Other`
   - `Date Extracted` → **Date** property
   - `Source` → **URL** property
4. Add a view: click the view tabs **+** → **Board** → name it **By Platform**
   → **Group by:** `Platform`.
5. Back on the Second Brain page, below the database, add a heading
   **Areas** and create the five topic pages under it.
6. Add a page called **Archive** at the bottom. Leave it empty.

Done — the vault is ready to receive notes.
