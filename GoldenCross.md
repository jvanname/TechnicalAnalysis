**Broad Description**

In this post, we try to determine whether one can use the golden cross (the points of intersections between moving averages) in order to make a profit while trading stocks. We use the stocks of both established companies that pay dividends as well as startups which currently do not pay dividends to shareholders.

**More technical details**


In this post, we use the hourly closing price of stocks to try to predict whether the price will go up or down in the future and also to determine whether our strategy results in a loss or a profit.

Suppose that $X_i$ denotes the closing price of the stock at hour $i$. Let $A$ denote the set of hours when the stock market is open (and therefore where we have a well-defined price).
If $i\in A$, then $X_i$ is clearly defined, but we otherwise define $X_k$ for each so that if $i,j$ are two consecutive elements in $A$, then the set $\{(k,X_k):i<k<j\}$ is colinear.

Let $M_i$ denote the moving average over the past week, and let $N_i$ denote the moving average over the past two weeks. When $M_i>N_i,M_{i-1}<N_{i-1}$, we buy and go long hoping to sell later at a higher price because we believe the market is in an uptrend.
When $M_i<N_i,M_{i-1}>N_{i-1}$ we do the opposite and go short because we believe the market is a downtrend. In order to simplify the analysis and to limit our risk, when we are going long, we put stop and limit orders to ensure that we always attain a 3 percent profit or 3 percent loss. In order to simplify our analysis and algorithm, the only way we close our trade is by using these stop and limit orders. To further simplify our analysis, each time we trade, we trade for the same amount. This means that whenever we trade, we always make the same amount of profit or the same amount of loss.

The timeframe of the data is from May 1, 2018 until approximately August 1, 2025.

I chose 3 percent because 3 percent is comparable to the standard deviation of $X_{i+168}/X_i$; the amount that the price varies every week.

**Results**

The following chart shows how much profit we trade. Here we calculate the profit as the number of trades in which we make a profit minus the number of trades in which we make a loss. The column 'Uptrend Profit' and 'total uptrend trades' refer to the trades and the profits made starting at the point $i$ where $M_i>N_i,M_{i-1}<N_{i-1}$. The other columns have analogous definitions. The stocks AMZN,INTC,MSFT,NVDA are well-known established companies while QUBT,PLTR,QBTS,CIFR are stocks that currently do not pay dividends.

Stock | Uptrend Profit      | Downtrend Profit      | Total Profit | Total uptrend trades | Total downtrend trades |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
AMZN| 14 | -22 | -8 | 100 | 100 |
INTC| 12 | -15 | -3 | 107 | 108 |
MSFT| 4 | -12 | -8 | 94 | 94 |
NVDA| 5 | -15 | -10 | 93 | 93 |
QUBT| 3 | -12 | -9 | 57 | 58 |
PLTR|-7 | -13 | -20|67|67|
QBTS|-13| 1 | -12 | 41| 41|
CIFR|-3| 4 | 1 | 57 |58 |

We observe that for each of the stocks, we would not have made any profit using our original strategy, but a modified strategy would have been profitable for these stocks for the timeframe.

**Statistical significance of modified strategy**
If we instead modified our strategy so that we always go long and never go short on each golden cross, then we would have made a statistically significant amount of profit for the stocks in question.

**What I did not cover in this analysis**

In this analysis, I did not take into consideration slippage, fees, and dividends, but I included some stocks such as QUBT that do not give dividends to get a picture of what happens in that case as well.

In this analysis, I decided to compare the 1 week moving average with the 2 week moving average which is a rather short timeframe. ig-academy defined the golden cross as where the 50 day moving average crosses the 200 day moving average. This is easy to change though.
