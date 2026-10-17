# MeerKatta - AI Dictation and Thought Capture

[MeerKatta](https://meerkatta.com/) is an AI dictation and thought-capture app
for Mac and iPhone, created by [Lugugul Design](https://lugugul.com/).
Speak into your work, or save an idea before it slips away. Keep your thoughts
flowing without pausing to edit.

- [Explore MeerKatta](https://meerkatta.com/)
- [Download the latest Mac installer](https://github.com/curiowls/meerkattasparkle/releases/latest/download/MeerKatta-latest.dmg)
- [Get started tips](https://meerkatta.com/welcome/)
- [Plans and pricing](https://meerkatta.com/pricing/)

## macOS release and update feed

This repository distributes the Mac app and its Sparkle update feed.

This repo holds:

- `appcast.xml` — the Sparkle feed the Mac app polls daily for updates.
- GitHub Releases under each version tag (`v1.0.0`, `v1.1.0`, …) — each
  attaches the signed, notarized `MeerKatta-<version>.dmg` as a release
  asset.

Release flow on the dev machine:

```sh
cd ~/meerkatta/swift-app
./release-mac.sh                    # builds, signs, notarizes, creates DMG,
                                    # uploads to GH release, prints appcast entry
# Then:
cd /path/to/meerkattasparkle
# paste the appcast entry inside <channel> in appcast.xml
git add appcast.xml && git commit -m "appcast: v<version>" && git push
```

The Mac app's `Info.plist` carries:

- `SUFeedURL` = `https://raw.githubusercontent.com/curiowls/meerkattasparkle/main/appcast.xml`
- `SUPublicEDKey` = `r6jz+VMG+AQFRG3uP6n2Yg+53ECNnkXoUv94W7/iBeM=`

The matching EdDSA private key lives only in the macOS Keychain on the
release machine (item: "Sparkle EdDSA Signing Key"). Losing that key means
existing installs won't trust new updates — protect accordingly.
