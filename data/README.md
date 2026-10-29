# Dataset Directory

Large datasets used by this research are intentionally excluded from version control.

The repository provides download utilities for the primary classification and robustness datasets.

## Windows

Install the Kaggle CLI:

```powershell
pip install kaggle
```

Place your Kaggle API credentials at:

```text
%USERPROFILE%\.kaggle\kaggle.json
```

Then run:

```powershell
powershell -ExecutionPolicy Bypass -File scripts\download_data.ps1
```

## Linux / macOS

Install and configure the Kaggle CLI, then run:

```bash
bash scripts/download_data.sh
```

## Supported Downloads

The scripts currently download:

* CIFAR-10
* Fashion-MNIST
* ImageNet-100
* Tiny-ImageNet
* ImageNet-V2

Downloaded files are stored beneath `data/` and remain ignored by Git.

Additional data used by exploratory VOC/WSSS notebooks is not currently provisioned by these scripts and should be prepared according to the corresponding notebook.
