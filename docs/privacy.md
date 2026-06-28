# Privacy statement

*Last updated: 2026-06-28*

Retirement Risk Lab is a Monte Carlo retirement simulator that runs entirely on your device. This page describes, in plain English, what data the app handles and what — if anything — leaves your device.

## What the app collects

**Nothing, in the normal sense of "collects."** There is no account to create, no email to enter, no profile, no usage analytics, no telemetry, no advertising SDK. The app does not phone home to a developer-controlled server at any point.

The information you enter into the form (your age, balance, spending, contributions, Social Security details, tax assumptions, etc.) is stored in two places:

1. **On your device.** Your in-progress scenario draft and any named scenarios you save live in the standard app data location for your operating system:
    - macOS: `~/Library/Application Support/RetirementRiskLab/`
    - iOS / iPadOS: the app's sandboxed Documents and Application Support directories.
2. **In your iCloud, optionally.** If you turn on iCloud sync (a Lifetime Unlock feature), your saved scenarios are synced via Apple's CloudKit private database. See "iCloud sync" below.

## What leaves your device

There are three narrow cases where data leaves your device, and in every case Apple — not the developer — is the only party who ever sees what's transmitted:

1. **App Store purchase and subscription handling.** When you tap "Unlock for $24.99" or "Restore Purchases," Apple's StoreKit handles the transaction. The developer never sees your payment method, billing address, or Apple ID. The developer is only notified, by Apple, that you are entitled to the Lifetime Unlock.
2. **iCloud sync (optional, off by default for Free users; available for Lifetime users).** When iCloud sync is on, your named scenarios are stored in Apple's CloudKit *private* database — a region of iCloud that belongs to your Apple ID and is end-to-end encrypted under it. The developer cannot read your scenarios; the only way to see them is through your Apple ID's iCloud account. You can turn iCloud sync off at any time in the app's Settings.
3. **Crash reports, if you opt in at the OS level.** If you have enabled "Share with App Developers" in iOS / macOS Privacy & Security settings, Apple may send the developer aggregated, anonymized crash logs to help fix bugs. This is controlled by Apple and your OS settings, not by the app itself. You can turn it off at any time. The crash reports do not contain your scenario data.

## What the app does NOT do

- **No analytics.** The app does not embed Google Analytics, Mixpanel, Segment, Firebase Analytics, or any equivalent SDK. It does not log "user viewed screen X" or "user tapped button Y" anywhere.
- **No advertising.** There are no ads in the app. There are no advertising SDKs in the app.
- **No third-party trackers.** The app does not contain Meta Pixel, TikTok Pixel, or any social-network tracking code.
- **No fingerprinting.** The app does not collect your device's advertising identifier, MAC address, or any other persistent device identifier for tracking purposes.
- **No machine binding.** Your Lifetime Unlock is tied to your Apple ID via Family Sharing, not to a specific device's hardware identifier.

## Your scenarios are yours

Your scenario data is yours. You can:

- **Export it.** Settings → Scenario Backup → Export creates a JSON file containing all your named scenarios. You can keep that file, move it to another device, or use it as a backup.
- **Delete it.** Delete a named scenario from the Library and it's gone from your device. If iCloud sync is on, the deletion propagates to your other devices via CloudKit.
- **Disconnect from iCloud.** Turn iCloud sync off in Settings and the app stops syncing immediately. Existing local data is unaffected. To purge what's already in iCloud, sign out of iCloud at the OS level (Settings → [Your Name] → iCloud) and delete the app's iCloud data via Apple's standard iCloud management tools.

## Third-party services

The only third-party service the app uses is **Apple's own infrastructure**: the App Store (for purchase), StoreKit (for in-app purchase), and CloudKit (for optional iCloud sync). All three are governed by Apple's privacy policy.

The app does not use any of the following: Stripe, PayPal, Lemon Squeezy, Auth0, Firebase, Google services, Facebook services, Twitter / X services, Microsoft services, Anthropic services, OpenAI services, or any other third-party API.

## Children

The app is not directed at children under 13 and does not knowingly collect any information from anyone. There is no account to create, so there is no opportunity for a child to register.

## Changes to this statement

If this statement changes, the updated version will be published on this page and the "Last updated" date at the top will change. Material changes (anything that would alter how your data is handled) will be highlighted in a banner on the home page and in the app itself.

## Questions or concerns

If you have questions about how your data is handled, or you believe the app's behavior differs from what's described here, please file an issue on the [GitHub repository](https://github.com/ether-ore/RRLsite) — that's the most effective place to reach the developer and get a public answer that helps everyone.

---

*This statement describes the app's behavior at the version reflected by the "Last updated" date. It is not a contract. It is the best plain-English description of what the app actually does, written by the person who built it.*
