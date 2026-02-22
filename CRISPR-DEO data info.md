# CRISPR-DEO: Power System Data Repository

## Associated Publication

**Paper:** CRISPR-DEO: Decision-Aware Economic Dispatch Optimization via Sparse Gradient Editing for Power System Forecasting  
**Journal:** IEEE Access (2026)  
**Status:** ✅ Accepted for Publication  
**Authors:** Ntebogang Dinah Moroke et al.

---

## 📊 Data Sources

All data used in this study are **publicly accessible** from official South African power system sources:

### Primary Source: Eskom Data Portal
- **URL:** https://www.eskom.co.za/dataportal/
- **Coverage:** January 2015 - December 2025 (87,600 hourly observations)
- **Geographic Scope:** South African national grid (47 generators)

### Data Components

| Component | Description | Source |
|-----------|-------------|--------|
| **System Demand** | Hourly electricity demand (MW) | Eskom System Status Reports |
| **Generator Fleet** | Coal, gas, diesel, hydro, nuclear units | Eskom Generation Dashboard |
| **Renewable Output** | Wind and solar generation (MW) | Renewable Energy Portal |
| **Weather Data** | Temperature, wind speed, dew point | SA Weather Service |
| **Load Shedding** | Stage levels (0-8) | Eskom Loadshedding API |

---

## 🔧 Data Processing

### Variable Descriptions

See [`variable_descriptions.md`](variable_descriptions.md) for detailed definitions of all variables used in the study.

### Preprocessing Pipeline

The `data_preprocessing.py` script provides a complete preprocessing template:

```python
# Example usage
from data_preprocessing import *

# Load raw data
data = load_eskom_data(
    data_dir='./raw_data/',
    start_date='2015-01-01',
    end_date='2025-12-31'
)

# Apply temporal encoding
temporal_features = encode_temporal_features(data.index)

# Compute net load
net_load = compute_net_load(
    demand_MW=data['demand_MW'],
    renewable_MW=data['renewable_MW']
)
```

### Key Transformations

1. **Inverse Distance Weighting** for meteorological variables (Section 3.4 of paper)
2. **Sine-Cosine Encoding** for temporal cyclicity (hour, day, month)
3. **Net Load Calculation**: D_net = D - R (demand minus renewables)
4. **Quantile Forecast Generation** using Temporal Fusion Transformer
5. **CVaR-Constrained Dispatch** with Gurobi solver

---

## 📁 Repository Contents

```
moroke-datasets/
├── README.md                    # This file
├── variable_descriptions.md     # Detailed variable definitions
├── data_preprocessing.py        # Python preprocessing pipeline
├── sample_data.csv             # Sample: First week of January 2015
└── LICENSE                      # MIT License
```

---

## 💻 Requirements

### Software Dependencies

```bash
# Python environment
pip install pandas numpy scipy

# Forecasting (TFT)
pip install pytorch-forecasting torch

# Optimization (CVaR dispatch)
pip install gurobipy cvxpy
```

### Gurobi License

CVaR-constrained dispatch requires Gurobi 10.0+:
- **Academic:** https://www.gurobi.com/academia/
- **Commercial:** https://www.gurobi.com/

### Hardware (for training CRISPR-DEO)

- **GPU:** 4× NVIDIA A100 (80GB) or equivalent
- **CPU:** 128 cores (for asynchronous dispatch)
- **RAM:** 256GB
- **Storage:** ~50GB

---

## 📖 Usage Example

```python
import pandas as pd
from data_preprocessing import encode_temporal_features, compute_net_load

# Load sample data
df = pd.read_csv('sample_data.csv', parse_dates=['timestamp'])

# Add temporal features
temporal = encode_temporal_features(df['timestamp'])
df = pd.concat([df, temporal], axis=1)

# Compute net load
df['net_load_MW'] = compute_net_load(
    df['demand_MW'], 
    df['renewable_MW']
)

print(df.head())
```

---

## 📊 Dataset Characteristics

| Metric | Value |
|--------|-------|
| Time Period | 2015-01-01 to 2025-12-31 |
| Total Observations | 87,600 hours |
| Generators | 47 units (coal, gas, diesel, hydro, nuclear) |
| Renewable Capacity Growth | 5.7× (2015 → 2025) |
| Coal Availability Decline | -19 percentage points |
| Load Shedding Events | 28.5× increase |

---

## 🎯 Reproducibility

To reproduce the results in the IEEE Access paper:

1. **Download data** from Eskom Data Portal (2015-2025)
2. **Run preprocessing**: `python data_preprocessing.py`
3. **Train TFT model** (Section 3.1 of paper)
4. **Solve CVaR dispatch** (Section 2.3 of paper)
5. **Apply sparse gradient editing** (Section 2.4 of paper)

Expected results:
- 14.4% operational cost reduction vs. decoupled approaches
- 39.9% reduction vs. deterministic baselines
- 90% parameter sparsity
- Sub-2-second inference time

---

## 📧 Contact

**Questions about data processing:**  
Ntebo.Moroke@nwu.ac.za

**Issues or contributions:**  
https://github.com/ntebo40/moroke-datasets/issues

---

## 📝 Citation

If you use this data or methodology, please cite:

```bibtex
@article{moroke2026crispr,
  title={CRISPR-DEO: Decision-Aware Economic Dispatch Optimization via 
         Sparse Gradient Editing for Power System Forecasting},
  author={Moroke, Ntebogang Dinah},
  journal={IEEE Access},
  year={2026},
  publisher={IEEE},
  note={Accepted for publication}
}
```

---

## 📜 License

MIT License - See LICENSE file for details.

Data sourced from Eskom Holdings SOC Ltd. is subject to their terms of use.

---

## 🙏 Acknowledgments

- Eskom Holdings SOC Ltd. for publicly accessible operational data
- South African Weather Service for meteorological data
- North-West University for computational resources
- IEEE Access reviewers for constructive feedback

---

**Last Updated:** February 2026  
**Repository:** https://github.com/ntebo40/moroke-datasets
