# Peter Griffin-inspired Piper TTS (unofficial)

An **unofficial, community-trained English (US) text-to-speech voice** designed for [Piper TTS](https://github.com/OHF-Voice/piper1-gpl) and local voice responses in [Home Assistant](https://www.home-assistant.io/).

> **Unofficial fan project.** This is not made, sponsored, or endorsed by the creators of *Family Guy*, its distributors, or the people who perform its characters. Rights to the source recordings and any resulting model have **not been verified for redistribution**. Review [Rights and licensing](RIGHTS_AND_LICENSING.md) before publishing model weights or audio samples.

## Overview

| Property | Value |
| --- | --- |
| Voice | Peter Griffin-inspired, unofficial |
| Language | English (United States), `en_US` |
| Engine | Piper TTS / ONNX Runtime |
| Architecture | VITS, single speaker |
| Quality label | `medium` |
| Sample rate | 22,050 Hz |
| ONNX file size | ~61 MB (local export) |
| Training method | Fine-tuned from the Piper Lessac medium checkpoint |
| Hardware used | RTX 4070 Ti (12 GB), Windows 11 + Ubuntu WSL2 |

The training log reported **1,444 processed utterances**. The training was configured for up to 2,000 epochs; the exact selected release checkpoint and final epoch should be documented in [MODEL_CARD.md](MODEL_CARD.md) when publishing a release.

## Download

Download **both** model files from the [latest release (`piper-tts`)](https://github.com/andreasNosalSK/peter-griffin-piper-tts/releases/tag/piper-tts):

- `en_US-peter-medium.onnx` (voice model)
- `en_US-peter-medium.onnx.json` (model configuration)

## Quick test (Windows / Linux / WSL2)

Install Piper in a Python environment:

```bash
python -m pip install piper-tts
```

In the directory containing the two model files, generate a test WAV:

```bash
python -m piper \
  -m ./en_US-peter-medium.onnx \
  -c ./en_US-peter-medium.onnx.json \
  -f ./test.wav \
  -- "Hey Lois, somebody left the kitchen lights on again!"
```

Play `test.wav` using your preferred audio player. No NVIDIA GPU is required for ordinary CPU inference.

For detailed instructions see [CLI usage](docs/CLI.md) and [troubleshooting](docs/TROUBLESHOOTING.md).

## Use with Home Assistant

1. Install and start the **Piper** app in Home Assistant (or use an existing Piper service connected through Wyoming).
2. Upload `en_US-peter-medium.onnx` **and** `en_US-peter-medium.onnx.json` using Piper's web interface. On supported Home Assistant OS setups, copying them to `/share/piper` is also supported.
3. **Reload the Wyoming integration** for Piper so Home Assistant refreshes its voice list.
4. Under **Settings > Voice assistants**, select the voice for the relevant Assist pipeline.
5. Test a spoken Home Assistant response.

See [the complete Home Assistant guide](docs/HOME_ASSISTANT.md).

## How it was created

- Source used: the community [petergriffinclassic dataset](https://huggingface.co/datasets/justinjohn-03/petergriffinclassic). Its displayed dataset card does not establish a clear redistribution license.
- Audio was converted to 22,050 Hz mono WAV and paired with text transcripts.
- Training used the [OHF-Voice Piper](https://github.com/OHF-Voice/piper1-gpl) VITS fine-tuning workflow and the Lessac medium base checkpoint.
- The trained checkpoint was exported to ONNX, and the matching JSON configuration was generated during training.

More details: [Model card](MODEL_CARD.md) and [Training notes](docs/TRAINING_NOTES.md).

## Limitations

This is a character-style experimental voice, not a general-purpose quality benchmark. It may pronounce unusual names, foreign-language words, numbers, or long sentences incorrectly. A successful ONNX export does not prove that all phrases will sound natural.

Do not use a synthetic voice to mislead people into thinking an actual actor or character creator approved or recorded a message.

## Credits

Thanks to the [Piper TTS project](https://github.com/OHF-Voice/piper1-gpl), the community dataset uploader, and Home Assistant's voice ecosystem. Mentioning a dataset or project is attribution, **not** evidence that it grants rights to redistribute recordings or a derived model.
