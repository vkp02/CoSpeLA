# **CoSpeLA**

Band-Agnostic Contrastive Spectral-Language Alignment for Low-Data Hyperspectral Retrieval
Official repository for the paper "CoSpeLA: Band-Agnostic Contrastive Spectral-Language 
Alignment for Low-Data Hyperspectral Retrieval" by Vijay Kumar Pandey and Tushar Sandhan 
(Department of Electrical Engineering, Indian Institute of Technology Kanpur).

CoSpeLA is a band-agnostic contrastive encoder that aligns hyperspectral cubes with 
free-form language in the low-data regime. It pools over a wavelength-conditioned band 
axis, so a single model consumes a variable number of spectral bands, and it is trained
on 670 public cubes on a single GPU.

> **Code availability.** The full code, captioned data, and configuration files
> will be released in this repository upon publication of the paper. This page
> documents the method and the structure and usage the release will follow.

## Planned repository layout
Upon release, the repository will be organized as follows.
```
.
├── cospela/        # core package: model, data, training
├── scripts/             # evaluation and figure generation
├── captions/            # generated captions (Qwen2.5-VL)
├── configs/             # training / evaluation configs
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
Once the code is released, the repository will include the training code, the
evaluation and figure-generation scripts, and the configuration files needed to
reproduce the results in the paper. The pipeline, in brief:

1. Install the dependencies from `requirements.txt`.
2. Train the band-agnostic encoder on a single GPU (contrastive pre-training
   followed by band-augmented training).
3. Evaluate spectrum-to-text and text-to-spectrum retrieval under the
   deterministic, bootstrap-validated protocol.
4. Run the frozen-encoder transfer to the real airborne sensors and generate the
   figures.

Full commands, configuration files, and the trained checkpoint (as a GitHub
Release asset) will accompany the code release.

## Citation
The paper is currently under review. Citation details will be added here upon publication.

## License
Released under the MIT License. See `LICENSE`.
