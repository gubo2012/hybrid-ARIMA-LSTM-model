# Summary
This hybrid ARIMA-LSTM model is an application of “Stock Price Prediction Based on ARIMA-RNN Combined Model” by Shui-Ling YU and Zhe Li. This model follows the same structure as the model proposed by YU and Li and is designed as a flexible platform to further explore the model’s capabilities. The model is prepared to forecast the daily closing prices of the SPDR S&P 500 ETF Trust (SPY).

A moving average filter is used to separate the daily closing prices into a low volatility times series (moving average output) and a high volatility time series (close – moving average). The moving average period is optimized such that the resulting output obeys a normal (mesokurtic) distribution. A normal distribution is defined as a kurtosis K value of 3. For K > 3, the data is leptokurtic and for K < 3, the data is platykurtic. The length of data used for determining the kurtosis value was set to 60 days. The length of data used has a direct effect on the kurtosis value. With longer data sets, K is less than 3 for all values of moving average period length. Several common types of moving averages are evaluated from the Ta-Lib library.

An LSTM (Long Short-Term Memory) recurrent neural network is used to forecast the high volatility time series. The neural network is comprised of a four neuron LSTM tensor, a two neuron LSTM tensor, and a single one neuron dense tensor. The high volatility time series is pre-processed with a scalar function to adjust the feature range to between 0 and 1. The LSTM model is fit with early stopping enabled to minimize potential over-fitting. An ARIMA (AutoRegressive Integrated Moving Average) model is used to forecast the low volatility time series. The model is fit for ARIMA parameters p, q, and d. The order of differencing d is determined via Phillips–Perron, Kwiatkowski–Phillips–Schmidt–Shin, or Augmented Dickey-Fuller. The predicted low and high volatility time series are summed to generate the predicted closing prices.

The accuracy of the ARIMA-LSTM model is evaluated in several ways. MSE, RMSE, and MAPE are utilized to asses the error between the predicted closing prices and the actual closing prices. Two simulations are conducted to asses the model’s predictive accuracy. In first simulation, the model’s predictions are compared to the previous day’s closing price. If the predicted closing price is greater than the previous closing price, then the SPY ETF is predicted to close higher the following day. In the second simulation, the model’s predictions are compared to the previous day’s prediction. If the predicted closing price is greater than the previous predicted closing price, then the SPY ETF is predicted to close higher the following day.

# Further Research
The hybrid ARIMA-LSTM model is open to a variety of experimentation. For ideal performance, a balance must be reached between the levels of volatility that work best for the ARIMA and LSTM models.  Using shorter MA periods that result in a non-mesokurtic distribution may achieve a better volatility balance between models. Additionally, the structure of the LSTM network can be altered to include more tensors of different lengths and dropout layers. Various activation functions and optimizers are also worth exploring. Finally, this model can be examined with other index ETF’s, stocks, futures, and forex contracts.

# Dependencies
* Python 3
* Numpy
* Pandas
* SciPy
* Scikit-Learn
* Pmdarima
* Keras
* Ta-Lib

# References
* [Stock Price Prediction Based on ARIMA-RNN Combined Model](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=2ahUKEwjU0NqbvejkAhXDJt8KHQTeAZ0QFjAAegQIAxAC&url=http%3A%2F%2Fdpi-proceedings.com%2Findex.php%2Fdtssehs%2Farticle%2Fdownload%2F19384%2F18875&usg=AOvVaw1Iy45JKJrEOXXxo0VqcE9J)
