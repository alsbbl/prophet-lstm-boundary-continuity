# Prophet-LSTM Residual-Correction Protocol for Gold Price Forecasting

## Overview

This repository provides the computational implementation of a reproducible Prophet-LSTM residual-correction protocol for operational domestic gold price forecasting.

The protocol integrates multivariate Prophet modeling, univariate LSTM residual correction, recursive multi-step forecasting, and boundary-continuity re-anchoring. It uses an example dataset of domestic gold prices (GAU/IDR) and seven exogenous variables.

The repository accompanies the methodological article:

**A Reproducible Prophet-LSTM Residual-Correction Protocol with Boundary-Continuity Re-Anchoring for Operational Domestic Gold Price Forecasting**

## Methodology

The protocol consists of the following stages:

1. Example dataset ingestion and data harmonization.
2. Chronological data preparation and train-test splitting.
3. Multivariate Prophet baseline modeling with seven exogenous regressors.
4. Residual extraction, scaling, and univariate LSTM residual correction.
5. Exogenous variable forecasting using seven univariate Prophet models.
6. Recursive 30-day forecasting and boundary-continuity re-anchoring.
7. Protocol validation and reproducibility auditing.

The hybrid forecast combines the Prophet baseline with the LSTM residual correction using a fixed weighting coefficient of λ = 0.5.

Boundary-continuity re-anchoring applies a constant offset on the log scale to align the forecast boundary with the last observed target value.

## Forecasting Modes

### Mode A: Conditional Evaluation

Mode A evaluates out-of-sample predictions using actual exogenous variables from the evaluation period. This mode provides a conditional assessment and is not an operational forecasting scenario.

### Mode B: Operational Forecasting

Mode B forecasts the seven exogenous variables using separate univariate Prophet models. These forecasts provide the inputs for recursive 30-day operational forecasting without using actual future exogenous values.

The resulting hybrid forecast is adjusted through boundary-continuity re-anchoring.

## Example Dataset

The example dataset contains domestic gold prices and seven exogenous variables:

- GAU/IDR: Domestic gold price, the target variable.
- GAU/USD: Gold price in US dollars.
- USD/IDR: US dollar to Indonesian rupiah exchange rate.
- DXY: US Dollar Index.
- Federal Funds Rate: US monetary policy rate.
- BI Rate: Bank Indonesia policy rate.
- Crude Oil: Crude oil price.
- Indonesian Inflation: Monthly inflation rate.

The dataset includes daily and monthly observations. The protocol harmonizes these frequencies into a daily time series.

See `data/data_dictionary.md` for the dataset descriptions and variable information.

## Repository Structure

```text
prophet-lstm-boundary-continuity/
├── data/
│   ├── GAU_IDR.csv
│   ├── GAU_USD.csv
│   ├── DXY.csv
│   ├── FED Rate.csv
│   ├── BI Rate.xlsx
│   ├── Data Inflasi.xlsx
│   ├── USD_IDR Historical Data.csv
│   ├── harga minyak dunia.csv
│   └── data_dictionary.md
├── notebooks/
│   └── prophet_lstm_forecasting_protocol.ipynb
├── CITATION.cff
├── LICENSE
├── README.md
└── requirements.txt
```

File names above illustrate the intended structure. Ensure they match the actual files in the repository.

## Requirements

The implementation uses Python and the following libraries:

- pandas
- NumPy
- scikit-learn
- Prophet
- TensorFlow/Keras
- Matplotlib
- SciPy
- statsmodels
- openpyxl

Install the dependencies with:

```bash
pip install -r requirements.txt
```

## How to Run

1. Clone or download this repository.
2. Install the required dependencies.
3. Verify that the example dataset files are located in the `data/` directory.
4. Open the Jupyter notebook in `notebooks/`.
5. Run the notebook cells sequentially, from data ingestion through protocol validation.

The notebook and dataset paths must match the repository structure.

## Validation and Reproducibility

The protocol includes checks for:

- Dataset completeness and daily index consistency.
- Chronological separation of training and evaluation periods.
- Training-only fitting of the residual scaler.
- Consistency of model parameters and input dimensions.
- Separation of conditional evaluation and operational forecasting.
- Forecast horizon and boundary continuity.
- Reproducibility of the computational workflow.

The example dataset demonstrates the implementation of the protocol. The reported outputs serve as protocol-validation results and should not be interpreted as evidence of new empirical superiority over alternative models.

## Citation

If you use this repository, please cite the associated methodological article when its publication details become available.

Citation metadata are provided in `CITATION.cff`.

## License

This repository's code and documentation are distributed under the license specified in `LICENSE`. The license does not automatically grant redistribution rights for third-party datasets.
