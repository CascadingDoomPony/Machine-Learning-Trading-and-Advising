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

## The progression of our model

This is the very first test we did on our model. You can see the close price from training first and testing after below. We are using 5 year TSLA data with a 1y train 4y test split (this is changed over time)

Training Close Price
![](Plots_and_Images_library/Dual%20SMA%20SVC/Close_Train.png)
Testing Close Price
![](Plots_and_Images_library/Dual%20SMA%20SVC/Close_Test.png)
As you can see in the testing graph, the model inexplicably stops trading after a certain amount of time. This occurred on almost all tests we did for our first iteration and you can see this in the Plots and Images folder in all our tests that didn't include RSI.

Once we added in our second set [RSI, ADX, ATR], We saw a significant improvement in the model. We now tested with all Disney (DIS) data we could grab from YFinance, and we grabbed 48 years of training data, and tested on the rest.

The first significant change was with adding RSI and ADX

Training Portfolio Total
![](Plots_and_Images_library/RSI%20ADX%20SVC/training_total.png)
Training Close Price
![](Plots_and_Images_library/RSI%20ADX%20SVC/training_close.png)
Testing Portfolio Total
![](Plots_and_Images_library/RSI%20ADX%20SVC/testing_total.png)
Testing Close Price
![](Plots_and_Images_library/RSI%20ADX%20SVC/testing_close.png)
Now we have resolved the issue where the model stops trading at a certain point. However if you look at the trends of the Portfolio Totals with the Close Prices, you'll notice that there is very little actual difference between the two graphs. This indicates that our model isn't making any significant trading decisions, and is almost exactly following the trends of the market.

Next we added ATR

Training Portfolio Total
![](Plots_and_Images_library/RSI%20ADX%20ATR%20SVC/training_total.png)
Training Close Price
![](Plots_and_Images_library/RSI%20ADX%20ATR%20SVC/training_close.png)
Testing Portfolio Total
![](Plots_and_Images_library/RSI%20ADX%20ATR%20SVC/testing_total.png)
Testing Close Price
![](Plots_and_Images_library/RSI%20ADX%20ATR%20SVC/testing_close.png)
We can see here that our model is now deviating from the close prices. It almost seems to avoid overly volatile periods which makes sense since ATR is a volatility indicator.

This is the final iteration of our model

You can see the rest of the tests in our Plots and Images folder.

### References

[Stanford Sentiment Paper](https://cs229.stanford.edu/proj2011/GoelMittal-StockMarketPredictionUsingTwitterSentimentAnalysis.pdf)
