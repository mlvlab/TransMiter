# [AAAI2026] Transferable Model-agnostic Vision-Language Model Adaptation for Efficient Weak-to-Strong Generalization

> Jihwan Park<sup>1</sup>, Taehoon Song<sup>2</sup>, Sanghyeok Lee<sup>2</sup>, Miso Choi<sup>1</sup>,  Hyunwoo J. Kim<sup>2</sup>
>
> <sup>1</sup>Korea University    <sup>2</sup>Korea Advanced Institute of Science and Technology (KAIST)


> **Note:** This repository currently contains the raw code. Code cleaning is in progress.
## Installation

```bash
conda create -n transmiter python=3.9 -y && conda activate transmiter
pip install torch==1.13.0+cu117 torchvision==0.14.0+cu117 torchaudio==0.13.0 --extra-index-url https://download.pytorch.org/whl/cu117
pip install -r requirements.txt
```

## Data

Download the data from [Hugging Face](https://huggingface.co/datasets/Jhp/transmiter) and place it in the `data` folder with the following structure:

```
data/
├── classnames_dictionary.csv
└── base2new_promptsrc/
    ├── caltech101/
    ├── dtd/
    ├── eurosat/
    ├── fgvc_aircraft/
    ├── food101/
    ├── imagenet/
    ├── oxford_flowers/
    ├── oxford_pets/
    ├── stanford_cars/
    ├── sun397/
    └── ucf101/
```

We use [PromptSRC](https://github.com/muzairkhattak/PromptSRC) for fine-tuning the source model.

**Supported datasets:** `EuroSAT`, `DTD`, `Food101`, `Pets`, `Aircraft`, `Flowers`, `UCF`, `Caltech`, `Cars`, `SUN397`, `ImageNet`

## Usage


### 1. Adaptation Knowledge Extraction

```bash
bash run_scripts/base2novel/knowledge_extraction/ket.sh \
    ViT-B-16 \ # source model
    "['promptsrc']" \ # source fine-tuning strategy
    dtd \ # dataset
    1 # seed
```

### 2. Adaptation Knowledge Transfer

```bash
bash run_scripts/base2novel/knowledge_transfer/transfer.sh \
    ViT-B-16 \ # source model
    ViT-L-14 \ # target model
    "['promptsrc']" \ # source fine-tuning strategy
    dtd \ # dataset
    1 # seed
```

## Citation

```bibtex
@inproceedings{park2026transmiter,
  title={Transferable Model-agnostic Vision-Language Model Adaptation for Efficient Weak-to-Strong Generalization},
  author={Park, Jihwan and Song, Taehoon and Lee, Sanghyeok and Choi, Miso and Kim, Hyunwoo J.},
  booktitle={AAAI},
  year={2026}
}
```