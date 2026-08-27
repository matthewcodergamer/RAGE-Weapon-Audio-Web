# RAGE Weapon Audio Web / Project Strike Asset Processor

Mobile-first browser utilities for preparing Project Strike assets.

## Audio decoder

The AWC converter treats **every AWC stream as an independent audio asset**. A multi-stream bank is parsed, validated, previewed and exported independently — never as one grouped fake conversion.

The current decoder follows the CodeWalker AWC layout:

- `ADAT` / `TADA` container parsing.
- `0xFA` format chunks and `0x55` data chunks.
- PCM16 (`codec 0`).
- Rockstar IMA ADPCM (`codec 4`).
- 2048-byte ADPCM blocks.
- unsupported/encrypted layouts are rejected instead of exported as noise.

## Model processor

Open `model-processor.html` (or `/RAGE-Weapon-Audio-Web/model-processor.html` on GitHub Pages).

It performs real asset processing rather than changing file extensions:

- extracts `.zip` archives locally with JSZip
- indexes model + texture files
- previews actual GLB/glTF models with Three.js
- resolves glTF BIN/texture dependencies selected in the same folder/ZIP
- parses FBX using Three.js `FBXLoader`
- converts a successfully parsed FBX scene to **binary GLB** using `GLTFExporter`
- reports mesh count, triangle count, materials, textures, bones and animation count
- preserves `.blend` as a Blender source asset instead of fake-converting it

`.blend` → GLB conversion belongs in the FPS repository's headless Blender GitHub Action, where real Blender opens the source file and exports the runtime GLB.

## Runtime target

Project Strike should normally ship GLB/glTF, KTX2 textures, JSON manifests and compressed audio. High-quality FBX/Blend/4K–8K source assets remain editable sources and are compiled into optimized runtime variants.

## GitHub Pages

Audio tool:

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/`

Model processor:

`https://matthewcodergamer.github.io/RAGE-Weapon-Audio-Web/model-processor.html`

## Asset notice

This repository contains no Rockstar Games, Call of Duty, GTA V mod-pack, or other third-party audio/model payloads. Files are selected and processed locally by the browser. Users are responsible for permission to use or redistribute source assets.
