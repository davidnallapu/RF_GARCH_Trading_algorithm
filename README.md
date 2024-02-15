# Enhancing Stock Trading Strategies with Machine Learning and Econometrics

## Abstract
In this research, I explore the application of machine learning and econometrics to create a trading strategy that combines a Random Forest (RF) algorithm with a Generalized Autoregressive Conditional Heteroskedasticity (GARCH) model. My objective is to assess the performance of this strategy on stock and ETF trading. The approach was tested on stocks PTN, JPM, and a custom-created ETF comprising 25% each of JPM, FITB, BAC, and SQ. These stocks were chosen for their diversity, representing both established financial institutions and new-age fintech companies, with a history of weathering various recessions.

## Methodology
Data Collection: Historical data for PTN and JPM were collected and analyzed. For a broader perspective, a custom ETF was created to encapsulate a diversified portfolio.

Feature Engineering: I computed technical indicators like Simple Moving Averages and Bollinger Bands to serve as features for the Random Forest model.

Random Forest Model: The RF model was trained to predict stock price movements. The model's hyperparameters were optimized using RandomizedSearchCV to minimize the mean absolute error.

GARCH Model Integration: Alongside the RF model, I employed a GARCH model to forecast volatility. The model was specified with p=2 and q=2, reflecting the assumption that both the autoregressive and moving average components of the volatility had a lag of two.

Trading Simulation: The trading strategy was simulated over a period, using the RF model to predict closing prices and the GARCH model to forecast volatility. The buy or sell decisions were based on the predicted closing price and volatility trends.

Results
The trading strategy yielded a profit of 7.54% over the simulation period, compared to a 4.46% profit from a buy-and-hold strategy. This indicates a successful application of the strategy in generating returns above a simple buy-and-hold approach.

![alt text](https://github.com/davidnallapu/RF_GARCH_Trading_algorithm/blob/main/download.png)

## Trading Methodology
The trading methodology was underpinned by the following logic:

Sell Signal: Generated when the actual opening price was higher than the RF model's predicted closing price, suggesting an overvalued opening price. Additionally, a sell was triggered if the GARCH model indicated increasing volatility, signaling a potential decrease in price movement.

Buy Signal: Triggered when the actual opening price was lower than the RF model's predicted closing price, indicating an undervalued opening price. A buy was also initiated if decreasing volatility was forecasted by the GARCH model, implying expected larger price movements that could be capitalized upon.

These decisions were encapsulated in a day_trade function that took into account both the RF model's predictions and the GARCH model's volatility forecasts, executing trades based on the combined signals.

### Discussion
The results suggest that integrating machine learning predictions with volatility forecasting can enhance trading strategies. The RF model provided a direct forecast of price movements, while the GARCH model added a layer of volatility expectation, which is crucial for risk management and decision-making in trading.

## Conclusion
This research demonstrates that combining predictive models with volatility forecasts can create a robust trading strategy. The positive results from the trading simulation warrant further exploration and live-testing in different market conditions to validate the strategy's effectiveness.

#Detailed Trading Methodology Using Random Forest and GARCH Models

## Data Preparation and Initial Analysis
To begin, I collected historical price data for the chosen stocks and ETF. This data was then preprocessed to calculate various technical indicators which served as input features for the predictive models. These indicators included:

Simple Moving Averages (SMAs) for periods of 5, 10, 20, 50, 100, and 200 days.
Bollinger Bands calculated for 20-day and 10-day periods, using 2 standard deviations for the former and 1 standard deviation for the latter.
These indicators are commonly used in trading to identify trends and potential reversal points in the price of assets.

### Predictive Modelling with Random Forest
The Random Forest model was trained using these features to predict future closing prices of the stocks and ETF. The model's hyperparameters were tuned to minimize prediction error, ensuring that the most predictive features were utilized for forecasting. This involved identifying correlations between features and the target variable to select the most significant predictors.

### GARCH Model for Volatility Forecasting
Alongside price prediction, a GARCH model was integrated to forecast future volatility. This econometric model captures the time-varying volatility clustering often observed in financial markets. By specifying a GARCH(2,2) model, I acknowledged that the previous two observations of volatility and shocks have predictive power for future volatility. This model was fitted on the percentage change of the closing prices to understand and forecast the conditional volatility.

### Combined Trading Strategy
The trading strategy was built upon the combination of signals from the Random Forest and GARCH models. The decision process was as follows:

### Pre-Market Analysis:

Each trading day, before the market opened, the RF model was used to predict the closing price of the asset for that day.
The GARCH model provided a three-day ahead volatility forecast, which was used to determine the expected market conditions.
Trading Signals:

A sell signal was generated when the actual opening price was higher than the predicted closing price from the RF model. This was interpreted as the market opening at an overvalued price level.
If the GARCH model indicated a increasing volatility trend, it reinforced the sell signal, suggesting a potential decrease and uncertainity in price movement ahead.
A buy signal was generated when the actual opening price was lower than the RF model's predicted closing price. This was seen as the market opening at an undervalued price level.
A decreased volatility trend from the GARCH model would trigger a buy signal, indicating larger expected and less volatile price movements that could be advantageous.

### Trade Execution:

The trades were executed based on the combined signals, with the model's output dictating whether to buy, sell, or hold.
The trade size and frequency were determined by the strength of the signals and the overall strategy's risk management rules.
Results Interpretation and Strategy Evaluation
The strategy yielded a 7.54% profit, outperforming the buy-and-hold strategy's 4.46% profit. This success is attributed to the dynamic nature of the strategy, which adjusts to daily market conditions and adapts to new information as it becomes available.

The integration of RF's predictive power with the GARCH model's volatility forecasting allowed for a more informed and nuanced trading strategy. It showed that machine learning could effectively predict price movements, and when combined with econometric models, could provide a comprehensive trading system.

### Conclusion
The detailed methodology demonstrates a sophisticated approach to stock trading. By leveraging the strengths of both machine learning and econometric models, I was able to create a strategy that adapts to market conditions and outperforms simpler, static strategies. Future work could involve expanding this strategy to incorporate additional predictive features, refine the models, and possibly deploy the strategy in live trading environments to test its effectiveness in real-time market conditions.
