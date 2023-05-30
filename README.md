# Hedge Fund Exposure


Modeling daily returns and corresponding NAV changes of individual hedge funds is important for hedge fund. NAV values of hedge funds are typically available on monthly basis.  The daily NAV for a hedge fund is computed based on modeling daily returns of the hedge fund as a weighted sum of returns of a combination of several market indices and factors.

These indices and factors typically include: a) US and international equity market indices; b) US and international fixed income indices. c) Currencies; d) Other market factors, such as credit spreads, volatilities, etc.

The model is calibrated based on historical monthly returns of the fund and the market indices and factors, resulting in an “exposure profile”. Exposure profile is a vector of index weights representing the “best” estimate of the systematic return of the fund in the past.

After the exposure profile is determined, the daily returns of the hedge fund are estimated by multiplying the exposure profile (as a vector) on the known vector of daily returns of the corresponding indices and factors.

The main problem in the practical application of this approach lies in the fact that on one hand the number of indices that can be used to build a model is very large and, on the other hand, the particular combination of indices relevant to a particular fund is usually not known.

A model is developed to identify a set of indices that is relevant for each particular hedge fund and to use only these indices to estimate daily returns and also develop a measure of accuracy of the estimation that does not depend on the number of indices used in the model.

The approach consists of two stages. The first stage (forward regression) starts with a single index selected based on maximum correlation with the returns of the hedge fund. Other indexes are sequentially added to the model using maximum partial correlation as the criterion for inclusion in the model.

 After the number of indices included in the model reaches certain predetermined number, the reverse process (backward elimination) starts – indices are sequentially removed from the model using the value of t-statistic as the criterion for removing an index. The process stops when only one index is left.

In the end, this approach produces several sets of indices that are reasonable candidates for the final model. The choice among these sets represents a complex task because standard statistics, such as F-statistic, t-statistic and R-Squared are biased when a selection process is used to choose indices from a large set.

The predictive power of the model is estimated based on the average of the values of Jackknife R-Squared and regression R-Squared, adjusted by the number of indices available in the index selection process.

The value of the R-Squared is computed by the linear regression module, while the value of the of Jackknife R-Squared statistic is computed by systematically excluding dates from the model and comparing predicted returns to the actual returns for each excluded date.

Even given the best model, the predictive power may be low for a substantial proportion of hedge funds – specifically those that hedge their exposure to the market factors. To forecast daily returns for these “low R-Squared” funds, we implement a proxy-based approach; the hedge funds with low R-Square are combined in a fund of funds, and the index selection procedure is applied to this fund of funds.

This approach leads to the determination of the exposure profile of the group of hedge funds, as opposed to the individual funds. This exposure profile represents the “best proxy” in the sense that when daily returns of the low R-Squared funds are estimated based on this proxy, the sum of estimated daily returns of individual hedge funds provides the best estimate for the returns of the total portfolio. 

The specific return component is determined by the factors specific to the individual securities the fund has a position in and is not related to the general economic and market indices. It follows, that for each period the return of a hedge fund can be written as
RF  =  + SF				(1)
Where:
RF - return of a hedge fund during the time period
Rj – return of an index j during the time period
bj – coefficients describing the sensitivity of the fund to the changes in the index
SF – the specific component of the hedge fund’s return


Within the linear regression framework, the specific component SF represents the “random error”. This error is relatively small for well-diversified traditional investment portfolios. For example, for domestic equity mutual funds the specific component usually accounts for not more than 10% of the fund’s returns RF. 

On the other hand, the specific component may become a dominant component of the returns of a hedge fund that maintains both long and short positions in each market segment it invests in.

When the size of specific return component is comparable or even exceeds the systematic component of returns, common least squares estimators (used in standard linear regression) become ineffective and more robust regression methods must be used. 

The linear regression model assumes that the hedge fund’s exposure to market factors remains constant, i.e., do not change with time. Mathematically speaking, the linear regression model assumes that coefficients are stationary. Of course, this is not necessarily the case with managed portfolios. For practical purposes we can assume that the values of bj are the “average exposures” for the period used to fit the model.

Consequently, the regression model will generate errors if the average exposure is a poor characteristic of the actual exposure at each particular point in the history (or future) of the fund.

Sometimes when a hedge fund maintains substantial positions in derivative securities, such as barrier options, its return cannot be accurately represented by a linear combination of indices because of the non-linear nature of relationship between returns on an option and the return on the underlying security represented by an index. 


References:

https://finpricing.com/lib/EqBarrier.html

https://derivatives.hcommons.org/equity-instruments/

