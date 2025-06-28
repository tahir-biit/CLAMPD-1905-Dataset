# CLAMPD-1905: Cross-Language Malicious Package Detection Dataset

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python" alt="Python">
  <img src="https://img.shields.io/badge/Research-Academic-red?style=flat-square" alt="Academic">
  <img src="https://img.shields.io/badge/Status-Active-success?style=flat-square" alt="Status">
</p>

---

## 🌟 Overview

**CLAMPD-1905** represents a breakthrough in cross-language malicious package detection research. This meticulously curated dataset addresses the critical need for unified, standardized evaluation of malware detection tools across diverse software supply chain ecosystems. Built upon the foundation of [MalwareBench](https://github.com/MalwareBench), CLAMPD-1905 provides the first comprehensive collection of **23,764 balanced software packages** from both PyPI and npm repositories, each encoded as sophisticated **1905-dimensional feature vectors** through advanced multimodal fusion techniques.

The prevalence of third-party components in modern software development has significantly amplified software supply chain security risks. Popular registries like npm and PyPI serve as highly targeted channels for malware distribution, necessitating robust detection mechanisms. CLAMPD-1905 addresses the fundamental challenge of cross-ecosystem threat detection by providing unified representations that capture structural, behavioral, and contextual characteristics of packages across different programming language ecosystems.

### Key Features

- **Cross-Ecosystem Coverage**: First dataset to provide unified feature representation across PyPI and npm
- **Multimodal Feature Integration**: Combines normalized metadata, HAN dependency graph embeddings, and BERT API behavioral features
- **Perfect Class Balance**: 23,764 packages with equal distribution of benign and malicious samples (11,882 each)
- **Advanced Feature Engineering**: 1905-dimensional vectors through sophisticated multimodal fusion
- **Research Ready**: Standardized format for immediate model training and evaluation
- **Reproducible**: Complete feature engineering pipeline and pre-computed embeddings
- **Comprehensive Representation**: Captures structural, behavioral, and contextual package characteristics

## Dataset Construction and Sources

CLAMPD-1905 is systematically constructed using packages from [MalwareBench](https://github.com/MalwareBench), a comprehensive benchmark dataset for software supply chain security research. Our enhanced dataset builds upon MalwareBench's foundation by applying advanced feature engineering and multimodal fusion techniques to create unified 1905-dimensional representations.

**Data Source**: [MalwareBench](https://dl.acm.org/doi/10.1145/3643991.3644883) - A labeled dataset comprising 20,792 packages from npm and PyPI ecosystems, enhanced through stratified upsampling to achieve perfect class balance.

**Referenced Works**:
- **[Backstabber's Knife Collection](https://link.springer.com/chapter/10.1007/978-3-030-52683-2_2)**: Foundational research on open-source supply chain attacks
- **[PyPiGuard](https://github.com/tahir-biit/PyPiGuard)**: PyPI package analysis and detection framework

### Dataset Characteristics

CLAMPD-1905 includes both malicious and benign packages, each annotated with comprehensive metadata and ground truth labels:

- **Malicious**: Packages designed to carry out harmful actions, posing threats to system confidentiality, integrity, or availability
- **Benign**: Packages with no discovered malware or suspicious behavioral patterns

The dataset provides extensive metadata including package identifiers, version information, ecosystem classification, file statistics, dependency relationships, and behavioral indicators for comprehensive threat analysis.

## Dataset Composition

### Feature Architecture (1905 Dimensions)

| Component | Dimensions | Description |
|-----------|------------|-------------|
| **Static Metadata** | 9 | Normalized package characteristics (ecosystem, artifact ID, threat type, file count, package size, size per file, version complexity, metadata completeness, release recency) |
| **Graph Embeddings** | 128 | HAN-based dependency relationship representations using two-layer GAT network trained with norm minimization loss |
| **API Behaviors** | 1768 | BERT semantic embeddings (768D) + bag-of-APIs frequency vectors (1000D) |

### Data Statistics

- **Total Packages**: 23,764 (balanced through stratified upsampling from 20,798 initial samples)
- **Class Distribution**: 50% benign (11,882), 50% malicious (11,882)
- **Ecosystems**: PyPI and npm packages with unified representation
- **Dependency Graph**: 20,968 nodes, 67,847 edges capturing cross-ecosystem relationships
- **API Processing**: Over one million source files processed for behavioral analysis

### Feature Engineering Pipeline

1. **Static Metadata Processing**: Z-score normalization of numerical features and categorical encoding
2. **Dependency Graph Construction**: Directed graphs from setup.py and package.json manifests
3. **HAN Embedding Training**: 128-dimensional structural representations via two-layer GAT with Adam optimizer (100 epochs, LR=5×10⁻³)
4. **API Sequence Processing**: BERT-based semantic encoding + bag-of-APIs frequency analysis
5. **Multimodal Fusion**: Horizontal concatenation into unified 1905D vectors

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
print(f"Feature dimensions: {features.shape[1]}")  # Should be 1905
print(f"Class distribution: {np.bincount(labels)}")  # Should be [11882, 11882]
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
├── examples/
│   ├── load_dataset.py                    # Data loading examples
│   └── baseline_models.py                 # Example model implementations
└── README.md
```

## Research Applications

### Primary Use Cases

- **Cross-Ecosystem Malware Detection**: Unified threat identification across PyPI and npm
- **Feature Engineering Research**: Advanced multimodal fusion techniques
- **Graph Learning Studies**: Dependency relationship modeling using HAN
- **Transfer Learning**: Cross-platform generalization studies
- **Baseline Development**: Comprehensive feature set for model comparison

### Suitable Detection Models

The CLAMPD-1905 dataset's 1905-dimensional unified feature representation makes it suitable for various machine learning approaches:

**Traditional Machine Learning**:
- Random Forest, SVM, XGBoost for baseline comparisons
- Ensemble methods for robust cross-ecosystem detection

**Deep Learning Architectures**:
- Convolutional Neural Networks (CNNs) for spatial feature pattern detection
- Recurrent Neural Networks (LSTM/GRU) for sequential behavioral analysis
- Transformer-based models (RoBERTa, BERT variants) for semantic understanding

**Specialized Architectures**:
- Graph Neural Networks for dependency relationship modeling
- Attention mechanisms for adaptive feature weighting
- Multimodal fusion networks for integrated threat detection
- Meta-learning approaches for cross-ecosystem generalization

**Advanced Techniques**:
- Adversarial training for robustness evaluation
- Federated learning for distributed threat detection
- Continual learning for evolving threat adaptation

## Data Quality Assurance

- **Completeness Check**: >99% feature availability across all modalities
- **Label Verification**: Manual validation of threat classifications from MalwareBench
- **Consistency Validation**: Cross-ecosystem format standardization
- **Reproducibility**: Deterministic feature extraction pipeline with fixed random seeds
- **Balance Verification**: Stratified upsampling ensures perfect 50/50 class distribution

## Comparison with Existing Datasets

| Dataset | Ecosystems | Size | Multimodal | Balanced | Graph Features | Semantic API |
|---------|------------|------|------------|----------|----------------|--------------|
| **CLAMPD-1905** | PyPI + npm | 23.7K | ✓ | ✓ | ✓ | ✓ |
| [MalwareBench](https://dl.acm.org/doi/10.1145/3643991.3644883) | PyPI + npm | 20.8K | ✗ | ✗ | ✗ | ✗ |
| [PackageIntel](https://arxiv.org/abs/2409.15049) | PyPI + npm | 37.0K | ✓ | ✗ | ✓ | ✓ |
| [PypiGuard](https://github.com/tahir-biit/PyPiGuard) | PyPI only | 6.7K | Partial | ✗ | ✗ | ✓ |
| [QUT-DV25](https://arxiv.org/abs/2505.13804) | PyPI only | 14.3K | ✗ | ✗ | ✗ | ✗ |
| [Bad Snakes](https://doi.org/10.1109/ICSE48619.2023.00052) | PyPI only | 13.4K | ✗ | ✗ | ✗ | ✗ |

## Citation

```bibtex
@article{iqbal2025clampd,
  title={CLAMPD-Net: Cross-Language Malicious Package Detection for Software Supply Chain Security across PyPI and NPM Ecosystems},
  author={Iqbal, Tahir and Wu, Guowei and Iqbal, Zahid},
  journal={IEEE Transactions on Software Engineering},
  year={2025},
  note={Under Review}
}
```

## Technical Details

### Static Metadata (9 Features)
- **Ecosystem**: Source repository identifier (PyPI/npm)
- **Artifact ID**: Package identifier with missing value handling
- **Threat Type**: Binary malicious/benign classification
- **File Count**: Number of source files (Z-score normalized)
- **Package Size**: Total file size in bytes (Z-score normalized)
- **Size per File**: Content density indicator (derived feature)
- **Version Complexity**: Version component count (Z-score normalized)
- **Metadata Completeness**: Optional field completion ratio
- **Release Recency**: Days since last update (log-transformed, Z-score normalized)

### Graph-Based Dependencies (128 Features)
- **Construction**: Directed graphs from setup.py and package.json manifests
- **Topology**: 20,968 nodes, 67,847 edges spanning both ecosystems
- **Node Features**: Normalized metadata-based attributes
- **HAN Training**: Two-layer GAT with multi-head attention
- **Optimization**: Adam optimizer, 100 epochs, learning rate 5×10⁻³

### Behavioral API Representation (1768 Features)
- **Bag-of-APIs**: 1000-dimensional frequency vectors from top API tokens
- **Semantic Embeddings**: 768-dimensional BERT [CLS] token representations
- **Source Processing**: AST traversal (Python) + regex patterns (JavaScript/TypeScript)
- **Scale**: Over 1 million source files processed

## Contact

**Tahir Iqbal**  
📧 tahir.biit@gmail.com | tahir@mail.dlut.edu.cn  
🏛️ Dalian University of Technology, School of Software Technology

**Guowei Wu** (Corresponding Author)  
📧 guowei@dlut.edu.cn  
🏛️ Dalian University of Technology, School of Software Technology

## License

This dataset is released under the MIT License. See `LICENSE` file for details.

---

**Note**: This dataset is provided for research purposes. Users are responsible for ensuring ethical use and compliance with applicable regulations.
