# Play Console — Data Safety form (answers)

This is the exact set of answers to fill into the Play Console **Data
safety** form for VelociKeys AI. Each section maps 1-to-1 to the Console
screens.

---

## Data collection and security

### Does your app collect or share any of the required user data types?

**No.**

VelociKeys AI does not transmit user data off the device for the core
keyboard experience. Optional AI features (translate / rewrite) send only
the text the user explicitly selects, do not retain it, and are off by
default. Optional voice typing uses the platform's system speech
service, which is governed by Google's own policies.

### Is all of the user data collected by your app encrypted in transit?

**N/A** (no data collected).

If the user opts into AI features, the optional backend call uses HTTPS
(TLS 1.2+). Stated under "Optional features" below.

### Do you provide a way for users to request that their data be deleted?

**Yes.**

- Personal dictionary, learned words, crash logs, and preferences are
  all deletable from in-app screens.
- Uninstalling the app wipes all data.

---

## Data types — answer "No, my app does not collect this data type" for ALL of:

- Approximate location, Precise location
- Personal info: Name, Email address, User IDs, Address, Phone number,
  Race and ethnicity, Political or religious beliefs, Sexual orientation,
  Other personal info
- Financial info (any)
- Health and fitness (any)
- Messages: Emails, SMS or MMS, Other in-app messages
- Photos and videos (any)
- Audio files (any)  ← **see Note 1 below**
- Files and docs (any)
- Calendar (any)
- Contacts (any)  ← **see Note 2 below**
- App activity: App interactions, In-app search history, Installed apps,
  Other user-generated content, Other actions
- Web browsing (any)
- App info and performance: Crash logs, Diagnostics, Other  ← **see Note 3**
- Device or other IDs (any)

> **Note 1 — Audio files**: VelociKeys AI never stores audio. Voice typing
> is handled by the Android platform speech service, which has its own
> declaration. No microphone audio is collected by the Keyboard itself.
>
> **Note 2 — Contacts**: If the user explicitly enables contact
> suggestions, the Keyboard reads contact NAMES on demand to provide
> completion suggestions. The data is never stored, transmitted, or
> shared. Because the Play Store rule is "collect" = "transferred
> off-device or persisted", on-demand reads do NOT count as collection.
> Selecting "No" is the correct answer per Google's own guidance, but
> you can describe the read in §3 of the Privacy Policy.
>
> **Note 3 — Crash logs**: Crashes are written to local files under the
> app sandbox. Nothing is uploaded automatically. If the user explicitly
> taps "Share" in Crash Reports, they choose where it goes. Per Play
> Console guidance, this is NOT collection — answer "No".

---

## Optional features (declare separately if you ever do collect)

The following sections apply only if you later add cloud sync, telemetry,
ad SDKs, or any feature that transmits personal data. **Do not check
these for v1.0.**

| Feature | Data type | Required? | Shared? | Encrypted in transit? |
|---|---|---|---|---|
| AI text rewrite (selected text only) | Other in-app messages | Optional | No | Yes (HTTPS) |
| AI translation (selected text only) | Other in-app messages | Optional | No | Yes (HTTPS) |

If you ship v1.0 without AI features active by default, leave these
blank. Activate the row in the form only when you ship the feature
turned on.

---

## App permissions screen (Play Console → Permissions)

When the form asks "Why does this app request these sensitive permissions?",
use these justifications verbatim:

### `RECORD_AUDIO`
> Required for the optional voice-typing feature (microphone icon on
> the keyboard). Permission is requested at runtime the first time the
> user taps the mic icon. The keyboard is fully usable without granting
> it. No audio is stored or transmitted by the app.

### `READ_CONTACTS`
> Required for the optional contact-suggestions feature. When enabled
> in Settings, contact names are read on demand to suggest completions
> as the user types. The feature is off by default. No contact data is
> stored or transmitted.

### `INTERNET`
> Required for the optional AI text rewrite and translation features.
> Activated per-action by the user; nothing is sent without an explicit
> tap. The keyboard is fully usable offline.

### `VIBRATE`
> Required for haptic feedback on key presses (standard keyboard
> behavior).

---

## Pre-launch checklist tied to this form

Before submitting the Data Safety form:

- [ ] Privacy Policy URL is publicly reachable (e.g., GitHub Pages)
- [ ] The privacy policy answers match the Data Safety form answers
      (no contradictions — Google's auto-checker will flag mismatches)
- [ ] No analytics / ads / crash-reporting SDKs in the dependencies
      list. Run `./gradlew :app:dependencies | grep -E 'firebase|crashlytics|amplitude|appsflyer|adjust|braze|amplitude|mixpanel'`
      and confirm empty output before each release
- [ ] The release APK does not include the swipe debug receiver
      (gated by `${isDevEnabled}` in the manifest — we set this above)
- [ ] No accessibility services declared (we don't use them)
- [ ] Target SDK 35 (current Play Store requirement; will rise to 36
      in 2027)

---

## Questions Google reviewers commonly ask for keyboards

If your listing review is escalated, prepare answers for these common
follow-ups:

1. **"Where is the privacy policy hosted?"** → GitHub Pages URL
2. **"What does INTERNET permission do?"** → Optional AI features only
3. **"How does the user revoke permissions?"** → Standard Android
   Settings → Apps → VelociKeys → Permissions; in-app toggles for
   AI / Contact suggestions
4. **"Do you collect typed text in any form?"** → No; this is the
   first answer in the privacy policy
5. **"What is the second launcher icon for?"** → Removed in release
   builds (gated by `${isDevEnabled}`); only in debug builds for
   developer use

---

## What to do if Google rejects the listing

Common rejection reasons for keyboard apps:

| Rejection | Fix |
|---|---|
| "Permission requests not justified" | Update the per-permission justifications in the listing |
| "Data Safety form contradicts privacy policy" | Diff the two; resolve any field that says "yes" in one and "no" in the other |
| "Sensitive accessibility services declared" | We don't use any; if a third-party library does, replace it |
| "App contains crash logs / IDs in a tracker" | Confirm Note 3 above; if Google still flags, link to the local-only file path |
| "Two launcher icons" | Confirm the manifest gate is in place and you submitted the release build, not the debug build |

---

## Source of truth

Ground truth for any data-related question is the file
`docs/PRIVACY_POLICY.md` in the project repository, plus the manifest
permissions list and `app/build.gradle.kts` dependencies. If any of
those change, update this form on the next release.
