# Hellscore rehearsal reminder — driven by the Google Calendar

Fires from the `Saturday WhatsApp` automation (Saturdays 20:00) into the
**Hellscore updates** WhatsApp group. The date, time and location are read from
the subscribed **Hellscore** Google Calendar, so nothing is hard-coded.

## Prerequisite — get the calendar into iOS Calendar

Shortcuts can only see calendars that appear in Apple's Calendar app.

1. **Settings → Apps → Calendar → Accounts → Gmail** — make sure **Calendars**
   is on.
2. Subscribed calendars (ones shared with you, like Hellscore) are excluded
   from iOS sync by default. Open <https://calendar.google.com/calendar/syncselect>
   in Safari, tick **Hellscore**, and Save.
3. Open the Calendar app → **Calendars** → confirm **Hellscore** is listed and
   checked, and that you can see the חזרה events on it.

## What's on that calendar

It carries more than rehearsals — recording sessions (`הקלטות ...`) and classes
(`פיתוח שמיעה`) sit alongside them. The rehearsals are the events whose titles
start with `חזרה` / `חזרת`:

| Title | Pattern |
|-------|---------|
| `חזרה Hellscore` | Wednesdays 20:00–22:30, HaTeiva |
| `חזרת אנסמבל` | Wednesdays 19:30–22:30, HaTeiva |

So the filter matches on `חזר` — the shared stem — which catches both spellings
and skips the recordings and classes.

## Build the shortcut

| # | Action | Settings |
|---|--------|----------|
| 1 | **Find Calendar Events** | Filter: **Calendar** `is` `Hellscore` · **Title** `contains` `חזר` · **Start Date** `is in the next` `7` `days` · Sort by **Start Date**, **Ascending**, **Limit** `1` |
| 2 | **If** | Input: **Calendar Events** · condition `has any value` |
| 3 | **Get Details of Calendar Events** | Detail: **Start Date** |
| 4 | **Format Date** | Input: that Start Date · Date Format **Custom** · `EEEE, d.M` — rename this variable `תאריך` |
| 5 | **Format Date** | Input: the same Start Date · Date Format **None** · Time Format **Short** — rename this variable `שעה` |
| 6 | **Get Details of Calendar Events** | Detail: **Location** — rename this variable `מקום` |
| 7 | **Text** | The message below |
| 8 | **Send Message** (WhatsApp) | Recipient: *Hellscore updates* · Message: the Text from step 7 |

Actions 3–8 go **inside** the If block, so a week with no rehearsal on the
calendar sends nothing at all instead of an empty message.

To reuse one Start Date across steps 4 and 5, tap the variable in step 5 and
pick **Start Date** from the Calendar Events magic variable — no need for a
second Get Details action.

## The message

```
היי הלסקוראים 🖤
תזכורת לחזרה הקרובה — ב[תאריך] בשעה [שעה], ב[מקום].
מגיעים בזמן, עם התווים ועם בקבוק מים.
נתראה! 🎶
```

Replace each `[...]` with the matching variable from the table. With the phone's
language set to Hebrew, a real send reads:

> תזכורת לחזרה הקרובה — ביום רביעי, 2.9 בשעה 19:30, ב-HaTeiva.

Some events have no **Location** set. If that bothers you, wrap the `ב[מקום]`
part in a second **If** on `מקום` `has any value`, or just drop the location
from the text.

## Optional — check every evening instead of only Saturdays

A single Saturday reminder assumes the rehearsal is always mid-week. To make it
follow the calendar completely, change the automation to run **daily** at 20:00
and change the step 1 filter to **Start Date** `is` `tomorrow`. It then messages
the group the evening before any rehearsal, whichever day it lands on, and stays
silent otherwise.
