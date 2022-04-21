# Machine-Learning-Trading-and-Advising

This project is an experiment on applying machine learning models to market trading. We applied ML models from the SKLearn package and used technical indicators to train, test, and evaluate using backtesting metrics.

## Data Gathering and Cleaning

Our data is pulled from YFinance using their packaged API to get market data on a variety of stock tickers. The data pulled from YFinance is usually quite clean and there isnt too much we need to do to make it usable. We pulled our data using a notebook (Data\stock_data.ipynb), and stored it in the Data folder.

## Target Value

The model will be used to predict whether the current close price will go up or down on the next day, so to produce our Y values we first create actual returns by running pctChange() on the close price of our data, then set boolean indicators for whether actual returns is positive or negative, which effectively represents perfect price trend predictions

## Features

We used TA to produce all of our features. Initially we had a set of Bollinger Band (BB) and Simple Moving Average (SMA), and the close price that is provided in the data. Later after some testing we added Relative Strength Index (RSI), Average Directional Index (ADX), and Average True Range(ATR)

## Model and Training
We used the SVC model from SKLearn and we train our data using an 80:20 training:testing split, which will produce different training lengths depending on the actual length of our data.

## Backtesting Metrics
For our backtesting suite we recorded Annualized and Cumulative Returns, Annualized Volatility, and Sharpe and Sortino Ratio. To get these calculations we did a diff() on the boolean trend signal to get the data points where it is most optimal to trade according to the model, and we set our initial portfolio size to 50,000 and a share trade size of 500.

For our tests we also plot the portfolio and close price change over time, and we plot the trading points on both of these graphs.



### References

[Stanford Sentiment Paper](https://cs229.stanford.edu/proj2011/GoelMittal-StockMarketPredictionUsingTwitterSentimentAnalysis.pdf)
