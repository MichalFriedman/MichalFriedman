# Hellscore rehearsal reminder — Hebrew message + shortcut setup

Fires from the `Saturday WhatsApp` automation (Saturdays 20:00) into the
**Hellscore updates** WhatsApp group.

## Message — version A (fixed text)

Use this if the rehearsal is always at the same day/time/place.

```
היי הלסקוראים 🖤
תזכורת לחזרה הקרובה — מחר, יום ראשון, בשעה 19:00 ב[מקום].
מגיעים בזמן, עם התווים ועם בקבוק מים.
נתראה! 🎶
```

## Message — version B (date fills itself in)

Use this if you want the actual date to appear, so the message stays right even
if you change the automation's day.

Build the shortcut with these four actions, in order:

1. **Date** → set to *Current Date*
2. **Adjust Date** → *Add* `1` *Days* to the Date from step 1
3. **Format Date** → input = Adjusted Date, Date Format = *Custom*,
   format string `EEEE, d.M`
   (with the iPhone's language set to Hebrew this renders as `יום ראשון, 24.8`)
4. **Send Message** (WhatsApp) → paste the text below into the Message field and
   drop the **Formatted Date** variable where marked

```
היי הלסקוראים 🖤
תזכורת לחזרה הקרובה — [Formatted Date] בשעה 19:00 ב[מקום].
מגיעים בזמן, עם התווים ועם בקבוק מים.
נתראה! 🎶
```

Change the `1` in step 2 to match how many days after Saturday the rehearsal
falls (1 = Sunday, 2 = Monday, and so on).

## Pointing it at the group

In the **Send Message** action, tap **Recipient** and search `Hellscore`. Group
chats show up in the picker alongside contacts.

If the group doesn't appear: open the Hellscore updates group in WhatsApp, send
or read a message, then force-quit and reopen Shortcuts. iOS only offers
conversations WhatsApp has recently surfaced to the system.

Then turn **Show When Run** off on both the Recipient and Message fields, as in
`whatsapp-saturday-automation.md`.

## Typing Hebrew into Shortcuts

Copy the message block above and paste it into the Message field rather than
retyping — pasting keeps the emoji and the line breaks intact, and avoids
fighting the RTL cursor while editing around the `[מקום]` placeholder.
