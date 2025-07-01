
1. Strategy Overview

This strategy uses a Support Vector Machine (SVM) model combined with technical indicators to predict market movements and make trading decisions. The strategy is applied on stocks while the Machine Learning SVM model is applied specifically on the SPY ETF (which tracks the S&P 500 index) to predict market trends. The strategy primarily takes long positions based on the bullish predictions from the SVM model but does not engage in short selling.

Key components of this strategy:


•	Technical Indicators: RSI (Relative Strength Index), MACD (Moving Average Convergence Divergence), and Bollinger Bands (BB).
•	SVM Model: A machine learning model that classifies market conditions as bullish or bearish based on historical technical data from SPY.
•	Feature Extraction: Input features include the SPY closing price, volume, RSI, MACD, Bollinger Bands (upper and lower bands).

The strategy only takes long positions in stocks selected from the S&P500 universe, when the SVM applied to SPY predicts favorable (bullish) conditions. It does not enter short positions, and all trades are governed by SPY’s market trend predictions.

2.	Technical Indicators Used

1.	RSI (Relative Strength Index):

•	A momentum oscillator that measures the speed and change of price movements.

•	This strategy uses a 14-period RSI to determine overbought and oversold conditions.

•	RSI values below 30 indicate oversold market conditions.

•	RSI values above 70 indicate overbought conditions.

2.	MACD (Moving Average Convergence Divergence):

•	A trend-following momentum indicator that shows the relationship between two moving averages of a security’s price.
•	A positive MACD suggests upward momentum (bullish).

•	A negative MACD suggests downward momentum (bearish).

3.	Bollinger Bands:

•	Volatility indicators consisting of an upper and lower band around a 20-day simple moving average (SMA).
•	The distance between the bands expands when volatility increases and contracts during periods of low volatility.

These indicators are applied specifically to SPY and used as input features for the SVM model, which forms the foundation of the trading decisions.
 

3. Support Vector Machine (SVM) Model
 
SVM Overview:


•	The SVM classifies whether the market is likely to be bullish (prices increasing) or bearish (prices decreasing) based on SPY’s technical indicators.
•	Kernel Trick: The SVM uses the RBF (Radial Basis Function) kernel to handle non-linear relationships between indicators, making it well-suited for capturing complex market behavior.
•	Probability Output: The SVM outputs a probability that SPY will be bullish. A higher probability indicates a higher likelihood of a bullish market, and vice versa.

The SVM model is trained exclusively on SPY data, and its predictions guide the strategy for trading in stocks from the QC500 universe.

4.	Training and Lookback Periods Training Period:

•	The training period refers to the specific date range of historical data used to initially train the model.

•	In this strategy, the model is trained using 10 years of SPY historical data from January 1, 2000, to December 31, 2009.

Lookback Period (2520 days):


•	The lookback period is the sliding window of past data points that the SVM considers at any given time to make predictions.
•	The lookback period is set to 2520 days, which represents approximately 10 years of market data (252 trading days per year).
•	This lookback window dynamically shifts forward day by day to ensure that the SVM always uses the most recent 10 years of data for predictions.

Key Difference:

•	The training period (2000-2009) is a fixed historical time range used to initially train the SVM model.

•	The lookback period (2520 days) is a rolling window of the most recent 10 years of data used to update the model and make real-time predictions during live trading.

5. Feature Extraction for the SVM

The strategy uses six key features from SPY’s historical data to train the SVM:


1.	Close Price: The end-of-day price for SPY.

2.	Volume: The number of shares traded for SPY.

3.	RSI: The relative strength index value for SPY.

4.	MACD: The difference between SPY’s short-term and long-term moving averages.

5.	BB Upper: The upper Bollinger Band value for SPY.

6.	BB Lower: The lower Bollinger Band value for SPY.
 
These features represent the state of the market for SPY, which is updated each day as new data becomes available. The SVM uses these features to predict the market’s future direction.

6.	Trading Logic and Rules Prediction and Market Entry:
•	The SVM model makes a daily prediction based on SPY’s most recent data. The output is a probability score between 0 and 1:
•	Probability > 0.5: Indicates a bullish market.

•	Probability < 0.5: Indicates a bearish market, but this is only used to exit positions, not for short trades.

Long Entry Conditions (Bullish Prediction):


•	If the model predicts a bullish market and:

•	The stock’s current price is above its 200-day SMA, and

•	The SVM gives a bullish prediction (probability > 0.5),

•	The strategy enters a long position (buys shares of SPY or other stocks in the universe).


Exit Conditions (Bearish Prediction or Downtrend):


•	The strategy exits long positions when:

•	The SVM predicts a bearish market (probability < 0.5), or

•	The stock’s price falls below its 200-day SMA, indicating a potential downtrend.


There is no short selling in this strategy. It only opens long positions when the SPY conditions are favorable and exits those positions when the SVM or technical signals indicate a reversal.

7. Risk Management

The strategy incorporates the following risk management rules:


•	Capital Allocation: The strategy allocates 5% of total capital per trade to minimize risk in individual positions.
•	Diversification: The strategy can hold positions in up to 20 different stocks, provided conditions are met.

By limiting the capital allocation per trade and using machine learning for predictive power combined with traditional technical signals, the strategy aims to make safer, informed trading decisions.

8. Predictions and Decision-Making
 

The SVM model applied to SPY predicts:
 
•	Bullish Market: If the model outputs a probability > 0.5, the strategy predicts an upward market movement and may enter long positions.
•	Bearish Market: If the probability < 0.5, the strategy predicts a downward market movement and will exit any existing long positions.

These predictions, along with other technical indicators, help determine whether to enter or exit long positions, creating a dynamic, adaptable trading strategy that focuses on capitalizing on bullish trends while minimizing exposure during bearish periods.
