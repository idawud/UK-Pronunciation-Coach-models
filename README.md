# UK Pronunciation Coach – model files

Phoneme-recognition models used by the [UK Pronunciation Coach](https://github.com/idawud/UK-Pronunciation-Coach) app. This repository only hosts the files as GitHub Release assets; the app and its CI download them by URL and check each file's SHA-256 against `assets/models/manifest.json` in the app repository.

## Releases

| Release | File | Tier | What it is |
| --- | --- | --- | --- |
| `models-v1` | `full-model.onnx`, `full-vocab.json` | Full (optional download in the app) | [facebook/wav2vec2-lv-60-espeak-cv-ft](https://huggingface.co/facebook/wav2vec2-lv-60-espeak-cv-ft), exported to ONNX (opset 17) and quantised to uint8. 392-token espeak IPA vocab, CTC blank `<pad>` at 0, 20 ms frames. |
| `models-v1` | `light-model.onnx`, `light-vocab.json` | Light (bundled in the app) | A 6-layer student distilled on CPU from the full model (layers 0, 4, 8, 12, 16, 20 kept), uint8. Same vocab as the full tier. |

`models-v1` is published. On held-out British speakers the full tier marks 2.5% of correct words red and catches 86.8% of substitution probes; the light tier marks 5.9% red (above the 5% target) and catches 68.0%, so it stays the fallback for slower phones, with word-level scores only and its own older scoring calibration. Neither tier yet reaches the error-detection rate wanted for a public release; that needs fine-tuning on British speech. See `docs/models.md` and `docs/eval-report.md` in the app repository.

## Licences and attribution

- **Model weights:** Apache-2.0, from facebook/wav2vec2-lv-60-espeak-cv-ft (Meta).
- **Light tier training data:** distilled on the [CSTR VCTK Corpus](https://datashare.ed.ac.uk/handle/10283/3443) (University of Edinburgh), licensed CC BY 4.0. Attribution: "Trained in part on the CSTR VCTK Corpus (University of Edinburgh), CC BY 4.0."

No user data is used or collected. The app runs these models on the phone and sends nothing anywhere.
