# Shifr-App

# Shifr — macOS Cipher App (Shifr-1.0)

A small, offline macOS app for experimenting with classical substitution ciphers (Caesar, Vigenère) built with SwiftUI.

## Overview

Shifr (Shifr-1.0.dmg) provides a simple graphical interface with several tools for encrypting, decrypting and analysing short texts. It is intended for learning, teaching, and quick encoding/decoding of short messages.

## Tabs / Tools

The app includes the following tabs (tools):

- Caesar — encrypt text with a configurable numeric shift (supports English and Russian alphabets).
- Vigenère — encrypt text with a user-supplied keyword (supports English and Russian alphabets).
- Decryptor — decrypt text in automatic or manual mode. Automatic mode will try candidate keys (for Caesar it lists all shifts; for Vigenère it attempts an automated analysis). Manual mode accepts a user-provided key.
- Key length analysis — attempts to estimate likely key lengths and candidate keys for the Vigenère cipher (currently optimized for Russian texts). You can inspect candidate plaintexts and apply a found key to the Decryptor tab.
- Frequency analysis — shows a bar chart of character frequencies for the supplied text (useful for manual analysis and heuristic attacks).

## Features & limitations

- Full offline operation — no network access or telemetry.
- Supports both English and Russian alphabets (case-preserving where possible).
- The key-length analysis and statistical attacks are focused on Russian text; the guided key-length scanning and the chi-square / IC methods are implemented for Russian (the app shows a warning if you attempt length analysis for non-Russian input).
- Automated Vigenère brute-force for non-Russian text is intentionally limited (small key lengths) to avoid combinatorial explosion; for longer English keys you should use external tools or build from source and adjust parameters.
- Frequency analysis uses a local charting view (the app imports Charts for visuals).

## Requirements

- macOS 15.6 Sequoia or later (the app bundle may contain a specific minimum target — check `Shifr.app/Contents/Info.plist` if you need an exact target).
- Apple Silicon or Intel Mac — the included app in the DMG should contain a binary for the supported architecture.

## Installation (from the DMG)

1. Open `Shifr-1.0.dmg` by double-clicking it in Finder.
2. In the window that appears, drag the `Shifr.app` icon to your `Applications` folder.
3. Eject the mounted DMG and, if desired, delete the downloaded `.dmg` file.

## Gatekeeper / First launch

If the app is not notarized/signed with a developer Apple ID, macOS Gatekeeper may block it on the first open. If that happens:

1. Right-click (or Control-click) the `Shifr.app` in Finder and choose "Open".
2. In the confirmation dialog click "Open" again. This allows the app to run while preserving Gatekeeper checks in the future.

## Usage examples

- Caesar:
  - Enter or paste text, set a numeric shift and press Encrypt/Decrypt. The app supports both English and Russian alphabets.

- Vigenère:
  - Enter text and a keyword (letters only). Press Encrypt/Decrypt.

- Decryptor:
  - Switch between automatic and manual modes. In automatic mode the app will generate candidate decryptions (Caesar: all shifts; Vigenère: statistical/heuristic attempts). In manual mode provide the key and decrypt.

- Key length analysis:
  - Paste the ciphertext and press "Scan key lengths". The tool will generate ranked candidates (k, average IC, candidate key and candidate plaintext). Selecting a candidate allows you to apply the key directly to the Decryptor.

- Frequency analysis:
  - Paste ciphertext in the Decryptor field and press "Analyze" in the Frequency tab to see a bar chart of character frequencies.

Notes:
- Non-letter characters are typically passed through unchanged for encrypt/decrypt operations.
- The Vigenère analysis assumes (where applicable) only alphabetic characters are used; the app performs a cleaning step for statistical analysis.

## Localization

UI strings are available in English and Russian. You can switch language in system preferences (macOS language settings) or rely on app automatic localization.

## Privacy & Security

- Shifr runs locally and does not transmit text or keys over the network.
- No telemetry or analytics are collected by the app.

## Troubleshooting

- App won’t open: see the Gatekeeper instructions above.
- Key length analysis only supports Russian text in the current implementation — you will see an in-app warning if you attempt to run it on non-Russian text.
- Automated Vigenère brute-force is limited for English (short keys only)

## Uninstall

- Quit the app.
- Remove `Shifr.app` from `/Applications`.
- Optionally remove preferences in `~/Library/Containers` or `~/Library/Preferences` if created.
