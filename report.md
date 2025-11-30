## Importing the data from yfinance

[datasets.ipynb](datasets.ipynb) will be responsible of importing the latest data from yfinance and storing it on google drive

## Initial Planning

#### Transformer

- Requires too much data for pretraining and training.
- Could use pretrained models but will still require a lot of data for training, overfitting risk
- Last resort, will try XGBoost and GRUs before

#### XGBoost

- Imported the dataset and added feature egineering
