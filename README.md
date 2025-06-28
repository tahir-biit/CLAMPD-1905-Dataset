# CLAMPD-1905: Cross-Language Malicious Package Detection Dataset

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python" alt="Python">
  <img src="https://img.shields.io/badge/Research-Academic-red?style=flat-square" alt="Academic">
  <img src="https://img.shields.io/badge/Status-Active-success?style=flat-square" alt="Status">
</p>

---

## 🌟 Overview

**CLAMPD-1905** represents a significant advancement in cross-language malicious package detection research. This meticulously curated dataset addresses the critical need for unified, standardized evaluation of malware detection tools across diverse software supply chain ecosystems. Built upon packages from [MalwareBench](https://github.com/MalwareBench), CLAMPD-1905 provides the first comprehensive collection of **23,764 balanced software packages** from both PyPI and npm repositories, each encoded as sophisticated **1905-dimensional feature vectors** through advanced multimodal fusion techniques.

This comprehensive dataset addresses a critical gap in software supply chain security research by providing the first large-scale, balanced collection that combines PyPI and npm packages with sophisticated feature representations. The unified approach eliminates ecosystem-specific preprocessing requirements and facilitates reproducible cross-ecosystem research, making it a valuable resource for advancing malicious package detection capabilities.

The dataset employs sophisticated feature engineering to create comprehensive package representations through three main components: static metadata (9 dimensions) captures essential package characteristics through normalized numerical features and categorical encodings; dependency relationships (128 dimensions) are modeled using graph neural networks trained on manifests from both ecosystems; and behavioral analysis (1768 dimensions) processes over one million source files to extract API usage patterns, combining frequency-based representations with semantic embeddings from transformer models. This multimodal approach results in unified 1905-dimensional vectors that preserve both structural and behavioral information while enabling consistent analysis across different programming language ecosystems.

### Key Features

- **Cross-Ecosystem Coverage**: First dataset to provide unified feature representation across PyPI and npm
- **Multimodal Feature Integration**: Combines normalized metadata, HAN dependency graph embeddings, and BERT API behavioral features
- **Perfect Class Balance**: 23,764 packages with equal distribution of benign and malicious samples (11,882 each)
- **Advanced Feature Engineering**: 1905-dimensional vectors through sophisticated multimodal fusion
- **Research Ready**: Standardized format for immediate model training and evaluation
- **Reproducible**: Complete feature engineering pipeline and pre-computed embeddings
- **Comprehensive Representation**: Captures structural, behavioral, and contextual package characteristics

## Dataset Construction

CLAMPD-1905 is constructed through a comprehensive Cross-Language Unified Feature Fusion Framework that transforms packages from MalwareBench into sophisticated 1905-dimensional feature representations. Starting with 20,798 initial samples from PyPI and npm ecosystems, we apply stratified upsampling to achieve perfect class balance, resulting in 23,764 packages (11,882 benign, 11,882 malicious).

Our construction process follows three parallel processing streams: static metadata preprocessing handles package characteristics like file counts, sizes, and ecosystem identifiers; dependency graph construction extracts relationships from setup.py and package.json manifests to create a unified graph with 20,968 nodes and 67,847 edges; and behavioral API sequence modeling processes source files using AST traversal for Python and regex patterns for JavaScript/TypeScript. The final step fuses these representations through horizontal concatenation into unified 1905-dimensional vectors.

**Referenced Works**:
- **[MalwareBench](https://dl.acm.org/doi/10.1145/3643991.3644883)**: Source of labeled packages from PyPI and npm ecosystems
- **[Backstabber's Knife Collection](https://link.springer.com/chapter/10.1007/978-3-030-52683-2_2)**: Foundational research on open-source supply chain attacks
- **[PyPiGuard](https://github.com/tahir-biit/PyPiGuard)**: PyPI package analysis and detection framework

### Dataset Characteristics

The dataset includes both malicious and benign packages with comprehensive annotations. Malicious packages are designed to carry out harmful actions threatening system security, while benign packages show no discovered malware or suspicious patterns. Each package provides extensive metadata including identifiers, version information, ecosystem classification, file statistics, dependency relationships, and behavioral indicators.

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

The CLAMPD-1905 dataset provides a rich 1905-dimensional feature space that enables researchers to explore various machine learning paradigms for enhanced malicious package detection. The unified representation supports traditional approaches like Random Forest and SVM for establishing baselines, while the multimodal nature makes it particularly well-suited for deep learning architectures including CNNs, RNNs, and transformer models. The dataset's comprehensive feature engineering—combining metadata, graph embeddings, and behavioral patterns—creates opportunities for developing sophisticated detection systems that can generalize effectively across different package ecosystems and adapt to evolving threat landscapes.

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

*Citation will be available upon publication.*

## Contact

**Tahir Iqbal**  
📧 tahir.biit@gmail.com | tahir@mail.dlut.edu.cn  
🏛️ Dalian University of Technology, School of Software Technology

**Guowei Wu**  
📧 guowei@dlut.edu.cn  
🏛️ Dalian University of Technology, School of Software Technology

## License

This dataset is released under the MIT License. See `LICENSE` file for details.

---

**Note**: This dataset is provided for research purposes. Users are responsible for ensuring ethical use and compliance with applicable regulations.
