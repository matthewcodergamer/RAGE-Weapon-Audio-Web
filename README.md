# RAGE Weapon Audio Web

Mobile-first browser utility for extracting GTA V / FiveM `.awc` weapon-audio banks into a flat, game-ready WAV ZIP.

## Decoder v5

The converter now treats **every AWC stream as an independent audio asset**. A 16-stream bank is parsed, validated, previewed and exported as 16 separate streams — never as one grouped fake conversion.

The current decoder follows the CodeWalker AWC layout:

- `ADAT` / `TADA` container parsing.
- `0xFA` format chunks and `0x55` data chunks.
- PCM16 (`codec 0`).
- Rockstar IMA ADPCM (`codec 4`).
- ADPCM uses 2048-byte blocks.
- Each ADPCM block reads the initial **16-bit predictor from bytes 0–1**, the **step index from byte 2**, emits the predictor sample, and then decodes up to 2044 bytes of nibbles.
- Unsupported, encrypted and multi-channel layouts are rejected instead of exported as noise.

Reference: `dexyfex/CodeWalker`, `AwcFile.cs` / `ADPCMCodec`.

## Per-stream verification

Each stream tracks:

- source bank and stream ID
- codec
- sample rate
- declared sample count
- decoded sample count
- duration
- raw-data hash
- decoded-audio hash
- peak level
- RMS level
- DC offset
- clipping ratio
- exact-duplicate relationship

Very short valid sounds are labeled **short component**. Weapon banks often contain trigger, bolt, casing, impact, mechanical, transient, tail or other tiny components in addition to complete gunshots, so a short click/punch is not automatically a decode failure.

## Fast large-folder workflow

Folder import only parses metadata and hashes raw stream chunks. It does **not** decode all 100+ clips immediately, which keeps iPhone/Safari responsive.

Actual PCM decoding happens independently when a stream is previewed or when **Export All Verified WAVs as ZIP** is pressed. The export loop yields back to the browser regularly so the interface stays responsive.

## Output

```text
Project-Strike-Audio/
├── audio/
│   ├── weapons_player__ptl_pistol__001__0x........wav
│   ├── weapons_player__ptl_pistol__002__0x........wav
│   ├── dlc_weapons__db_shotgun__001__0x........wav
│   └── ... all verified WAVs in this one folder
└── audio-manifest.json
```

There is no folder per bank or per sound. Layer + bank + stream information is embedded into filenames to prevent silent ZIP overwrites.

## GitHub Pages

Publish `main` from `/ (root)` under **Settings → Pages**.

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/`

## Asset notice

This repository contains no Rockstar Games, Call of Duty, GTA V mod-pack, or other third-party audio assets. Files are selected and processed locally by the browser. Users are responsible for permission to use or redistribute source audio.