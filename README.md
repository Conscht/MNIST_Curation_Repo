# 🧹 🧹 🧹  MNIST Visual Curation — Enhanced MNIST with IDK Class🧹 🧹 🧹 

This repository contains the code and methodology used to curate a visually enhanced version of the classic **MNIST** dataset.  
The curated dataset adds an **IDK (“I Don’t Know”)** class for ambiguous, noisy, or hard-to-classify digits, enabling research on robust classification and uncertainty handling.

👉 **Curated dataset on Hugging Face:**  
https://huggingface.co/datasets/YOUR_DATASET_NAME  

👉 **This repository:** Code for data curation, embedding visualization, IDK generation, and classifier training.

---

## Overview

The curated MNIST dataset:

- keeps the original **10 digit classes (0–9)**
- adds an **11th class: `IDK`**
- relabels visually ambiguous, distorted, or extremely noisy samples as `IDK`
- is designed for:
  - robust classification experiments  
  - out-of-distribution detection  
  - dataset curation workflows  
  - training models that can abstain (“I don’t know”)  

---

## Motivation

Standard MNIST contains many *ambiguous* digits:

- spaghetti-like “9”  
- fuzzy or low-contrast strokes  
- digits written strangely or partially cropped  
- digits consistently misclassified by vanilla LeNet

These images reduce model reliability and complicate evaluation.  
The goal of this project is to:

1. **Identify** such problematic samples  
2. **Relabel** them as `IDK`  
3. **Retrain** a classifier on the improved dataset  
4. **Compare** the baseline vs IDK-aware model

---

## Curation Workflow

The curation process uses **FiftyOne**, **UMAP**, **PCA**, and **Brain metrics**.

### 1. Train a baseline **LeNet-5** classifier  
Used to extract embeddings and detect misclassified samples.

### 2. Visualize embedding space  
Using:
- **PCA**  
- **UMAP**  
- FiftyOne’s interactive embedding view
- 
### 3. Compute FiftyOne Brain metrics
- `hardness` – how often the model hesitates  
- `mistakenness` – samples frequently misclassified  
- `uniqueness` – outliers in embedding space  
- `representativeness` – typicality within the dataset



This reveals clusters of ambiguous digits and strong outliers.

Example UMAP visualization:

![UMAP Visualization](https://cdn-uploads.huggingface.co/production/uploads/673e7e7c4dca9bce31534dd7/bHTbMCZ0QL3ETONxoUT4S.png)

### 4. Manual curation in the FiftyOne App  
Suspicious samples detected by the above metrics were visually inspected:

- ambiguous shapes  
- messy handwriting  
- conflicting class evidence  
- strong outliers  
- mislabeled samples  

These were relabeled as `IDK`.

---


## Citation

If you use this curated dataset or code, please cite the original MNIST paper:

```bibtex
@article{lecun1998gradient,
  title={Gradient-based learning applied to document recognition},
  author={LeCun, Yann and Bottou, L{\'e}on and Bengio, Yoshua and Haffner, Patrick},
  journal={Proceedings of the IEEE},
  volume={86},
  number={11},
  pages={2278--2324},
  year={1998},
  publisher={IEEE}
}

