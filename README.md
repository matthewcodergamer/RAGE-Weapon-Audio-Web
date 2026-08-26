# RAGE Weapon Audio Web

Mobile-first browser utility for converting GTA V / FiveM `ADAT` `.awc` weapon-audio banks into one game-ready WAV ZIP.

## Simple workflow

1. Tap **Choose Folder** and select the extracted folder containing your `.awc` files.
2. If folder selection is unavailable on your iPhone, tap **Choose AWC Files** and select multiple `.awc` files instead.
3. The app scans and parses every supported AWC bank locally.
4. Tap the single **Export All to WAV ZIP** button.
5. Every detected stream is converted to WAV automatically.
6. The browser downloads one file: `Project-Strike-Audio.zip`.

There are no per-bank export buttons and no need to select individual sounds for the normal batch workflow.

## ZIP layout

```text
Project-Strike-Audio/
├── audio/
│   ├── lmg_combat/
│   │   ├── lmg_combat_stream_001_0x........wav
│   │   └── ...
│   ├── ptl_pistol/
│   ├── sht_pump/
│   └── ...
├── manifest/
│   └── audio-manifest.json
└── IMPORT-INTO-GAME.txt
```

`audio-manifest.json` records the source bank, stream ID/hash, WAV path, codec, sample rate, sample count and duration so the exported package can plug into the Project Strike audio loader later.

## Current support

- Batch folder import where supported by the browser.
- Multi-file AWC import as an iPhone fallback.
- ADAT AWC parsing.
- PCM16 (`codec 0`).
- IMA ADPCM (`codec 4`).
- One-click conversion of all loaded streams.
- One ZIP download containing all WAV files.
- Automatic game-ready folder organization.
- Automatic audio manifest generation.
- Conversion and ZIP progress display.
- Processing happens locally in the browser.

The parser was initially verified against `lmg_combat.awc`, which contains four mono PCM16 streams at 48 kHz.

## GitHub Pages

Publish from `main` and `/ (root)` under Repository **Settings → Pages**.

Expected URL:

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/`

## Asset notice

This repository contains no Rockstar Games, Call of Duty, GTA V mod-pack, or other third-party audio assets. The utility only processes user-selected files locally. Users are responsible for having permission to use, export, or redistribute their source audio.