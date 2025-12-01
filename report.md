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
- Trained the model on all data before 1 december 2025, then tested and compared results
- Results are very bad compared to how the model was previously predicting
- Probably due to the long plateau in silver and gold, and sudden spike in all 3 currencies
- My hypothesis is no model will be able to perform well after these times, especially for silver and gold

#### XGBoost (1 hour and 1 day)

- same implementation as 30mins, but we only change the datasets
- Models performed very poorly, values often plateau after a certain timestep
- Checked the datasets again, realized that at least one of the 3 currencies in each dataset (30m, 1h, 1d) had initial plateaued values
- Could be considered as noise and confuse the models during training
- decided to check further into the issue

#### Initial plateaus in datasets

- when we get data from yfinance and set period='60d' or period='730d', we will get values older than that, but not for all instances
- for example, i would get gold for a month before 60d, but CAD 3 months older than 60d
- when we did forward and backward fill, these missing times in the other currencies were filled as the first timestep retrieved from yfinance
- results in plateaus and noise in the dataset
- to solve this, we had to manually go through the dataset to find where values started fluctuating
- manually set start and end period. specific start and end periods in [datasets.ipynb](datasets.ipynb)
- Result : not much noticeable difference. XGBoost was mostly reliable for predicting 30m


#### GRU test (30m, 1h, 1d)

- Straightforward approach, hyperparameter tuning using hyperband
- impressive results for all metrics and time intervals except gold