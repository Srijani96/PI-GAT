# Physics-Informed Graph Learning by Architecture for PV System Modeling

This repository provides the reference implementation (Jupyter notebooks) for the paper:

Beyond Black Boxes: Physics-Informed Graph Learning by Architecture for PV System Modeling

The code implements a Physics-Informed Graph Attention Network with GRU (PI-GAT) for photovoltaic (PV) systems, where physical knowledge is embedded directly into the model architecture via graph structure and physics-informed edge attributes.


## Repository contents

```
.
├── PI-GAT-short-term-power-prediction.ipynb
├── PI-GAT-long-term-power-prediction.ipynb
├── PI-GAT-module-temperature-prediction.ipynb
├── requirements.txt
├── LICENSE
├── .gitignore
└── README.md
```

### Notebook overview

| Notebook                                       | Description                                                                                                                                             |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PI-GAT-short-term-power-prediction.ipynb   | One-year PV power prediction using PI-GAT-GRU, including uncertainty analysis and hybrid anomaly detection (physics-residual + Isolation Forest + LOF). |
| PI-GAT-long-term-power-prediction.ipynb    | Five-year PV power prediction with continual learning and degradation analysis using energy-normalized efficiency and robust regression.                |
| PI-GAT-module-temperature-prediction.ipynb | One-year PV module temperature prediction using the same physics-informed graph architecture, compared against analytical temperature models.           |

All notebooks include figures and plots as generated for the paper.


## Method summary

At each timestamp, the PV system is represented as a three-node physics-informed micro-graph:

* Module node – internal electrical/thermal state
* Environment node – irradiance, ambient temperature, solar geometry
* Thermal node – heat exchange and convective effects

Physics-informed edge attributes (e.g., effective irradiance, thermal gradients, convective coupling proxies) are injected directly into the Graph Attention Network (GAT) attention mechanism, constraining learning to physically meaningful interactions.

A GRU is used for temporal modeling within a sliding-window continual-learning framework, ensuring:

* no future data leakage,
* adaptability to seasonal and long-term changes,
* robustness for operational PV monitoring.

---

## Environment setup

### Recommended Python version

* Python 3.9 or 3.10

### Install dependencies

```bash
pip install -r requirements.txt
```

> Note: `torch-geometric` must match your installed PyTorch and CUDA versions.
> Please follow the official PyTorch Geometric installation guide if needed.

---

## Data availability

Due to institutional and licensing constraints, raw experimental datasets are not included in this repository.

Each notebook contains:

* a clearly marked data loading section,
* documentation of required input variables,
* preprocessing and filtering steps used in the paper.

### Typical required variables

Depending on the notebook, required columns include combinations of:

* Irradiance: `Gsw`
* Temperatures: `T_PV`, `T_air`
* Wind: Wind speed `U`, optionally wind direction `eta`
* Geometry: `cos_theta` (measured or reconstructed from solar incidence angle 'theta')
* Electrical power: `P_actual` / `P_measured`
* Optional (short-term dataset): `q_HFM`, `h_conv`

---

## How to run the notebooks

Launch Jupyter and open the desired notebook:

```bash
jupyter notebook
```

Then run cells top to bottom.

### 1️. Short-term power prediction + anomaly detection

`PI-GAT-short-term-power-prediction.ipynb`

Outputs:

* out-of-sample power predictions,
* hybrid anomaly detection results,
* uncertainty analysis under irradiance and temperature noise,
* performance metrics and figures.

---

### 2️. Long-term power prediction + degradation analysis

`PI-GAT-long-term-power-prediction.ipynb`

Outputs:

* five-year rolling forecasts,
* degradation rate estimation (%/year),
* seasonal MAE analysis,
* long-term performance plots.

---

### 3️. Module temperature prediction

`PI-GAT-module-temperature-prediction.ipynb`

Outputs:

* hourly module temperature predictions,
* comparison against analytical temperature models (e.g., NOCT, SAPM),
* error metrics and visualizations.

---

## Reproducibility notes

* All normalization is performed using training-only statistics within each sliding window.
* Continual learning ensures predictions are always out-of-sample.
* Random seeds are fixed where applicable.
* Notebooks are designed to be run independently.

For exact reproduction of paper figures:

* use the same filtering thresholds,
* avoid skipping cells,
* run notebooks sequentially from the top.

---

## Intended use and scope

This code is intended for:

* physics-informed PV power and temperature modeling,
* long-term performance and degradation analysis,
* robust monitoring and anomaly detection.

The objective is not to compete with purely black-box deep learning models on MAE alone, but to demonstrate how physics-informed learning by architecture enables interpretable, robust, and physically consistent AI for energy systems.

---

## Citation

If you use this code, please cite:

```bibtex
@article{Mukherjee2025PIGNN,
  title   = {Beyond Black Boxes: Physics-Informed Learning by Architecture with Graph Neural Networks for Interpretable PV System Modeling},
  author  = {Mukherjee, S. and Tsanakas, I. and Colin, H. and Pabiou, H. and Dutykh, D. and Vuillon, L.},
  journal = {Energy and AI (submitted)},
  year    = {2025}
}
```

---

## License

This repository is released under the license specified in the `LICENSE` file.

---

## Contact

Srijani Mukherjee
[srijani.mukherjee@univ-smb.fr](mailto:srijani.mukherjee@univ-smb.fr)

---
