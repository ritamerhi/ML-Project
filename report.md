## Importing the data from yfinance

[datasets.ipynb](datasets.ipynb) will be responsible of importing the latest data from yfinance and storing it on google drive

## Initial Planning

#### Transformer

- Requires too much data for pretraining and training.
- Could use pretrained models but will still require a lot of data for training, overfitting risk
- Last resort, will try XGBoost and GRUs before

#### XGBoost (30 mins)

- Imported the dataset and added feature egineering
- Tried a random model just to understand how to implement XGBoost
- Implemented hyperparameter tuning by doing bayesian search
- Initially did k-fold CV before realizing this disrupts the time-order
- Somewhat good results so far
- If i don't do validation in bayesian search, the best model will be picked based on training results (risk of overfitting)
- Implemented predefined split indexing to do normal train/validation and prevent k-fold cross validation