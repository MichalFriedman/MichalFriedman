# Hellscore rehearsal reminder — Hebrew message + shortcut setup

Fires from the `Saturday WhatsApp` automation (Saturdays 20:00) into the
**Hellscore updates** WhatsApp group, about the **Wednesday** rehearsal.
The date fills itself in each week.

## Build the shortcut

Four actions, in this order:

| # | Action | Settings |
|---|--------|----------|
| 1 | **Date** | Current Date |
| 2 | **Adjust Date** | *Add* `4` *Days* to the Date from step 1 — Saturday + 4 = Wednesday |
| 3 | **Format Date** | Input: Adjusted Date · Date Format: **Custom** · format string `EEEE, d.M` |
| 4 | **Send Message** (WhatsApp) | Recipient: *Hellscore updates* · Message: the text below |

With the iPhone's language set to Hebrew, step 3 renders as `יום רביעי, 26.8`.

## The message

Paste this into the Message field, then delete `[Formatted Date]` and drop the
**Formatted Date** variable in its place:

```
היי הלסקוראים 🖤
תזכורת לחזרה הקרובה — ב[Formatted Date] בשעה [שעה], ב[מקום].
מגיעים בזמן, עם התווים ועם בקבוק מים.
נתראה! 🎶
```

Fill in `[שעה]` and `[מקום]` with the rehearsal time and location.

Copy-paste rather than retyping — pasting keeps the emoji and line breaks
intact and saves you fighting the RTL cursor around the placeholders.

## Pointing it at the group

In the **Send Message** action, tap **Recipient** and search `Hellscore`. Group
chats appear in the picker alongside contacts.

If the group doesn't show up: open the Hellscore updates group in WhatsApp, send
or read a message there, then force-quit and reopen Shortcuts. iOS only offers
conversations WhatsApp has recently surfaced to the system.

Then turn **Show When Run** off on both the Recipient and Message fields, per
`whatsapp-saturday-automation.md`.

## Changing the rehearsal day later

Edit the number in step 2 — it's days after Saturday: `1` Sunday, `2` Monday,
`3` Tuesday, `4` Wednesday, `5` Thursday. The weekday name in the message comes
from the date itself, so nothing else needs touching.
