# Physics-Informed Graph Attention Network (PI-GAT) for PV System Modelling

This repository provides a set of Jupyter notebooks for the paper Mukherjee et. al. "_Beyond Black Boxes: Physics-Informed Graph Learning by Architecture for PV System Modeling_"

The code implements a Physics-Informed Graph Attention Network with GRU (PI-GAT) for PV systems, where physical knowledge is embedded directly into the model architecture via graph structure and physics-informed edge attributes.

### Notebook overview
                                                                                                                          
1. "PI-GAT-short-term-power-prediction.ipynb" : One-year PV power prediction using PI-GAT, including uncertainty analysis and hybrid anomaly detection.
2. "PI-GAT-long-term-power-prediction.ipynb" : Five-year PV power prediction with continual learning and degradation analysis.      
3. "PI-GAT-module-temperature-prediction.ipynb" : One-year PV module temperature prediction using the same physics-informed graph architecture.

**Recommended Python version:** Python 3.9 or 3.10, see ```reqirements.txt``` for a list of python dependencies.

### Typical required variables

Depending on the notebook, required columns include combinations of:

* Irradiance: `Gsw`
* Temperatures: `T_PV`, `T_air`
* Wind: Wind speed `U`, optionally wind direction `eta`
* Incidence angle: `cos_theta` (measured or reconstructed from solar incidence angle 'theta')
* Electrical power: `P_actual` / `P_measured`
* Optional (Temperature modelling): Outgoing heat flux from the PV module `q_HFM`, convective heat transfer coefficient  `h_conv`

This code is intended for physics-informed PV power and temperature modeling, long-term performance and degradation analysis and anomaly detection. The objective is not to compete with purely black-box deep learning models on MAE alone, but to demonstrate how physics-informed learning by architecture enables interpretable, robust, and physically consistent AI for energy systems.

If you use this code, please cite: [TBD]

## Contact

For questions or collaborations, please open an issue or contact srijani.mukherjee@univ-smb.fr
