# RAGE Weapon Audio Web

Mobile-first browser utility for reading GTA V / FiveM `ADAT` `.awc` weapon audio banks and converting them into game-ready WAV packs.

## Batch workflow

1. Open one or many `.awc` files, or choose a folder.
2. The tool parses all supported banks locally in the browser.
3. Preview any individual stream.
4. Select the banks you want to export.
5. Tap **Download Game-Ready ZIP**.
6. The generated ZIP contains organized WAV folders plus an `audio-manifest.json` ready to plug into a game asset pipeline.

## Output layout

```text
Project-Strike-Audio/
├── audio/
│   ├── lmg_combat/
│   │   ├── lmg_combat_stream_001_0x........wav
│   │   └── ...
│   ├── ptl_pistol/
│   └── ...
├── manifest/
│   └── audio-manifest.json
└── IMPORT-INTO-GAME.txt
```

The generated manifest records the bank name, stream hash/id, output WAV path, source codec, sample rate, sample count and duration for every converted stream.

## Current features

- Works entirely in the browser; selected audio is not uploaded.
- iPhone/Safari-friendly interface.
- Multi-file AWC import.
- Folder import where supported by the browser.
- Drag-and-drop on desktop.
- Parses ADAT stream tables and FORMAT/DATA chunks.
- Supports PCM16 (`codec 0`) weapon streams.
- Supports IMA ADPCM (`codec 4`) streams.
- Individual stream preview with Web Audio.
- Export individual streams as WAV.
- Export one bank as a ZIP.
- Select multiple/all banks and export every stream in one ZIP.
- Automatic game-ready folder organization.
- Automatic `audio-manifest.json` generation.
- Conversion/ZIP progress display.
- Displays stream hash/id, sample rate, duration, codec and size.

## Verified sample

The initial parser was developed against `lmg_combat.awc` from a GTA V/FiveM weapon-audio bank. That sample contains four mono PCM16 streams at 48 kHz and is handled directly by this tool.

## GitHub Pages

Publish the repository from the `main` branch root:

1. Repository **Settings** → **Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select `main` and `/ (root)`.
4. Save.

Expected Pages URL:

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/`

## iPhone usage

Use **Choose AWC Files** to select multiple banks from the Files app. After loading, keep the banks you want checked and tap **Download Game-Ready ZIP**. For large collections, exporting in several groups can reduce Safari memory pressure.

## Asset notice

This repository contains no Rockstar Games, Call of Duty, GTA V mod-pack, or other third-party audio assets. The utility processes files selected by the user locally. Users are responsible for having permission to use, export or redistribute the source audio they select.
