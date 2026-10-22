# Doing-App (Prototype)

A personal to-do board in the style of Jira, packed into **one single HTML file**. No installation, no server, no account – open the file in Microsoft Edge and start working. Everything is saved automatically.

| File | Language |
|---|---|
| `Doing-App_Prototype.html` | German UI |
| `Doing-App_Prototype_en.html` | English UI (separate data – the two versions don't mix) |

> Design inspired by [sanidhyy/jira-clone](https://github.com/sanidhyy/jira-clone).

---

## Quick start

1. Open the file in **Microsoft Edge** (Chrome / Brave / Firefox work too – Firefox without auto-sync, see Data safety).
2. Go to **the menu button (bottom left) > Check data safety** and set up **auto-sync to a file** – ideally in your OneDrive folder.
3. Delete the example tickets and add your own with **+ New** (key `C`) or **Paste list** (key `L`).

---

## Features

### My tasks – Board, List, Calendar
- **Board:** Kanban with *Backlog > To Do > In Progress > Waiting > Done*. *Paused* and *Cancelled* can be shown on demand. Drag & drop, quick-add per column, filters by goal, importance, type, label and meeting.
- **List:** an Excel-like table.
  - per-column filters with checkboxes, sorting, show/hide columns
  - inline editing
  - columns for week number, waiting for, follow-up, source, agenda and cancel reason
  - CSV export of the current view
- **Calendar:** month view with soft and hard deadlines, follow-up dates, meeting dates with their open agenda items, planned recurring tasks and calendar-week numbers.

### Tickets
- Title, description, **sub-tasks**, updates log and labels. Sub-tasks can be expanded and ticked off **right on the card**. There are deliberately only two levels: ticket > sub-task.
- **Importance:** *Must* / *Worth it* / *Nice-to-have*.
- **Two dates:** *target* (soft) and *deadline* (hard). Cards turn yellow or red when they are due. The deadline can also be entered as a **week number** (e.g. `43` > Friday of that week).
- **Waiting:** who you are waiting for, plus a follow-up date. The card shows "waiting for X · for 3 days", and turns purple once the follow-up is due.
- **Paused** (with a resume date) and **Cancelled** (asks for the reason).
- **Source:** which meeting the task came from, the date, and a link (e.g. to the OneNote page).
- **On agenda for:** puts the ticket on a meeting's agenda.
- **Recurrence** with a fixed rhythm:

  | Rhythm | Example |
  |---|---|
  | weekly | every week |
  | every 2 weeks | every other week |
  | specific weekdays | 2× per week: Mon + Thu |
  | monthly (same date) | every 15th |
  | monthly, n-th weekday | 1st Monday of the month |
  | monthly, last working day | last working day of the month |
  | monthly, n-th working day | 3rd working day of the month |
  | quarterly | every 3 months |

  Per series you can set the buffer between the soft and the hard deadline, and how many days in advance the ticket appears. Public holidays are not taken into account.
- **Private** flag (see Show mode).

### Stakeholders, sub-task deadlines, wins
- **Stakeholders** per ticket (comma-separated). Shown on the card, as a list column with filter, and suggested from earlier entries.
- **Sub-task due dates:** every sub-task can have its own date. Overdue open sub-tasks turn the card red; the card shows the next due date next to the sub-task counter.
- **Contribution & impact** per ticket: *what I did*, *role* (Lead / Contributor / Support) and *impact*. **Menu > Wins as CSV (brag sheet)** exports all done tickets with date, project/goal, what you did, role, importance, impact, stakeholders and source – ready for performance reviews, salary talks or your CV.

### Features on/off
**Menu > Features on/off** hides stakeholders, sub-task due dates, contribution & impact or the timeline view. This only affects the display: data you entered stays saved and reappears as soon as you switch the feature back on. Turned-off sub-task dates also stop turning cards red. The setting is saved with your data (and in backups).

### Timeline (flow view)
**📈 Timeline** in a ticket or on a goal card opens a visual history:
- **Ticket:** flow chain of all status phases with durations (e.g. *To Do 3 d → In progress 3 d → Waiting 4 d, waiting for X → …*), a "where did the time go?" bar, a timeline with sub-task completions, sub-task due dates, updates, target/deadline and today, plus the people involved and the impact text.
- **Goal:** Gantt chart of all tickets (click a row to open it), time split across all tickets, and a **Venn diagram** of the top-3 stakeholders showing how many tickets they share.

Phases are rebuilt from the automatic status entries in the updates log. Tickets created before this existed show an approximate flow.

### Paste list (action items > tickets)
Paste action items, e.g. copied from OneNote, and each line becomes a ticket. Recognised automatically:
- **Indented lines** become sub-tasks of the line above.
- `#label` sets a label.
- `KW43` / `wk43` or `24.10.` sets the deadline.
- `!` or `(Pflicht)` / `(must)` sets the importance to *Must*.
- `@Name` sets the status *Waiting* for that name.
- `+Name` adds a stakeholder.
- An indented line with `KW43` or `24.10.` sets that **sub-task's** due date.
- Lines ending in `:` count as headings and are skipped.

Status, goal, source meeting and date, agenda, labels and the private flag can be set once for all tickets in the list. A live preview shows the result before anything is created.

### Meetings
- Meetings have a rhythm and a next date. Past dates move forward automatically.
- The **agenda** lists all open tickets that are on it. Tick items off with **discussed**, or copy the agenda as text.
- **Sync prep** builds a ready-made text for syncs with your manager, which you can edit, then copy or download as a file:
  - agenda items
  - done since the last meeting
  - in progress
  - blockers you are waiting on
  - overdue items
  - what is coming up
  - cancelled items

  Private tickets are always excluded.
- Each meeting also lists the open tasks that originally came from it.

### Weekly review
Pick a week to get a text with *Done*, *In progress*, *Waiting for*, *Overdue*, *Next week* and optionally *Cancelled* and *Paused*. You can switch sections and options on and off, edit the text, and copy it straight into Teams or Outlook.

### Goals
Goals group several tickets and show a progress bar; cancelled tickets don't count towards it. The Goals page also lists all recurring tasks, which you can pause, change or delete there. Clicking a goal in the sidebar filters the board.

### Notes & AI prompts
- **Notes:** simple free-form notes. Meeting notes are meant to stay in OneNote.
- **Prompts:** AI templates that work in three steps:
  1. Pick a template. The included ones turn notes into tickets, turn a meeting into tasks plus a summary, plan the week, or clean up a note.
  2. Insert your notes and copy the finished prompt.
  3. Paste the AI's answer and import it. The JSON is extracted automatically. Existing tickets are updated when the answer contains their `key`.

### Private / Show mode
The toggle sits at the bottom of the sidebar. **Show mode** hides private tickets everywhere, plus notes, prompts and the update logs, so you can share your screen with your manager. This is a visual privacy screen, not encryption.

---

## Data safety

| Layer | What it does |
|---|---|
| **Browser storage** | Saved automatically ~0.3 s after every change (Edge profile, `localStorage`). |
| **Auto-sync file** | Menu > *Auto-sync to new file*: every change is also written to a JSON file of your choice (Edge/Chrome only). After a browser restart, click **Resume** once. |
| **Backup** | Menu > *Export backup (JSON)* – a full backup that can be restored. *All tickets as CSV* is an Excel export for reading only. |

**Menu > Check data safety** runs these checks:
- whether the browser can save
- whether the storage is protected from automatic clean-up
- auto-sync status and last write
- date of the last backup
- a **restart test**: start it, close all Edge windows, reopen the file, and the check reports whether the data survived
- a reminder to check `edge://settings/clearBrowsingDataOnClose`; *Cookies and other site data* must be **off**

A banner appears as long as neither auto-sync nor a recent backup exists.

**Firefox:** everything works except the auto-sync file (Firefox doesn't support the File System Access API). Firefox stores data **per file path** – renaming or moving the file shows an empty board. Export a backup first and import it into the renamed file. Edge/Chrome are not affected.

**Older backups** can be imported as they are: new fields (stakeholders, sub-task dates, impact) simply start empty.

Browser data is lost if site data is cleared, if "clear on close" is enabled (common on company PCs), in InPrivate windows, or when you switch PC or browser. Use the auto-sync file and backups for that.

---

## Keyboard shortcuts
| Key | Action |
|---|---|
| `C` | New ticket |
| `L` | Paste list |
| `N` | New note (private mode) |
| `/` | Search board |
| `Esc` | Close dialog / popup |
| `Ctrl` + `Enter` | Save update in a ticket |

---

## Limitations
- Single user, single device; no real-time sync between devices.
- No notifications while the page is closed. Recurring tickets are created the next time it is opened.
- Recurrence ignores public holidays.
- Drag & drop doesn't work on touch devices; use the status field instead.

## Tech
Plain HTML, CSS and vanilla JavaScript in one file, with no build step and no dependencies. Data is stored in `localStorage`. The file sync uses the File System Access API, with the file handle kept in IndexedDB.
