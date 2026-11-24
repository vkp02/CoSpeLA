# CoSpeLA

**Band-Agnostic Contrastive Spectral-Language Alignment for Low-Data Hyperspectral Retrieval**

Official repository for the paper *"CoSpeLA: Band-Agnostic Contrastive
Spectral-Language Alignment for Low-Data Hyperspectral Retrieval"* by
Vijay Kumar Pandey and Tushar Sandhan (Department of Electrical Engineering,
Indian Institute of Technology Kanpur).

CoSpeLA is a band-agnostic contrastive encoder that aligns hyperspectral cubes
with free-form language in the low-data regime. It pools over a
wavelength-conditioned band axis, so a single model consumes a variable number of
spectral bands, and it is trained on 670 public cubes on a single GPU.

> **Code availability.** The full code, captioned data, and configuration files
> will be released in this repository upon publication of the paper. This page
> documents the method and the structure and usage the release will follow; the
> sections below describe what the release will contain.

## Planned repository layout
Upon release, the repository will be organized as follows.
```
.
├── materialclip/            # core package: model, data, training
│   ├── models/              # the CoSpeLA encoder
│   ├── data/                # hyperspectral dataset / loaders
│   └── train/               # training entry point(s)
├── scripts/                 # evaluation and figure generation
│   ├── dump_val_embeddings.py
│   ├── retrieval_stats.py
│   ├── eval_dofa_clip_retrieval.py
│   ├── make_tsne_realsensor.py
│   └── qualitative_retrieval.py
├── captions/                # generated captions (Qwen2.5-VL), one per cube
├── configs/                 # training / evaluation configs
├── requirements.txt
├── LICENSE
└── README.md
```

## Data
Training cubes come from three public datasets: ICVL, CAVE, and NTIRE 2020 ARAD
(31 bands, 400–700 nm). The real-sensor transfer uses the public AVIRIS (Salinas,
Indian Pines) and ROSIS (Pavia University, Pavia Centre) scenes. The generated
captions, and the expected directory layout for the raw cubes, will be provided
with the code release.

## Usage (available on release)
Once the code is released, the environment and the main experiments will be
reproduced as follows.
```bash
# setup
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# train (single GPU): stage 1, then stage 2 with band augmentation
python -m materialclip.train.train --config configs/stage1.yaml
python -m materialclip.train.train --config configs/stage2_bandaug.yaml --resume <stage1_ckpt>

# retrieval metrics with bootstrap confidence intervals
python scripts/dump_val_embeddings.py --ckpt <ckpt> --out embeddings/
python scripts/retrieval_stats.py --emb embeddings/

# real-sensor transfer t-SNE
python scripts/make_tsne_realsensor.py --ckpt <ckpt> --data_dir downstream --scenes salinas pavia
```
The trained checkpoint will be provided as a GitHub Release asset.

## Citation
```bibtex
@article{pandey2026cospela,
  title   = {{CoSpeLA}: Band-Agnostic Contrastive Spectral-Language Alignment for Low-Data Hyperspectral Retrieval},
  author  = {Pandey, Vijay Kumar and Sandhan, Tushar},
  year    = {2026}
}
```

## License
Released under the MIT License. See `LICENSE`.
