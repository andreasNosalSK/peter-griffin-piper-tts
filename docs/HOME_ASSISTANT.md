# Install a Piper custom voice in Home Assistant

Requires a working Home Assistant setup using the **Piper** app/service with the **Wyoming** integration. The training PC is not required for inference once the two export files have been copied to the system that runs Piper.

## Files required

```text
en_US-peter-medium.onnx
en_US-peter-medium.onnx.json
```

The names must match and the config must be named `<model>.onnx.json`.

## Install using the Piper web interface

1. Open Home Assistant and find the **Piper** app in **Settings > Apps** (install it if required).
2. Start the app and open its web interface.
3. Use the custom Piper voice upload control to upload **both** files.
4. In **Settings > Devices & services**, reload the Wyoming integration for Piper so its voice list refreshes.
5. In **Settings > Voice assistants**, open your Assist pipeline and select the new voice for text-to-speech.
6. Test the assistant with a short sentence.

## Alternative: `/share/piper`

On Home Assistant OS setups with a supported `/share/piper` directory, copy both voice files to that directory. The Piper app can discover custom models there; the Wyoming integration may still need a reload to show the new voice.

## Troubleshooting

**Voice not listed:** verify both filenames, check that the Piper app is using the `piper` backend, and reload the Wyoming integration.

**Only JSON uploaded:** the JSON file is not the speech model; it must be paired with the ONNX file.

**Voice works on your PC but not on Home Assistant:** check the architecture/back-end, model/config accessibility, and Piper app logs. Verify the model locally first (see [CLI.md](CLI.md)).

**Unexpected sound:** compare against a local generated WAV and consider switching to a better training checkpoint.

Official reference: https://github.com/home-assistant/apps/blob/master/piper/DOCS.md
