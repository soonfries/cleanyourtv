# Project context

CleanYourTV strips ads, telemetry and preloaded apps from Android TV and Google TV sets over ADB
(`pm disable-user`, never uninstall) and replaces the home screen with a small native launcher
(`launcher/`, package `com.gathin.tvhome`). Everything is reversible with `tools/restore.sh`.

## Conventions that specs must respect

- Launcher: plain Java, AndroidX RecyclerView, no Kotlin, no Compose, no network, no polling, no
  background services. Targets TVs with about 1 GB of RAM.
- TV-specific values go in `launcher/app/src/main/res/values/config.xml` or a theme, not in code.
- D-pad navigation is deterministic.
- New strings go in `values/strings.xml` and every `values-*` folder.
- Privacy by design and by default (Art. 25 GDPR): the launcher has no `INTERNET` permission,
  `allowBackup="false"`, and stores nothing that is not needed for the home screen.
- Third-party features ship as separate module apps that declare a card (`docs/specs/card.md`).
