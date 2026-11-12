# Local Dictation voice models

Files the Local Dictation apps (Windows, Android) download once, on first run. Speech is turned into text on the
device; nothing is ever uploaded.

## redux-fp32-v1 (Windows)

Parakeet Redux by Moondream (https://huggingface.co/moondream/parakeet-redux), licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), based on NVIDIA parakeet-tdt-0.6b-v3
(https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3), licensed CC BY 4.0.
Changes: exported to ONNX (encoder weights stored as plain 32-bit floats, one file per weight), decoder and joiner
as separate ONNX files, tokenizer pieces in tokens.txt. Each file is Brotli-compressed (`<name>.br`);
`manifest.json` lists every file with its size and SHA-256.

## redux-q4-v1 (Windows, from 1.0.0)

The same Parakeet Redux model with the encoder stored as exact 4-bit blocks (ONNX MatMulNBits, 4 bits, block 128):
Redux's encoder weights are already -1, 0 or +1 times one scale per block of 128, so this storage is lossless.
Packed by the Local Dictation Android chat (`tools/pack_q4.py`); on 306 test clips it writes exactly the same words as
redux-fp32-v1. One `encoder.onnx` (344 MB) plus the decoder, joiner and tokens. Same licence and credits as above.

## Licence

The model files are licensed under the Creative Commons Attribution 4.0 International licence
(https://creativecommons.org/licenses/by/4.0/legalcode). Attribution: Moondream (Parakeet Redux) and NVIDIA
(Parakeet TDT 0.6B v3). The ONNX conversion and packaging by Sebastian Škoić are released under the same licence.
