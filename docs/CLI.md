# Local Piper usage

## Install

Use Python 3 in a virtual environment:

```bash
python -m pip install piper-tts
```

Place both model files in one directory, then run:

```bash
python -m piper \
  -m ./en_US-peter-medium.onnx \
  -c ./en_US-peter-medium.onnx.json \
  -f ./test.wav \
  -- "Hey Lois, somebody left the kitchen lights on again!"
```

The WAV file can be played with any audio player. You can use the same command under Windows PowerShell by entering it on a single line:

```powershell
python -m piper -m .\en_US-peter-medium.onnx -c .\en_US-peter-medium.onnx.json -f .\test.wav -- "Hey Lois, somebody left the kitchen lights on again!"
```

## Verify before upload

In the extracted repository, stage the exported files from your WSL2 training directory (only if you have distribution rights):

```bash
python scripts/prepare_release.py --source ~/peter-tts/output --dest ./release-assets
```

To validate the staged model and compute SHA-256 digests:

```bash
python scripts/verify_voice.py --dir ./release-assets
```

For an additional ONNX structural check, install `onnx` and add `--deep`:

```bash
python -m pip install onnx
python scripts/verify_voice.py --dir ./release-assets --deep
```

## WSL2 to Windows Desktop

To open the output directory in Windows Explorer from Ubuntu:

```bash
explorer.exe "$(wslpath -w "$HOME/peter-tts/output")"
```

Then copy the `.onnx` and `.onnx.json` files to your Windows Desktop. Always keep matching filenames.

Official Piper CLI reference: https://github.com/OHF-Voice/piper1-gpl/blob/main/docs/CLI.md
