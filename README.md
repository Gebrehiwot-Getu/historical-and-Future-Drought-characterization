# Historical Characterization and LightGBM-Based Future Projection of Agricultural Drought under CMIP6 Scenarios in Tekeze Basin, North Ethiopia

This repository contains all Python scripts used in the analysis and visualization
for the manuscript submitted for peer review.

---

## Author

**Gebrehiwot G. Kassie**
📧 ggetu9552@gmail.com

---

## Repository Structure
├── 01_drought_indices/          # SPI, SPEI, VCI, TCI, VHI, CDI computation
├── 02_bias_correction/          # Random Forest bias correction for CMIP6 PR and TA
├── 03_lgbm_model/               # LightGBM model training, evaluation, and prediction
├── 04_future_projection/        # Future CDI projection (2030–2050) SSP2-4.5 and SSP5-8.5
├── 05_visualization/            # All figures, maps, and graphical abstract scripts
└── README.md

---

## Study Overview

This study characterizes historical agricultural drought patterns (2000–2025)
and projects future drought dynamics (2030–2050) in the Tekeze Basin, North
Ethiopia, using a multi-index approach and the Light Gradient Boosting Machine
(LightGBM) algorithm. Five drought indices — SPI, SPEI, VCI, TCI, and VHI —
are integrated into a single Combined Drought Index (CDI), which serves as
the target variable for the LightGBM model trained on CHIRPS precipitation
and ERA5 temperature inputs. Future projections are generated using
bias-corrected CMIP6 climate outputs under SSP2-4.5 and SSP5-8.5 emission
scenarios.

---

## Data Sources

| Dataset | Variable | Period | Source |
|---|---|---|---|
| CHIRPS v2.0 | Precipitation | 2000–2025 | chirps.ucsb.edu |
| ERA5-Land | Mean temperature | 2000–2025 | Copernicus Climate Data Store |
| MODIS MOD13A3 | NDVI | 2000–2025 | NASA Earthdata |
| MODIS MOD11A2 | Land surface temperature | 2000–2025 | NASA Earthdata |
| NEX-GDDP-CMIP6 GFDL-CM4 | Future precipitation | 2030–2050 | NASA NEX |
| NEX-GDDP-CMIP6 INM-CM5-0 | Future temperature | 2030–2050 | NASA NEX |

---

## Key Dependencies

```bash
pip install numpy pandas rasterio geopandas lightgbm scikit-learn
pip install matplotlib scipy pillow xarray pyproj shapely
```

Python version: 3.9 or higher recommended.

---

## Workflow Summary
Step 1 — Drought Index Computation
CHIRPS + ERA5 + MODIS → SPI | SPEI | VCI | TCI | VHI → CDI
Step 2 — LightGBM Model Training
CHIRPS (PR) + ERA5 (TA) + Month → CDI
Training: 70% | Testing: 30% | Samples: 42,607
Step 3 — CMIP6 Bias Correction
Random Forest correction:
GFDL-CM4   → Precipitation
INM-CM5-0  → Temperature
Step 4 — Future CDI Projection (2030–2050)
Bias-corrected PR + TA → LightGBM → CDI maps
Scenarios: SSP2-4.5 | SSP5-8.5
Step 5 — Analysis and Visualization
Spatial maps | Seasonal analysis | Time series | Graphical abstract

---

## LightGBM Model Performance

| Phase | R² | RMSE | MAE | NSE | PBIAS |
|---|---|---|---|---|---|
| Training | 0.98 | 0.27 | 0.21 | 0.98 | −0.02% |
| Testing | 0.97 | 0.29 | 0.22 | 0.97 | 0.15% |

Overfitting gap (Train R² − Test R²): **0.005**
Best iteration (early stopping): **93 boosting rounds**

---

## LightGBM Hyperparameters

| Parameter | Value |
|---|---|
| Boosting type | gbdt |
| Number of leaves | 127 |
| Learning rate | 0.05 |
| Maximum boosting rounds | 1000 |
| Early stopping rounds | 50 |
| Row subsampling | 0.8 |
| L1 / L2 regularization | 0.01 / 1.0 |
| Minimum samples per leaf | 20 |

---

## Key Results

- Basin-wide drought-affected area (CDI < −0.5) ranged from **7.63%** (2024)
  to **100%** (2009) over the historical period.
- LightGBM achieved R² = 0.97 on unseen test data with negligible overfitting.
- Precipitation was identified as the dominant predictor of CDI,
  substantially outweighing mean temperature.
- Under SSP2-4.5, drought-affected area peaked at **99.32%** in 2030.
- Under SSP5-8.5, drought extent reached **73.97%** by 2050.
- Projected future drought remains confined to the **moderate category**
  under both scenarios — no severe or extreme drought anticipated by 2050.

---

## Citation

If you use these scripts or data in your research, please cite:

> Kassie, G. G. (2025). Historical Characterization and LightGBM-Based Future
> Projection of Agricultural Drought under CMIP6 Scenarios in Tekeze Basin,
> North Ethiopia. *(manuscript under review)*

This section will be updated with full journal citation upon publication.

---

## License

This project is licensed under the **MIT License** — see the LICENSE file for details.

---

## Acknowledgements

The author acknowledges NASA for providing NEX-GDDP-CMIP6 climate data,
the Climate Hazards Group for CHIRPS precipitation data, the Copernicus
Climate Change Service for ERA5-Land reanalysis, and NASA Earthdata for
MODIS satellite products.

---

*Last updated: July 2025*
