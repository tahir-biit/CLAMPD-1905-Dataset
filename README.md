# CLAMPD-1905: Cross-Language Malicious Package Detection Dataset

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python" alt="Python">
  <img src="https://img.shields.io/badge/Research-Academic-red?style=flat-square" alt="Academic">
  <img src="https://img.shields.io/badge/Status-Active-success?style=flat-square" alt="Status">
</p>

---

## 🌟 Overview

**CLAMPD-1905** represents a breakthrough in cross-language malicious package detection research. This meticulously curated dataset addresses the critical need for unified, standardized evaluation of malware detection tools across diverse software supply chain ecosystems. Built upon the foundation of [MalwareBench](https://github.com/MalwareBench), CLAMPD-1905 provides the first comprehensive collection of **20,000 labeled software packages** from both PyPI and npm repositories, each encoded as sophisticated **1905-dimensional feature vectors** through advanced multimodal fusion techniques.

The prevalence of third-party components in modern software development has significantly amplified software supply chain security risks. Popular registries like npm and PyPI serve as highly targeted channels for malware distribution, necessitating robust detection mechanisms. CLAMPD-1905 addresses the fundamental challenge of cross-ecosystem threat detection by providing unified representations that capture structural, behavioral, and contextual characteristics of packages across different programming language ecosystems.

### Key Contributions

- **Cross-Ecosystem Coverage**: First dataset to provide unified detection across PyPI and npm
- **Multimodal Feature Fusion**: Combines metadata, graph structures, and API semantics
- **Perfect Balance**: Equal distribution of benign and malicious samples
- **Research Ready**: Standardized format for immediate model training and evaluation
- **Reproducible**: Complete feature engineering pipeline and pre-computed embeddings
- **Enhanced Representation**: 1905-dimensional vectors enabling sophisticated threat analysis

## Dataset Construction and Sources

CLAMPD-1905 is systematically constructed using packages from [MalwareBench](https://github.com/MalwareBench), a comprehensive benchmark dataset for software supply chain security research. Our enhanced dataset builds upon MalwareBench's foundation by applying advanced feature engineering and multimodal fusion techniques to create unified 1905-dimensional representations.

**Data Source**: [MalwareBench](https://dl.acm.org/doi/10.1145/3643991.3644883) - A labeled dataset comprising 20,792 packages from npm and PyPI ecosystems

**Referenced Works**:
- **[Backstabber's Knife Collection](https://link.springer.com/chapter/10.1007/978-3-030-52683-2_2)**: Foundational research on open-source supply chain attacks
- **[PyPiGuard](https://github.com/tahir-biit/PyPiGuard)**: PyPI package analysis and detection framework

### Data Description and Structure

CLAMPD-1905 includes both malicious and neutral packages, each annotated with comprehensive metadata and ground truth labels. Ground truth classifications categorize packages into two groups:

- **Malicious**: Packages designed to carry out harmful actions, posing threats to system confidentiality, integrity, or availability
- **Benign**: Packages with no discovered malware or suspicious behavioral patterns

The dataset provides extensive metadata including package identifiers, version information, ecosystem classification, file statistics, dependency relationships, and behavioral indicators for comprehensive threat analysis.

## Dataset Composition

### Feature Architecture (1905 Dimensions)

| Component | Dimensions | Description |
|-----------|------------|-------------|
| **Static Metadata** | 9 | Normalized package characteristics (size, file count, ecosystem) |
| **Graph Embeddings** | 128 | HAN-based dependency relationship representations |
| **API Behaviors** | 1768 | BERT semantics (768D) + frequency vectors (1000D) |

### Data Statistics

- **Total Packages**: 20,000 (10,000 PyPI + 10,000 npm)
- **Class Distribution**: 50% benign, 50% malicious

## Quick Start

### Loading the Dataset

```python
import numpy as np
import pandas as pd

# Load feature matrix and labels
features = np.load('data/features/final_combined_features.npy')
labels = np.load('data/features/labels.npy')
feature_names = np.load('data/features/full_feature_names.npy')

# Load metadata
metadata = pd.read_csv('data/metadata/enhanced_metadata.csv')

print(f"Dataset shape: {features.shape}")
print(f"Feature dimensions: {features.shape[1]}")
print(f"Class distribution: {np.bincount(labels)}")
```

### File Structure

```
CLAMPD-1905/
├── data/
│   ├── features/
│   │   ├── final_combined_features.npy    # Main 1905D dataset
│   │   ├── labels.npy                     # Ground truth labels
│   │   └── full_feature_names.npy         # Feature mappings
│   ├── metadata/
│   │   ├── enhanced_metadata.csv          # Package metadata
│   │   └── api_statistical_features.csv   # API statistics
│   └── graphs/
│       └── dependency_graph.gpickle       # Dependency structure
└── README.md
```

## Research Applications

### Primary Use Cases

- **Malware Detection**: Cross-ecosystem threat identification
- **Feature Engineering**: Multimodal fusion techniques
- **Graph Learning**: Dependency relationship modeling
- **Transfer Learning**: Cross-platform generalization studies



## Citation

*Citation will be available upon publication.*

## Technical Details

### Feature Engineering Pipeline

1. **Metadata Normalization**: Z-score standardization of numerical features
2. **Dependency Graph Construction**: Directed graphs from package manifests
3. **HAN Embedding Training**: 128-dimensional structural representations
4. **API Sequence Processing**: BERT-based semantic encoding + frequency analysis
5. **Multimodal Fusion**: Concatenation into unified 1905D vectors

### Data Quality Assurance

- **Completeness Check**: >99% feature availability
- **Label Verification**: Manual validation of threat classifications  
- **Consistency Validation**: Cross-ecosystem format standardization
- **Reproducibility**: Deterministic feature extraction pipeline

## Comparison with Existing Datasets

| Dataset | Ecosystems | Size | Multimodal | Balanced | Graph Features |
|---------|------------|------|------------|----------|----------------|
| **CLAMPD-1905** | PyPI + npm | 20K | ✓ | ✓ | ✓ |
| [MalwareBench](https://dl.acm.org/doi/10.1145/3643991.3644883) | PyPI + npm | 20K | ✗ | ✗ | ✗ |
| [PypiGuard](https://github.com/tahir-biit/PyPiGuard) | PyPI only | 6K | Partial | ✗ | ✗ |
| [Backstabber's](https://link.springer.com/chapter/10.1007/978-3-030-52683-2_2) | PyPI only | 13K | ✗ | ✗ | ✗ |

## Contact

**Tahir Iqbal**  
📧 tahir.biit@gmail.com | tahir@mail.dlut.edu.cn  
🏛️ Dalian University of Technology, School of Software Technology

## License

This dataset is released under the MIT License. See `LICENSE` file for details.

---

**Note**: This dataset is provided for research purposes. Users are responsible for ensuring ethical use and compliance with applicable regulations.
