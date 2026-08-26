# RAGE Weapon Audio Web

Mobile-first browser utility for reading GTA V / FiveM `ADAT` `.awc` weapon audio banks and exporting individual streams as standard WAV files.

## Current features

- Works entirely in the browser; selected audio is not uploaded.
- iPhone/Safari-friendly file picker.
- Open one or many `.awc` files.
- Open a folder and scan its `.awc` files.
- Parses ADAT stream tables and FORMAT/DATA chunks.
- Supports PCM16 (`codec 0`) weapon streams.
- Supports IMA ADPCM (`codec 4`) streams.
- Individual stream preview with Web Audio.
- Waveform preview.
- Export individual streams as WAV.
- Export all streams in a bank as WAV downloads.
- Displays stream hash/id, sample rate, duration, codec, sample count, and size.

## Verified sample

The initial parser was developed against `lmg_combat.awc` from a GTA V/FiveM weapon-audio bank. That sample contains four mono PCM16 streams at 48 kHz and is handled directly by this tool.

## GitHub Pages

Publish the repository from the `main` branch root:

1. Repository **Settings** → **Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select `main` and `/ (root)`.
4. Save.

The expected Pages URL is:

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/`

## iPhone usage

1. Open the Pages site in Safari.
2. Tap **Choose AWC Files**.
3. Pick a file such as `lmg_combat.awc`, `ptl_pistol.awc`, or `sht_bullpup.awc` from Files.
4. The bank should appear with its individual streams.
5. Tap **▶** to preview a stream.
6. Tap **WAV** to export that stream as a standard PCM WAV file.

For many banks, use **Choose Folder** and select the extracted folder containing your `.awc` files.

## Format references

The implementation follows publicly documented/researched GTA V AWC/ADAT structures, including work in CodeWalker and related community implementations. The IMA ADPCM decoder uses the standard IMA ADPCM algorithm.

## Asset notice

This repository contains no Rockstar Games, Call of Duty, GTA V mod-pack, or other third-party audio assets. The utility processes files selected by the user locally. Users are responsible for having permission to use/export/distribute the source audio they select.
