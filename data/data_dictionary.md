# Data Dictionary

## Overview

This directory contains the datasets used in the hybrid Prophet-LSTM forecasting protocol for domestic gold prices in Indonesia (GAU/IDR).

The datasets include the target variable and seven exogenous variables used to investigate domestic gold price movements.

## Dataset Description

### 1. GAU_IDR.csv

Target variable representing the domestic gold price in Indonesian Rupiah (IDR). The model uses this variable as the primary forecasting target.

### 2. GAU_USD.csv

Represents the gold price denominated in US dollars. This variable provides information about international gold price movements.

### 3. USD_IDR Historical Data.csv

Contains the USD/IDR exchange rate. This variable captures exchange rate movements that may affect domestic gold prices.

### 4. DXY.csv

Contains the US Dollar Index (DXY), which represents the strength of the US dollar relative to a basket of major currencies.

### 5. FED Rate.csv

Contains the Federal Funds Rate, representing the monetary policy interest rate set by the US Federal Reserve.

### 6. BI Rate.xlsx

Contains the Bank Indonesia policy interest rate. This variable represents domestic monetary policy conditions.

### 7. harga minyak dunia.csv

Contains crude oil price data. This variable represents movements in global energy markets.

### 8. Data Inflasi.xlsx

Contains Indonesian inflation data, representing changes in domestic price levels.

## Data Frequency and Harmonization

The datasets have different observation frequencies. The domestic gold price and financial market variables are collected at daily frequency, while macroeconomic variables may be available at monthly frequency.

To construct a consistent multivariate time series, the datasets are aligned to a daily timeline. Monthly macroeconomic observations are forward-filled across the corresponding daily dates.

Forward-filling carries the latest available observation forward until a new observation becomes available. This procedure does not generate new observed macroeconomic information.

## Data Preprocessing

The preprocessing workflow includes:

1. Loading the individual datasets.
2. Converting date columns into a consistent datetime format.
3. Sorting observations chronologically.
4. Aligning datasets using their date columns.
5. Applying forward-filling to lower-frequency macroeconomic variables.
6. Checking missing values, duplicate dates, and data types.
7. Applying a logarithmic transformation to the target variable when required by the forecasting protocol.

## Forecasting Variables

The target variable is domestic gold price (GAU/IDR).

The seven exogenous variables are:

- GAU/USD
- USD/IDR
- US Dollar Index (DXY)
- Federal Funds Rate
- Bank Indonesia policy rate
- Crude oil price
- Indonesian inflation

These variables are used by the multivariate Prophet baseline and the associated residual-learning framework, subject to the forecasting scenario.

## Forecasting Scenarios

Mode A uses observed exogenous variables during the evaluation period to assess conditional forecasting performance.

Mode B forecasts the exogenous variables using individual Prophet models trained only on data available up to the training cutoff. Actual exogenous observations from the evaluation period are not used to generate Mode B forecasts.

## Data Sources and Availability

The original data files are provided in this directory for reproducibility, subject to the redistribution permissions and terms of their respective sources.

The exact source URLs, units, date ranges, and retrieval dates should be documented for each dataset before publication.

## Limitations

Forward-filling monthly macroeconomic variables to daily frequency does not increase their actual information frequency.

Forecasting results depend on data quality, temporal alignment, model configuration, and the availability of exogenous variables.

Mode A and Mode B represent different forecasting conditions and should be evaluated and interpreted separately.
