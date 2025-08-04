In this post, we use the hourly closing price of stocks to try to predict whether the price will go up or down in the future.

Suppose that $X_i$ denotes the closing price of the stock at hour $i$. Let $A$ denote the set of hours when the stock market is open (and therefore where we have a well-defined price).
If $i\in A$, then $X_i$ is clearly defined, but we otherwise define $X_k$ for each so that if $i,j$ are two consecutive elements in $A$, then the set $\{(k,X_k):i<k<j\}$ is colinear.

Let $M_i$ denote the moving average over the past week, and let $N_i$ denote the moving average over the past two weeks. When $M_i>N_i,M_{i-1}<N_{i-1}$, we buy and go long hoping to sell later at a higher price.
When $M_i<N_i,M_{i-1}>N_{i-1}$ we do the opposite and go short. In order to simplify the analysis and to limit our risk, when we are going long, we put stop and limit orders to ensure that we always attain a 3 percent profit or 3 percent loss. In order to simplify our analysis and algorithm, the only way we close our trade is by using these stop and limit orders.

I chose 3 percent because 3 percent is approximately the standard deviation of $X_{i+168}/X_i$; the amount that the price varies every week.



**Results**

$\begin{bmatrix}
1 & 2\\
3 & 4
\end{bmatrix}$

**What I did not cover in this analysis**

In this analysis, I did not take into consideration slippage, fees, and dividends.

In this analysis, I decided to compare the 1 week moving average with the 2 week moving average which is a rather short timeframe. ig-academy defined the golden cross as where the 50 day moving average crosses the 200 day moving average. This is easy to change though.
