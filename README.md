# MasterSet

A large-scale benchmark for **must-cite citation recommendation** in the AI/ML literature.

**Paper:** MasterSet: A Large-Scale Benchmark for Must-Cite Citation Recommendation in the AI/ML Literature — accepted at the 2026 SIAM International Conference on Data Mining (SDM26).

This repository is the entry point for the MasterSet benchmark. It contains the
versioned benchmark split (`data/train_eval_set/v1.0`) and links to all code and
raw data.

---

## Overview

MasterSet evaluates whether a system can retrieve the papers a researcher *must*
cite — experimental baselines, directly extended methods, and core datasets —
given only a paper's title and abstract.

- **153,373 papers** from 15 peer-reviewed venues (NeurIPS, ICML, ICLR, CVPR, ACL, AAAI, and others)
- **2M+ citation instances** annotated with a three-tier labeling scheme
- **MasterSet-CoreML-v1** — a versioned benchmark split (67,761-paper candidate pool)

### Three-Tier Must-Cite Labels

| Tier | Label | Description |
|------|-------|-------------|
| Type I | Experimental Baseline (binary) | Is the cited paper used as a direct comparison baseline? |
| Type II | Core Relevance (1–5) | How central is the cited work to the query paper's task and method? (≥ 4 = must-cite) |
| Type III | Mention Frequency | Is the cited paper mentioned ≥ 3 times in the query paper? |

---

## Code Repositories

The pipeline is split across three repositories, one per stage:

| Repository | Link | Purpose |
|------------|------|---------|
| [OpenPapers](https://github.com/NIU-Graph-Intelligence/OpenPapers) | `https://github.com/NIU-Graph-Intelligence/OpenPapers` | Venue-specific crawlers for collecting papers and metadata from official proceedings |
| [masterset-toolkit](https://github.com/NIU-Graph-Intelligence/masterset-toolkit) | `https://github.com/NIU-Graph-Intelligence/masterset-toolkit` | Reference extraction, citation matching, and the LLM-based annotation pipeline |
| [masterset-benchmark](https://github.com/NIU-Graph-Intelligence/masterset-benchmark) | `https://github.com/NIU-Graph-Intelligence/masterset-benchmark` | Baseline implementations and evaluation code for reproducing all reported results |

---

## Data

The **benchmark split** used for training and evaluation is included directly in
this repository:

```
data/
└── train_eval_set/
    └── v1.0/
        ├── all_papers_with_refs_and_labels.parquet
        ├── train.parquet
        └── eval.parquet
```

```python
import pandas as pd
train = pd.read_parquet("data/train_eval_set/v1.0/train.parquet")
eval_ = pd.read_parquet("data/train_eval_set/v1.0/eval.parquet")
```

The **full raw data** — paper metadata, annotations, and prompt scores — is
hosted on the Hugging Face Hub (too large for GitHub):

**https://huggingface.co/datasets/trratul/MasterSet/tree/main/data**

Consistent with the licensing terms below, we release metadata, citation graphs,
and LLM-generated labels only; source PDFs are not redistributed.

---

## Supported Venues

NeurIPS, ICML, ICLR, AAAI, IJCAI, CVPR, ICCV, ECCV, ACL, EMNLP, NAACL, COLT, UAI,
AISTATS, and JMLR. Coverage begins with the deep-learning era (most venues from
2012–2013 onward).

---

## Citation

If you use MasterSet in your research, please cite:

```bibtex
@inproceedings{ratul2026masterset,
  title     = {{MasterSet}: A Large-Scale Benchmark for Must-Cite Citation Recommendation in the {AI/ML} Literature},
  author    = {Ratul, Md Toyaha Rahman and Chen, Zhiqian and Fu, Kaiqun and Ji, Taoran and Zhang, Lei},
  booktitle = {Proceedings of the 2026 SIAM International Conference on Data Mining (SDM26)},
  year      = {2026},
  url       = {https://arxiv.org/abs/2604.17680}
}
```

The proceedings DOI and page numbers are not available yet; this entry links to
the current preprint and will be updated after publication.

---

## License

Source code across the component repositories is licensed under the MIT License.

The dataset is released under CC BY 4.0. This project does not claim ownership of
paper metadata, abstracts, or PDFs retrieved from public conference and publisher
websites; those materials remain subject to the rights and terms of their
respective authors, publishers, and source websites.