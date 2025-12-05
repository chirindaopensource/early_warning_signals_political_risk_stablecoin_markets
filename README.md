# `README.md`

# On-Chain Behavioral Pre-Emption System (OBPS): Early-Warning Signals of Political Risk in Stablecoin Markets

<!-- PROJECT SHIELDS -->
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/)
[![arXiv](https://img.shields.io/badge/arXiv-2512.00893-b31b1b.svg)](https://arxiv.org/abs/2512.00893)
[![Journal](https://img.shields.io/badge/Journal-Quantitative%20Finance%20(q--fin.ST)-003366)](https://arxiv.org/abs/2512.00893)
[![Year](https://img.shields.io/badge/Year-2025-purple)](https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets)
[![Discipline](https://img.shields.io/badge/Discipline-Econophysics%20%7C%20Blockchain%20Analytics-00529B)](https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets)
[![Data Sources](https://img.shields.io/badge/Data-Ethereum%20Blockchain%20(ERC--20)-lightgrey)](https://etherscan.io/)
[![Data Sources](https://img.shields.io/badge/Data-Google%20BigQuery%20Crypto-lightgrey)](https://cloud.google.com/blog/products/data-analytics/introducing-six-new-cryptocurrencies-in-bigquery-public-datasets-and-how-to-analyze-them)
[![Data Sources](https://img.shields.io/badge/Data-CoinGecko%20%2F%20CEX%20Data-lightgrey)](https://www.coingecko.com/)
[![Core Method](https://img.shields.io/badge/Method-Bai--Perron%20Structural%20Breaks%20%7C%20Hilbert--Huang%20Transform-orange)](https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets)
[![Analysis](https://img.shields.io/badge/Analysis-Structural%20VAR%20%7C%20AAFT%20Surrogates-red)](https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Type Checking: mypy](https://img.shields.io/badge/type%20checking-mypy-blue)](http://mypy-lang.org/)
[![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)](https://numpy.org/)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![SciPy](https://img.shields.io/badge/SciPy-%230C55A5.svg?style=flat&logo=scipy&logoColor=white)](https://scipy.org/)
[![Statsmodels](https://img.shields.io/badge/statsmodels-blue.svg)](https://www.statsmodels.org/)
[![PyYAML](https://img.shields.io/badge/PyYAML-gray?logo=yaml&logoColor=white)](https://pyyaml.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-%23F37626.svg?style=flat&logo=Jupyter&logoColor=white)](https://jupyter.org/)

**Repository:** `https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets`

**Owner:** 2025 Craig Chirinda (Open Source Projects)

This repository contains an **independent**, professional-grade Python implementation of the research methodology from the 2025 paper entitled **"Early-Warning Signals of Political Risk in Stablecoin Markets: Human and Algorithmic Behavior Around the 2024 U.S. Election"** by:

*   Kundan Mukhia
*   Buddha Nath Sharma
*   Salam Rabindrajit Luwang
*   Md. Nurujjaman
*   Chittaranjan Hens
*   Suman Saha
*   Tanujit Chakraborty

The project provides a complete, end-to-end computational framework for replicating the paper's findings. It delivers a modular, auditable, and extensible pipeline that executes the entire research workflow: from rigorous on-chain data validation and behavioral topology classification to advanced structural break detection, non-linear signal processing via Hilbert-Huang Transform, and regime-dependent Structural Vector Autoregression (SVAR) analysis.

## Table of Contents

- [Introduction](#introduction)
- [Theoretical Background](#theoretical-background)
- [Features](#features)
- [Methodology Implemented](#methodology-implemented)
- [Core Components (Notebook Structure)](#core-components-notebook-structure)
- [Key Callable: `run_obps_pipeline`](#key-callable-run_obps_pipeline)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Input Data Structure](#input-data-structure)
- [Usage](#usage)
- [Output Structure](#output-structure)
- [Project Structure](#project-structure)
- [Customization](#customization)
- [Contributing](#contributing)
- [Recommended Extensions](#recommended-extensions)
- [License](#license)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)

## Introduction

This project provides a Python implementation of the analytical framework presented in Mukhia et al. (2025). The core of this repository is the iPython Notebook `early_warning_signals_political_risk_stablecoin_markets_draft.ipynb`, which contains a comprehensive suite of functions to replicate the paper's findings. The pipeline is designed to be a generalizable toolkit for detecting and quantifying the transmission of political uncertainty into cryptocurrency markets.

The paper addresses the challenge of identifying early-warning signals of market stress by distinguishing between human-driven peer-to-peer stablecoin transactions and automated algorithmic activity. This codebase operationalizes the paper's framework, allowing users to:
-   Rigorously validate and manage the entire experimental configuration via a single `config.yaml` file.
-   Process raw ERC-20 transaction logs to isolate **Human (EOA-EOA)** and **Algorithmic (SC-SC)** flows.
-   Implement **Bai-Perron Structural Break Detection** using dynamic programming to identify endogenous regime shifts in transaction volumes.
-   Apply **Empirical Mode Decomposition (EMD)** and **Hilbert Spectral Analysis** to detect non-linear extreme volatility events in BTC and ETH prices.
-   Execute **Structural Vector Autoregression (SVAR)** with Cholesky identification to quantify volatility spillovers between stablecoins (USDT/USDC).
-   Validate findings using **Amplitude-Adjusted Fourier Transform (AAFT)** surrogates and **Wald statistics** for regime comparison.
-   Automatically generate a comprehensive synthesis report confirming the "early warning" property of human on-chain flows.

## Theoretical Background

The implemented methods are grounded in econophysics, time-series econometrics, and blockchain analytics.

**1. Behavioral Topology Classification:**
The core differentiation strategy relies on the Ethereum Account Model.
-   **Human Signal (EOA-EOA):** Transactions where both sender and receiver are Externally Owned Accounts (controlled by private keys). This captures direct human sentiment and precautionary hedging.
-   **Algorithmic Signal (SC-SC):** Transactions involving Smart Contracts, reflecting automated arbitrage, DeFi protocols, and bot activity.

**2. Structural Break Detection:**
The pipeline uses the Bai-Perron methodology to estimate unknown break dates $T_1, \dots, T_m$ in a mean-shift model $y_t = \mu_j + u_t$. The optimal partition is found by minimizing the global Sum of Squared Residuals (SSR) via dynamic programming:
$$ \{\hat{T}_1, \dots, \hat{T}_m\} = \arg \min_{(T_1, \dots, T_m)} SSR(T_1, \dots, T_m) $$

**3. Non-Linear Signal Processing:**
To analyze non-stationary price dynamics, the Hilbert-Huang Transform is used:
-   **EMD:** Decomposes the signal into Intrinsic Mode Functions (IMFs).
-   **Hilbert Spectrum:** Computes instantaneous energy $IE(t) = \int H^2(t, \omega) d\omega$.
-   **Extreme Events:** Identified when $IE(t) > E_\mu + 4\sigma$.

**4. Structural VAR:**
Volatility spillovers are modeled using a regime-dependent SVAR:
$$ A_0 u_t = \varepsilon_t \implies \Sigma_u = A_0^{-1} (A_0^{-1})' $$
Identification is achieved via Cholesky decomposition, and regime shifts are tested using the Wald statistic.

Below is a diagram which summarizes the proposed approach:

<div align="center">
  <img src="https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets/blob/main/early_warning_signals_political_risk_stablecoin_markets_summary.png" alt="OBPS Process Summary" width="100%">
</div>

## Features

The provided iPython Notebook (`early_warning_signals_political_risk_stablecoin_markets_draft.ipynb`) implements the full research pipeline, including:

-   **Modular, Multi-Task Architecture:** The entire pipeline is broken down into 32 distinct, modular tasks, each with its own orchestrator function.
-   **Configuration-Driven Design:** All study parameters are managed in an external `config.yaml` file.
-   **Rigorous Data Validation:** A multi-stage validation process checks the schema, content integrity, and temporal consistency of blockchain and market data.
-   **Advanced Econometrics:** Integrates `statsmodels` for ADF tests and VAR estimation, and custom `numpy`/`scipy` implementations for Bai-Perron DP and EMD.
-   **Robustness Verification:** Includes automated AAFT surrogate generation (1000 iterations) to validate the statistical significance of all detected breaks and events.
-   **Reproducible Artifacts:** Generates structured dataclasses for every intermediate result, ensuring full auditability.

## Methodology Implemented

The core analytical steps directly implement the methodology from the paper:

1.  **Validation & Preprocessing (Tasks 1-9):** Ingests raw chain logs, validates schemas, filters by time/status, normalizes values to USD, deduplicates, and classifies topology.
2.  **Market Data Processing (Tasks 10-11):** Cleanses exchange data and extracts aligned price/volume series.
3.  **Panel Construction (Tasks 12-15):** Merges datasets, applies log-transformations, tests stationarity (ADF), and differences I(1) series.
4.  **Structural Break Analysis (Tasks 16-21):** Executes Bai-Perron detection on EOA, SC, and Exchange series, validated by AAFT surrogates.
5.  **HHT Analysis (Tasks 22-26):** Performs EMD and Hilbert Spectral Analysis on BTC/ETH prices to detect extreme volatility events.
6.  **SVAR Analysis (Tasks 27-31):** Estimates regime-dependent VAR models, identifies structural shocks via Cholesky, and performs Wald tests for parameter stability.
7.  **Synthesis (Task 32):** Aggregates all findings and validates them against the expected empirical results (e.g., Nov 3 human signal vs. Nov 5 election).

## Core Components (Notebook Structure)

The `early_warning_signals_political_risk_stablecoin_markets_draft.ipynb` notebook is structured as a logical pipeline with modular orchestrator functions for each of the 32 major tasks. All functions are self-contained, fully documented with type hints and docstrings, and designed for professional-grade execution.

## Key Callable: `run_obps_pipeline`

The project is designed around a single, top-level user-facing interface function:

-   **`run_obps_pipeline`:** This master orchestrator function, located in the final section of the notebook, runs the entire automated research pipeline from end-to-end. A single call to this function reproduces the entire computational portion of the project, managing data flow between all 32 sub-tasks.

## Prerequisites

-   Python 3.9+
-   Core dependencies: `pandas`, `numpy`, `pyyaml`, `scipy`, `statsmodels`.

## Installation

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets.git
    cd early_warning_signals_political_risk_stablecoin_markets
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install Python dependencies:**
    ```sh
    pip install pandas numpy pyyaml scipy statsmodels
    ```

## Input Data Structure

The pipeline requires two primary DataFrames:
1.  **`df_chain_raw`**: ERC-20 transfer logs with columns: `timeStamp`, `tokenAddress`, `from`, `to`, `value`, `fromIsContract`, `toIsContract`, `transactionHash`, `blockNumber`, `logIndex`, `txStatus`.
2.  **`df_market_raw`**: Exchange OHLCV data with columns: `Date`, `Symbol`, `Close`, `Volume`.

## Usage

The `early_warning_signals_political_risk_stablecoin_markets_draft.ipynb` notebook provides a complete, step-by-step guide. The primary workflow is to execute the final cell of the notebook, which demonstrates how to use the top-level `run_obps_pipeline` orchestrator:

```python
# Final cell of the notebook

# This block serves as the main entry point for the entire project.
if __name__ == '__main__':
    # 1. Load the master configuration from the YAML file.
    with open('config.yaml', 'r') as f:
        study_config = yaml.safe_load(f)
    
    # 2. Load raw datasets (Example using synthetic generator provided in the notebook)
    # In production, load from CSV/Parquet: pd.read_csv(...)
    df_chain_raw = ... 
    df_market_raw = ...
    
    # 3. Execute the entire replication study.
    results = run_obps_pipeline(
        df_chain_raw=df_chain_raw,
        df_market_raw=df_market_raw,
        study_config=study_config
    )
    
    # 4. Access results
    print(f"Conclusion: {results.final_report.overall_conclusion}")
```

## Output Structure

The pipeline returns an `OBPSPipelineResult` object containing all analytical artifacts:
-   **`config`**: Validated configuration object.
-   **`final_panel`**: The processed econometric panel DataFrame.
-   **`structural_breaks`**: Dictionary of detected break dates and SupF statistics.
-   **`break_robustness`**: AAFT p-values for structural breaks.
-   **`hht_analysis`**: Hilbert Spectra and detected extreme event dates.
-   **`svar_model`**: Full-sample VAR estimation results.
-   **`svar_regimes`**: Pre- and Post-election VAR models.
-   **`svar_identification`**: Structural impact matrices (Cholesky factors).
-   **`wald_test`**: Wald statistic for regime shift significance.
-   **`final_report`**: A synthesis object comparing observed results to expected findings.

## Project Structure

```
early_warning_signals_political_risk_stablecoin_markets/
│
├── early_warning_signals_political_risk_stablecoin_markets_draft.ipynb  # Main implementation notebook
├── config.yaml                                                          # Master configuration file
├── requirements.txt                                                     # Python package dependencies
│
├── LICENSE                                                              # MIT Project License File
└── README.md                                                            # This file
```

## Customization

The pipeline is highly customizable via the `config.yaml` file. Users can modify study parameters such as:
-   **Observation Window:** `start_date`, `end_date`.
-   **Bai-Perron Settings:** `max_breaks`, `trimming_epsilon`.
-   **HHT Settings:** `max_imfs`, `B` (threshold multiplier).
-   **SVAR Settings:** `max_lags`, `break_date`.

## Contributing

Contributions are welcome. Please fork the repository, create a feature branch, and submit a pull request with a clear description of your changes. Adherence to PEP 8, type hinting, and comprehensive docstrings is required.

## Recommended Extensions

Future extensions could include:
-   **Real-Time Monitoring:** Adapting the pipeline for streaming blockchain data.
-   **Multi-Chain Support:** Extending the analysis to other EVM-compatible chains (Polygon, Arbitrum).
-   **Machine Learning Integration:** Incorporating LSTM or Transformer models for predictive signaling.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Citation

If you use this code or the methodology in your research, please cite the original paper:

```bibtex
@article{mukhia2025earlywarning,
  title={Early-Warning Signals of Political Risk in Stablecoin Markets: Human and Algorithmic Behavior Around the 2024 U.S. Election},
  author={Mukhia, Kundan and Sharma, Buddha Nath and Luwang, Salam Rabindrajit and Nurujjaman, Md. and Hens, Chittaranjan and Saha, Suman and Chakraborty, Tanujit},
  journal={arXiv preprint arXiv:2512.00893},
  year={2025}
}
```

For the implementation itself, you may cite this repository:
```
Chirinda, C. (2025). On-Chain Behavioral Pre-Emption System (OBPS): An Open Source Implementation.
GitHub repository: https://github.com/chirindaopensource/early_warning_signals_political_risk_stablecoin_markets
```

## Acknowledgments

-   Credit to **Kundan Mukhia et al.** for the foundational research that forms the entire basis for this computational replication.
-   This project is built upon the exceptional tools provided by the open-source community. Sincere thanks to the developers of the scientific Python ecosystem, including **Pandas, NumPy, SciPy, and Statsmodels**.

--

*This README was generated based on the structure and content of the `early_warning_signals_political_risk_stablecoin_markets_draft.ipynb` notebook and follows best practices for research software documentation.*
