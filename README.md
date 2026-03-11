## globicus-forecasting-lstm

LSTM neural networks trained on three Federal Reserve economic series to forecast 
one month ahead and produce short-term projections.

## Prerequisites

- Python 3
- The following packages:
  - tensorflow
  - pandas
  - numpy
  - scikit-learn
  - scipy
  - seaborn
  - matplotlib

## Data

All three datasets are included in the repository as CSVs, originally sourced from 
[FRED](https://fred.stlouisfed.org/).

| File | Series | Description |
|---|---|---|
| `PAYEMS.csv` | PAYEMS | Total Nonfarm Payroll Employment |
| `UNRATE.csv` | UNRATE | Unemployment Rate |
| `ACDGNO.csv` | ACDGNO | New Orders for Consumer Goods |

## How It Works

1. The last 12 months of values are used as features to predict the next month
2. Data is scaled using MinMaxScaler fit on the training set
3. An LSTM model is trained on 80% of the data and validated on the remaining 20%
4. The model forecasts 3 months into the future by feeding its own predictions back as input

## Models

All three models share the same architecture with minor differences in learning rate:

| Series | Hidden Units | Batch Size | Epochs | Learning Rate |
|---|---|---|---|---|
| PAYEMS | 32 | 32 | 30 | 1e-4 |
| UNRATE | 32 | 32 | 30 | 1e-4 |
| ACDGNO | 32 | 32 | 30 | 2e-4 |

## Performance

| Series | Train MSE | Train R² | Test MSE | Test R² |
|---|---|---|---|---|
| PAYEMS | 0.000424 | 0.9958 | 0.000685 | 0.9167 |
| UNRATE | 0.003861 | 0.8945 | 0.018035 | 0.7152 |
| ACDGNO | 0.001247 | 0.9675 | 0.007457 | 0.5986 |

Note: UNRATE and ACDGNO show a larger train/test gap than PAYEMS, reflecting the 
greater volatility and less predictable nature of these series.
