# Model card: Peter Griffin-inspired Piper voice

## Model details

| Field | Detail |
| --- | --- |
| Model ID | `en_US-peter-medium` |
| Model type | Text-to-speech (Piper / VITS / ONNX) |
| Locale | `en_US` |
| Speakers | 1 |
| Output sample rate | 22,050 Hz |
| Base checkpoint | Piper `en_US/lessac/medium`, warm-start fine-tuning |
| Training runtime | Windows 11, Ubuntu WSL2, NVIDIA RTX 4070 Ti (12 GB VRAM) |
| Local ONNX export size | ~61 MB |
| Config | `en_US-peter-medium.onnx.json` |
| Final release checkpoint | **TODO: record exact checkpoint filename / epoch** |
| Model license | **Undetermined; no permission to redistribute is asserted** |

## Intended uses

Local text-to-speech experiments and Home Assistant responses where use of the voice and underlying recordings is authorized. The character-inspired voice is not an official recording or an endorsed product.

## Training data and provenance

- Community dataset: https://huggingface.co/datasets/justinjohn-03/petergriffinclassic
- Dataset listing: 1,646 rows; audio plus text fields.
- Dataset converter generated a single-speaker Piper-compatible corpus with 22,050 Hz mono WAV and transcript metadata.
- Training log reported **1,444 utterances processed**; this is not an independently audited count of accurately transcribed clips.
- Dataset licensing, provenance and permissions are **not established** by the available dataset card. This matters for publishing fine-tuned weights.

Do not ship the original training recordings or full training caches as part of this repository.

## Training and export

The fine-tune used the Open Home Foundation Piper training framework, initialized from Lessac medium and run with a batch size of 4. The configured maximum was 2,000 epochs. An ONNX export produced `en_US-peter-medium.onnx` (~61 MB) and a matching JSON config (~5 KB). See [training notes](docs/TRAINING_NOTES.md).

**Before publishing a model release**, fill in:

- Exact released checkpoint path and epoch: TODO
- Training code commit or Piper version: TODO
- Dataset cleaning/review performed: TODO
- SHA-256 of both released files: TODO

## Evaluation

The creator reported generating and listening to a successful voice sample using Piper. No controlled speaker-similarity, intelligibility, MOS, robustness, or bias evaluation has been provided. Avoid presenting the model as validated for unrestricted production use.

Recommended release checks: intelligibility on unseen Home Assistant phrases; pronunciation of names/numbers; latency on CPU; voice consistency on long text; and volume/distortion.

## Limitations and risks

- Accents, numbers, abbreviations, and unseen words may be synthesized incorrectly.
- Small or noisy voice datasets can cause unusual timing and pronunciation.
- A familiar character-like synthetic voice may cause listener confusion about attribution or endorsement.
- The source recordings and likeness may be protected by copyright and other applicable rights.

## Rights

The character and source media are not owned by this repository. The author of this template does not grant redistribution rights to a character performance, dataset, model weights, or other third-party material. See [RIGHTS_AND_LICENSING.md](RIGHTS_AND_LICENSING.md).
