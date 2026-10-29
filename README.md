# Robustness & Interpretability of Vision Foundation Models

**Research artifact from the IASc–INSA–NASI Summer Research Fellowship Programme 2025**
**Machine Intelligence Unit, Indian Statistical Institute, Kolkata**

A reproducible experimental study of **robustness, interpretability, and model behaviour under distribution shift** across convolutional and transformer-based vision architectures.

---

## Overview

Modern vision models can achieve strong predictive performance while behaving very differently when inputs are perturbed or when their decisions are interpreted.

This project studies two related questions:

1. **How robust are CNNs and Vision Transformers under common distribution shifts?**
2. **How stable and informative are their explanations when the input distribution changes?**

The repository contains experiments across:

* ResNet-18
* Vision Transformer (ViT)
* Swin Transformer
* CIFAR-10
* Fashion-MNIST
* Tiny-ImageNet
* ImageNet-100
* ImageNet-V2

Interpretability experiments use both convolutional and transformer-oriented methods, including:

* Grad-CAM
* LayerCAM
* ScoreCAM
* EigenCAM
* Attention Rollout
* transformer attribution variants

The broader goal is not only to compare predictive accuracy, but to examine how **model architecture, robustness and explanation behaviour interact**.

---

## Research Context

This work was conducted during the **IASc–INSA–NASI Summer Research Fellowship Programme 2025** at the **Indian Statistical Institute, Kolkata**.

### Research supervision

**Prof. Sanghamitra Bandyopadhyay**
Professor, Machine Intelligence Unit
Indian Statistical Institute, Kolkata

**Dr. Malay Bhattacharyya**
Associate Professor, Machine Intelligence Unit
Indian Statistical Institute, Kolkata

The complete fellowship report is included in:

```text
survey-report/
└── SRFP-Suha_Robustness_Interpretebility_VFM.pdf
```

---

## Research Workflow

```text
Dataset
   │
   ▼
Model / architecture
   │
   ├── ResNet
   ├── ViT
   └── Swin Transformer
   │
   ▼
Baseline evaluation
   │
   ▼
Distribution shift / perturbation
   │
   ├── flip
   ├── rotation
   ├── blur
   ├── brightness
   └── Gaussian noise
   │
   ▼
Robustness evaluation
   │
   ▼
Explanation generation
   │
   ├── CAM-based methods
   └── transformer attention / attribution
   │
   ▼
Comparative analysis
```

The experiments are designed to examine both:

```text
prediction behaviour
        +
explanation behaviour
```

rather than treating interpretability as an isolated visualization step.

---

## Experimental Tracks

### 1. Robustness under distribution shift

The primary experiments compare CNN and transformer-based architectures under controlled image perturbations.

The evaluation investigates how model predictions change under transformations such as:

* horizontal or spatial transformations,
* rotation,
* image blur,
* brightness changes,
* Gaussian noise.

Experiments span small-scale classification datasets and ImageNet-derived evaluation sets.

---

### 2. Explainability across architectures

Different architectures require different interpretation strategies.

For convolutional models, the repository explores CAM-family methods such as:

```text
Grad-CAM
LayerCAM
ScoreCAM
EigenCAM
```

For transformer-based architectures, experiments include attention-based and transformer attribution approaches such as:

```text
Attention Rollout
transformer attribution variants
```

This allows explanation behaviour to be compared alongside predictive robustness.

---

### 3. Weakly-Supervised Segmentation Experiments

The repository also contains exploratory notebooks investigating **CAM- and transformer-based localization / weakly-supervised segmentation workflows**.

These include experiments around:

* Grad-CAM-derived activation masks,
* ViT attention rollout,
* mask morphology,
* dilation and erosion variants,
* rotation perturbations,
* Dice-loss-related experiments.

These notebooks represent an additional experimental track and are kept alongside the main robustness and interpretability study for reproducibility.

---

## Datasets

| Dataset                   | Role                                                           |
| ------------------------- | -------------------------------------------------------------- |
| **CIFAR-10**              | CNN / transformer training and robustness experiments          |
| **Fashion-MNIST**         | Cross-domain small-image robustness experiments                |
| **Tiny-ImageNet**         | Higher-complexity visual robustness evaluation                 |
| **ImageNet-100**          | ImageNet-scale subset experiments                              |
| **ImageNet-V2**           | Distribution-shift evaluation                                  |
| **VOC-based experiments** | Exploratory localization / weakly-supervised segmentation work |

Large datasets are **not committed to Git**.

Dataset download utilities are provided in:

```text
scripts/
├── download_data.ps1
└── download_data.sh
```

---

## Model Weights

Trained model artifacts are intentionally stored outside GitHub.

Weights are available through Hugging Face:

**https://huggingface.co/suharoy/vfm-robustness-weights**

Available released checkpoints include:

| Architecture     | Dataset       |
| ---------------- | ------------- |
| ResNet-18        | CIFAR-10      |
| ResNet-18        | Fashion-MNIST |
| ViT              | CIFAR-10      |
| ViT              | Fashion-MNIST |
| Swin Transformer | CIFAR-10      |
| Swin Transformer | Fashion-MNIST |

Download them with:

```powershell
python scripts/download_models_hf.py
```

The script creates the local `models/` directory automatically.

---

## Repository Structure

```text
.
├── data/
│   └── README.md
│
├── notebooks/
│   ├── cifar-10-resnet-vit.ipynb
│   ├── cifar-10-swin.ipynb
│   ├── fashionmnist-resnet-vit.ipynb
│   ├── fashionmnist-swin.ipynb
│   ├── imagenet-100-robustness+explainability.ipynb
│   ├── imagenet-v2-robustness+explainability.ipynb
│   ├── tiny-imagenet-robustness+explainability.ipynb
│   │
│   ├── gcam-voc-wsss-baseline-v1.ipynb
│   ├── gcam_voc-wsss-a-rotate.ipynb
│   ├── gcam_voc-wsss-b-diceloss.ipynb
│   ├── gcam_voc-wsss-c-dilate3.ipynb
│   ├── gcam_voc-wsss-d-dilate5.ipynb
│   ├── gcam-voc-wsss-e-erode3.ipynb
│   └── voc-wsss-vitroll-all-exp.ipynb
│
├── scripts/
│   ├── download_data.ps1
│   ├── download_data.sh
│   └── download_models_hf.py
│
├── survey-report/
│   └── SRFP-Suha_Robustness_Interpretebility_VFM.pdf
│
├── .gitignore
├── CITATION.cff
├── LICENSE
├── README.md
└── requirements.txt
```

---

## Notebook Guide

### Classification, robustness and explainability

| Notebook                                        | Focus                                        |
| ----------------------------------------------- | -------------------------------------------- |
| `cifar-10-resnet-vit.ipynb`                     | ResNet-18 and ViT experiments on CIFAR-10    |
| `cifar-10-swin.ipynb`                           | Swin Transformer experiments on CIFAR-10     |
| `fashionmnist-resnet-vit.ipynb`                 | ResNet-18 and ViT on Fashion-MNIST           |
| `fashionmnist-swin.ipynb`                       | Swin Transformer on Fashion-MNIST            |
| `imagenet-100-robustness+explainability.ipynb`  | ImageNet-100 robustness and explanations     |
| `imagenet-v2-robustness+explainability.ipynb`   | Distribution-shift evaluation on ImageNet-V2 |
| `tiny-imagenet-robustness+explainability.ipynb` | Tiny-ImageNet robustness and explainability  |

### WSSS / localization experiments

| Notebook                          | Experimental focus                |
| --------------------------------- | --------------------------------- |
| `gcam-voc-wsss-baseline-v1.ipynb` | Grad-CAM baseline                 |
| `gcam_voc-wsss-a-rotate.ipynb`    | Rotation experiment               |
| `gcam_voc-wsss-b-diceloss.ipynb`  | Dice-loss experiment              |
| `gcam_voc-wsss-c-dilate3.ipynb`   | Mask dilation experiment          |
| `gcam_voc-wsss-d-dilate5.ipynb`   | Larger mask dilation experiment   |
| `gcam-voc-wsss-e-erode3.ipynb`    | Mask erosion experiment           |
| `voc-wsss-vitroll-all-exp.ipynb`  | ViT attention-rollout experiments |

These names describe the experimental variants represented by the notebooks; detailed methodology and outputs should be read directly from the corresponding notebook.

---

## Key Findings

Across the experiments, several general observations emerged.

### Architecture matters under distribution shift

CNN and transformer architectures do not respond identically to image perturbations. Robustness varies with both the architecture and the type of shift applied.

### Explanation behaviour also changes

Model explanations can change even when predictions remain correct.

This makes robustness of the **explanation itself** an important consideration when interpreting model behaviour under shifted inputs.

### CNN and transformer explanations are structurally different

CAM-based CNN explanations often produce localized activation regions, whereas transformer attention and attribution methods tend to represent information more globally.

Direct visual comparison therefore needs to account for architecture-specific explanation mechanisms.

### There is no universally dominant model / explanation pair

No single architecture or explanation method should be assumed to dominate across every dataset, perturbation and evaluation setting.

The experimental context matters.

---

## Reproducibility

### Requirements

* Python 3.10+
* Git
* Kaggle credentials for automatic dataset download
* sufficient storage for the selected datasets
* GPU recommended for training and larger experiments

Clone the repository:

```powershell
git clone https://github.com/suharoy/Robustness-Interpretebility-VFM-Survey.git
cd Robustness-Interpretebility-VFM-Survey
```

Create an isolated environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

---

## Download Datasets

Install and configure the Kaggle CLI.

Place your Kaggle credentials at:

```text
%USERPROFILE%\.kaggle\kaggle.json
```

Then on Windows:

```powershell
powershell -ExecutionPolicy Bypass -File scripts\download_data.ps1
```

On Linux / macOS:

```bash
bash scripts/download_data.sh
```

The current download scripts support:

* CIFAR-10
* Fashion-MNIST
* ImageNet-100
* Tiny-ImageNet
* ImageNet-V2

Additional data required by the exploratory VOC notebooks should be prepared according to the corresponding notebook.

---

## Download Released Weights

```powershell
python scripts/download_models_hf.py
```

The files are downloaded from:

**https://huggingface.co/suharoy/vfm-robustness-weights**

into:

```text
./models/
```

---

## Run the Experiments

Start JupyterLab:

```powershell
jupyter lab
```

Then open the notebook corresponding to the dataset, architecture or experimental track of interest.

Some notebooks were originally developed in notebook-based research environments such as Kaggle. Dataset paths may therefore need to be adjusted for local execution.

---

## Research Report

The full fellowship report is available directly in this repository:

[**SRFP Report — Robustness & Interpretability of Vision Foundation Models**](survey-report/SRFP-Suha_Robustness_Interpretebility_VFM.pdf)

The report provides the broader research motivation, literature context and experimental discussion accompanying the repository.

---

## Reproducibility and Repository Hygiene

Large artifacts are intentionally excluded from Git.

The repository keeps:

```text
source notebooks
download scripts
dependency definitions
research report
documentation
```

while excluding:

```text
datasets
model checkpoints
temporary caches
notebook checkpoints
local environments
```

Released model weights are hosted separately on Hugging Face.

---

## Limitations

This repository should be interpreted as a **research artifact**, not a production vision library.

Important limitations include:

* robustness is evaluated against a defined set of perturbations rather than every possible real-world distribution shift;
* explanation quality cannot be reduced to a single universal metric;
* different attribution methods are not always directly comparable across architectures;
* several experiments are notebook-oriented rather than packaged as a single training framework;
* the VOC/WSSS notebooks represent exploratory experimental variants and are not presented as a standalone segmentation framework;
* dataset preparation and compute requirements vary substantially across experiments.

These constraints are important when interpreting individual results.

---

## Citation

If you use this repository or the released model weights in academic work, please cite:

```bibtex
@misc{roy2025vfm,
  author       = {Suha Roy},
  title        = {Robustness and Interpretability of Vision Foundation Models under Distributional Shifts},
  year         = {2025},
  howpublished = {GitHub repository},
  url          = {https://github.com/suharoy/Robustness-Interpretebility-VFM-Survey},
  note         = {Research conducted during the IASc-INSA-NASI Summer Research Fellowship Programme 2025 at the Indian Statistical Institute, Kolkata}
}
```

A machine-readable citation is also provided in `CITATION.cff`.

---

## Acknowledgements

This work was carried out as part of the **IASc–INSA–NASI Summer Research Fellowship Programme 2025**.

I gratefully acknowledge:

* **Prof. Sanghamitra Bandyopadhyay**, Machine Intelligence Unit, Indian Statistical Institute, Kolkata
* **Dr. Malay Bhattacharyya**, Machine Intelligence Unit, Indian Statistical Institute, Kolkata
* **Indian Statistical Institute, Kolkata**
* **IASc–INSA–NASI Summer Research Fellowship Programme**

---

## License

The original code and documentation in this repository are released under the **MIT License**. See [`LICENSE`](LICENSE).

Datasets, pretrained models, research libraries and other third-party resources remain subject to their respective licenses and terms.

---

## Author

**Suha Roy**

M.Sc. Computer Science — Big Data Analytics
Central University of Rajasthan

**GitHub:** https://github.com/suharoy
**Hugging Face:** https://huggingface.co/suharoy
**LinkedIn:** https://linkedin.com/in/suharoy
