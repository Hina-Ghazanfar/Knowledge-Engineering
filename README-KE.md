# Knowledge Engineering — Ontology & Knowledge Graph Pipeline

![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-blue)
![Python](https://img.shields.io/badge/Python-3.9%2B-green)
![owlready2](https://img.shields.io/badge/Ontology-owlready2-9cf)
![NetworkX](https://img.shields.io/badge/Graphs-NetworkX-ff69b4)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

This repository contains **`Knowledge_Engineering_code.ipynb`**, a practical notebook for **knowledge engineering**. It demonstrates how to:
- Build and extend an **OWL ontology** with **owlready2**
- Construct a **knowledge graph** from tabular sources (CSV/TSV) and existing OWL files
- Perform **lightweight reasoning** (inferring classes/relations) where applicable
- Visualize graphs and clusters with **NetworkX** and **d3graph**
- (Optional) Explore **probabilistic modeling** of relationships with **PyMC**

The notebook references several example files (e.g., `primekg/*.csv`, `.tsv`, `.owl`), which you can replace with your own domain data.

---

## Repository Structure

```
.
├── Knowledge_Engineering_code.ipynb
├── data/
│   ├── primekg/                # place PrimeKG-style CSV/TSV here (edges, nodes, mappings)
│   ├── ontologies/             # input OWL/TTL files you want to load/merge
│   └── exports/                # notebook will write derived OWL/CSV/plots here
├── requirements.txt
├── .gitignore
└── README.md
```

> **Note:** All local datasets/OWL files should live under `data/`. The folder is Git-ignored to avoid committing private data.

---

## Getting Started

### 1) Clone and create a virtual environment
```bash
git clone <YOUR_REPO_URL>.git
cd <YOUR_REPO_NAME>

python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows (PowerShell)
# .venv\Scripts\Activate.ps1

pip install -r requirements.txt
```

### 2) Add your data
Populate `data/` with the resources you plan to use, for example:
```
data/ontologies/kgd_ontology_with_sources_and_targets.owl
data/primekg/edges.csv
data/primekg/nodes.tsv
data/drugs.csv
data/diseases.csv
```
Update any file paths in the data-loading cells if your layout differs.

### 3) Launch Jupyter
```bash
jupyter lab
# or
jupyter notebook
```
Open **`Knowledge_Engineering_code.ipynb`** and run the cells sequentially.

---

## Workflow Overview

### Ontology authoring (OWL)
- Load base ontologies via `owlready2.get_ontology(...).load()`
- Programmatically define classes, object/data properties, and individuals
- Assert relationships and save updated ontologies (e.g., `onto.save(...)`)

### Knowledge graph construction
- Read tabular sources (CSV/TSV) with `pandas`
- Build a graph in **NetworkX** (nodes, edges, attributes)
- Compute graph statistics (degree, centrality) and export snapshots

### Reasoning (optional)
- Use owlready2's reasoning helpers (e.g., `sync_reasoner`) to infer new facts
- Persist inferred axioms into a derived ontology file

> Reasoning may require a Java-based reasoner; see owlready2 docs for platform setup.

### Visualization
- Plot network structure with **NetworkX**
- Use **d3graph** for interactive 2D layouts

### Probabilistic modeling (optional)
- If enabled, use **PyMC** to estimate uncertainty in relationships
- Keep these steps optional for environments without advanced compilers

---

## Reproducibility & Tips
- Set seeds for any randomized routines to ensure repeatability
- Keep paths relative (`data/...`) so the repo stays portable
- Consider exporting intermediate artifacts to `data/exports/`

---

## Requirements

Install with:
```bash
pip install -r requirements.txt
```

Core dependencies used in the notebook:
- `pandas`, `numpy`
- `networkx`, `matplotlib`
- `owlready2`
- `d3graph`
- `pgmpy` (if you explore PGM structures)
- `pymc` (optional; for probabilistic modeling)
- `tqdm`
- `scipy`
- `jupyter`

> **Graphviz note:** If you add explicit Graphviz rendering, you'll need the system package (`graphviz`) plus the Python wrapper (`graphviz`). This notebook currently relies on NetworkX/d3graph for visualization.

---

## License
Add your preferred license (MIT/Apache-2.0/BSD-3-Clause) and include a `LICENSE` file.

## Acknowledgements
- owlready2, NetworkX, pandas, numpy communities
- d3graph maintainers for interactive graph layouts
- PyMC and pgmpy teams for probabilistic modeling tooling

---

**Maintainer tips**  
Clear notebook outputs before committing to keep diffs tidy:
```bash
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace Knowledge_Engineering_code.ipynb
```
Pin versions in `requirements.txt` for stable builds.
