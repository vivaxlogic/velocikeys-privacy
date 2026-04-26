# VelociKeys AI — Privacy Policy

**Last updated: 2026-04-26**

VelociKeys AI ("the Keyboard", "we") is a privacy-first input method for
Android. This document describes exactly what data the Keyboard handles,
where it goes, and what control you have.

The TL;DR: **we do not collect, transmit, sell, or share what you type.**
Optional features (AI rewrite, voice typing, contact suggestions) are
explicitly opt-in and behave as described below.

---

## 1. What we do NOT collect

The following categories of data are **never** collected, stored on our
servers, or transmitted off your device:

- The text you type
- Your typing patterns (rhythm, speed, key sequences)
- Swipe-typing gesture paths
- Your personal dictionary / learned words
- Words you delete or correct
- Your contacts (unless you explicitly enable contact suggestions —
  see §4 below)
- Your microphone audio (unless you tap the mic button — see §3 below)
- Your location, advertising ID, device identifiers, or any other
  identifier outside the app sandbox

There is **no analytics SDK, no crash reporting SDK, no advertising SDK,
and no tracking library** in the application. You can verify this by
inspecting `app/build.gradle.kts` in the published source.

---

## 2. What stays on your device

The following data is created and stored **only on your device**, in the
application's private sandbox storage. None of it is uploaded anywhere
unless you explicitly choose to share it (see §6):

| What | Where | Why | Removable |
|---|---|---|---|
| Personal dictionary (`UserDictionaryStore`) | `files/user_dict/` | Improves swipe-typing for words you commonly type | Settings → Personal Dictionary → Clear |
| Learned-word list | `files/learned_words/` | Auto-corrects what the system learned from your usage | Settings → Learned Words → Clear |
| Swipe debug log (debug builds only) | `cache/swipe-debug/` | Diagnoses swipe-typing accuracy issues | Diag → Clear log |
| Crash reports | `files/crash_logs/` | Lets you share a crash report with support | Crash Reports → Delete all |
| User preferences | `SharedPreferences` | Theme, sounds, vibration, language settings | Settings → Reset |

When you uninstall the Keyboard, Android wipes the entire sandbox
automatically. Nothing persists outside it.

---

## 3. Voice typing (optional, off by default)

If you tap the microphone icon on the keyboard, the Keyboard will request
the **`RECORD_AUDIO`** permission the first time. Audio is processed for
speech-to-text using Android's system voice typing service (not by us).
We do not store audio buffers and do not transmit them.

You can revoke microphone access at any time from Android Settings → Apps →
VelociKeys → Permissions.

---

## 4. Contact suggestions (optional, off by default)

If you enable contact suggestions in Settings, the Keyboard will request
the **`READ_CONTACTS`** permission. Contact names are then used to suggest
completions when you start typing one (e.g., typing "Mar" suggests
"Maria"). The contacts data is read only on demand and never stored or
transmitted. Disabling the feature in Settings stops all reads
immediately.

---

## 5. AI features (optional, off by default)

Some advanced features (text rewrite, translation) require sending the
selected text to an AI backend over the internet. These features are:

- **Off by default**. You activate them per-action by tapping a button
  in the AI toolbar.
- **Scoped to selection**. Only the text you explicitly select is sent —
  never the surrounding document or anything you type elsewhere.
- **Not retained**. Our backend processes the request and returns a
  result; no copy of the request is stored long-term.

If you do not want the AI features, do not tap the AI button. The
keyboard works fully offline without them.

---

## 6. Crash reports — local-first

If the keyboard crashes, a crash report is written locally to
`files/crash_logs/`. **Nothing is uploaded automatically.** From the
Crash Reports screen you can:

- See how many reports exist on your device
- Preview each report
- **Tap Share** to send a report yourself (e.g., by email) using the
  Android system share sheet
- **Tap Delete all** to wipe every report

Only when you tap Share does any crash data leave your device, and only
to the destination you choose.

---

## 7. Swipe debug log (debug builds only)

In debug-flavored builds (used for development and beta testing), a
`SwipeDebugCapture` writes detailed swipe-typing traces to
`cache/swipe-debug/`. This is gated behind a manifest flag and is **not
present in Play Store release builds.** If you receive a beta build with
this enabled, the same control applies: nothing is uploaded; you choose
when to share.

---

## 8. Children's privacy

The Keyboard does not knowingly collect or process any personal
information. It is suitable for users of any age and complies with
COPPA / GDPR-K because no identifiable data is collected.

---

## 9. Your rights (GDPR / CCPA)

Because the Keyboard does not collect or transmit personal data, most
GDPR / CCPA articles do not apply. The data that does exist (personal
dictionary, learned words, preferences) lives entirely under your
control on your device. You can:

- **View**: Settings → Personal Dictionary, Learned Words, Crash Reports
- **Export**: tap Share on any item to export it via the system share
  sheet
- **Delete**: each screen has a Clear / Delete All control; uninstalling
  the Keyboard wipes everything

For any question, contact the developer at the address in the Play
Store listing.

---

## 10. Changes to this policy

If this policy changes, the new version will be published at the same
URL with an updated "Last updated" date. Material changes will be
disclosed in the app's changelog and onboarding screen.

---

## 11. Source verification

VelociKeys AI is built on the open-source HeliBoard / AOSP keyboard
foundation. The full source code, including this privacy policy and the
exact data-flow rules implemented in code, is available in the project
repository for independent audit.
