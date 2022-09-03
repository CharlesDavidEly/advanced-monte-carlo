# Monte Carlo Basic

This project is intended to showcase a basic Monte Carlo simulation implementation in VBA. It enables one to simulate underlying price movements for multiple stocks, having a few basic additions beyond a plain vanilla implementation that allow for more realistic and useful results. It is based upon this paper (https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2665147), using the methods described therein and extrapolating minor additional optionality on top of that.

![Screenshot](MonteCarloEqn.jpg)

The above formula is the core of the stock price Monte Carlo simulation concept, modeling geometric Brownian under the risk-neutral measure. A simulated stock price can be conceptualized as the previous day's stock price multiplied by *e* to the sum of 1) some drift (scaled by time step Δt), and 2) a random walk (scaled by √(Δt)).

## Drift

An underlying's drift is simply a product of its μ (average simple return) and σ (simple return standard deviation) as calculated over some specified ex-post sample period, interacting as depicted in the formula above and then being scaled by Δt. Notably, the core of the drift term (that is, the part in the parentheses that's ultimately scaled by Δt) is also equivalent to the same ex-post sample's log return, so it could just be defined as that directly without any need for μ or σ. Alternatively, μ and σ (or an expected average log return as previously explained) could be specified explictly to plug a particular ex-ante market view into the model.

## Random Walk

An underlying's random walk is simply ε (a random movement) scaled by both σ and √(Δt).

## Extras

Importantly, this random term ε is ultimately the center of all attention. It is this term, for each underlying at each simulation step, that must be manipulated in careful and clever ways to account for nonnormality and correlation.

Specifically, there is at each step of the simulation with respect to the random term, ε:

1) The application of skew and kurtosis (ex-post sample or ex-ante desired) to each stock's simulated log return
2) The determination of necessary correlations by taking desired correlations (ex-post sample or ex-ante desired) and accounting for interactive effects (they must be made stronger due to the correlation muting effect caused by applying skew and kurtosis in step 1))
3) The application of necessary correlations to the log returns resulting from step 1)

# Parameters

## Underlying

In addition to the most basic and fundamental parameters for this method (mean and variance), this Monte Carlo simulation implementation allows for the following inputs:

1) Skew
2) Kurtosis
3) Correlation

It also gives the option for all parameters to change over time, linearly from A to B or however else this is to be defined. This allows for the very useful assessment of nuanced market views, (e.g. that a stock's returns variance will increase over the next year, or that two stocks' returns correlation will decrease).

Though this naturally slows down the simulation process in simple cases, say if mean returns or return correlations remain constant, this is intended to be a generic implementation that gives the user significant optionality.

Where performance time is critical, an implementation tailored specifically for the task at hand with the precise amount of complexity necessary could be written. Moreover, a low-level language much better suited for such a task, such as C++, would likely be in order.

## Simulation Parameters

In addition to those parameters associated with the underlyings, there are the following inputs at the simulation level:

1) Simulation number
2) Time unit size = Δt (in trading days; e.g., days (1), weeks (5 trading days), months (21 trading days), etc.)
3) Time units (e.g., 252 if your simulation unit size is days (1) and you want to simulate prices over the course of a year)

Fasdfadsfasdf

# Limitations

As the word "basic" in the name implies, this Monte Carlo specification does not account for everything. Specifically, it does not capture the empirical reality of volatility clustering, as could be done using a GARCH model. Moreover, it does not accurately capture the differentiated behavior between open market and after hours periods, as would a jump diffusion model.

The primary impact of these limitations is that for underlyings whose precise movements (and especially volatilities) in the very near term are of critical importance to identify, this specification will leave much to be desired. An easy example of such a scenario would be an underlying we're looking at because we're considering purchasing a call option on it that expires in a week.

For most use cases however, where the duration of going concern for a portfolio of underlyings is over the medium to long term, this specification should prove quite appropriate and satisfactory. Although basic, it accounts for all of the low-hanging fruit, so to speak.
