# Saturday 20:00 WhatsApp automation (iPhone)

Sends a WhatsApp message every Saturday evening at 20:00 using the built-in
**Shortcuts** app. No third-party apps, no subscriptions.

## Part 1 — Build the shortcut

1. Open **Shortcuts** → **Shortcuts** tab → **+** (top right).
2. Tap **Add Action**, search for **WhatsApp**, and pick **Send Message**.
   (If WhatsApp doesn't appear, open WhatsApp once and send any message first —
   iOS only exposes the action after the app has been used.)
3. Tap the **Recipient** field and choose the contact or group.
4. Tap the **Message** field and type the text to send.
5. Long-press (or tap the ⓘ next to) each blue field and turn **Show When Run**
   **OFF** for both Recipient and Message. This is the toggle that removes the
   confirmation step.
6. Rename the shortcut (top of screen) to `Saturday WhatsApp` → **Done**.
7. **Test it now**: tap the shortcut to run it. Confirm the message actually
   arrives without you tapping anything. See "If it still asks you to tap" below.

## Part 2 — Schedule it for Saturdays at 20:00

1. Shortcuts → **Automation** tab → **+**.
2. Choose **Time of Day**.
3. Set the time to **20:00**, repeat **Weekly**, and select **Saturday** only.
4. Tap **Next** → choose the `Saturday WhatsApp` shortcut.
5. Set **Run Immediately** (not "Run After Confirmation") — this is what makes
   it hands-off.
6. Optionally turn **Notify When Run** off so it fires silently.
7. **Done**.

## If it still asks you to tap send

Apple deliberately restricts one app from driving another, and whether
WhatsApp's Send Message action posts in the background or opens the chat
pre-filled has changed between WhatsApp releases. If step 7 of Part 1 opens
WhatsApp instead of sending:

- **Option A — one-tap version.** Keep the automation exactly as built. At 20:00
  the chat opens with the message already typed; you press the send arrow. Two
  seconds of effort, and it never breaks.
- **Option B — truly hands-off, off-device.** Send from a service instead of the
  phone: WhatsApp Business Platform (Cloud API) or a wrapper like Twilio, driven
  by a weekly cron job. Fires with no device involved, but it sends from a
  WhatsApp Business number, needs an approved message template for the recipient,
  and costs per message. Only worth it for something like a business reminder.

## Things that can make the automation skip

- Phone powered off at 20:00 — it won't fire retroactively.
- **Low Power Mode** can delay background automations by minutes.
- A **Focus** mode doesn't block the automation, but can hide its notification.
- Changing the shortcut's name doesn't break the automation; deleting and
  recreating the shortcut does — re-pick it in the automation.

## Message and recipient

Fill these in at steps 3 and 4:

- Recipient: _<contact or group>_
- Message: _<text>_

If you want the text to vary week to week, insert a **Text** action before the
WhatsApp action and use variables such as **Current Date** (formatted) inside it,
then pass that Text as the Message.
