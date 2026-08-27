# RAGE Weapon Audio Web

Mobile-first browser utility for extracting GTA V / FiveM `ADAT` `.awc` weapon-audio banks into a flat, game-ready WAV ZIP.

## What changed

The decoder now follows the established CodeWalker AWC layout instead of guessing ADPCM blocks.

- AWC header and chunk tables are validated before export.
- PCM (`codec 0`) is decoded directly.
- Rockstar IMA ADPCM (`codec 4`) uses fixed 2048-byte blocks.
- ADPCM block header is read as CodeWalker does: step index at byte 0, predictor at bytes 2-3, followed by 2044 bytes of nibbles.
- Unsupported, multi-channel, or encrypted layouts are rejected instead of being exported as noise.
- Each bank has a **Preview** button so you can hear the first decoded stream before exporting everything.

Reference implementation: `dexyfex/CodeWalker`, `AwcFile.cs` / `ADPCMCodec.DecodeADPCM`.

## Workflow

1. Tap **Choose Folder** and select a folder containing `.awc` files.
2. Or use **Choose AWC Files** to select many files manually on iPhone.
3. The app validates each bank and lists its stream count + codec.
4. Tap **Preview** on a bank to verify decoding.
5. Tap **Export All WAVs as ZIP** once.
6. Download `Project-Strike-Audio.zip`.

## Flat ZIP layout

```text
Project-Strike-Audio/
├── audio/
│   ├── lmg_combat__001__0x........wav
│   ├── lmg_combat__002__0x........wav
│   ├── ptl_pistol__001__0x........wav
│   ├── sht_pump__001__0x........wav
│   └── ... every WAV in this one folder
├── audio-manifest.json
└── README.txt
```

There is **no folder per bank and no folder per sound**. Bank names are built into filenames to prevent collisions, so `audio/` can be dragged directly into the game project's audio location.

`audio-manifest.json` preserves the original bank, stream ID/hash, source filename, WAV path, codec, sample rate, sample count, and duration.

## Current support

- Batch folder import.
- Multi-file AWC import.
- Little-endian `ADAT` and big-endian `TADA` header recognition.
- Single-channel weapon banks.
- PCM16 (`codec 0`).
- Rockstar IMA ADPCM (`codec 4`).
- CodeWalker-compatible 2048-byte ADPCM block decoding.
- Preview before export.
- One-click batch conversion.
- One flat WAV folder inside one ZIP.
- Game manifest generation.
- Local-only browser processing.

The parser was verified against `lmg_combat.awc`, which exposes four mono PCM streams at 48 kHz.

## Intentionally rejected

The tool refuses layouts it cannot decode reliably rather than creating fake/random audio:

- single-channel encrypted banks
- multi-channel banks
- multi-channel encrypted banks
- unknown codecs
- corrupted chunk tables

Those formats need a dedicated implementation before they are allowed through the export path.

## GitHub Pages

Publish `main` from `/ (root)` under **Settings → Pages**.

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/`

## Asset notice

This repository contains no Rockstar Games, Call of Duty, GTA V mod-pack, or other third-party audio assets. Files are selected and processed locally by the browser. Users are responsible for permission to use or redistribute source audio.