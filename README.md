# Monte Carlo Basic

This project is intended to showcase a basic Monte Carlo simulation implementation in Python. It enables one to simulate underlying price movements for multiple stocks, having a few basic additions beyond a plain vanilla implementation that allow for more realistic and useful results. It is based upon this paper (https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2665147), using the methods described therein and extrapolating minor additional optionality on top of that.

![Screenshot](MonteCarloEqn.jpg)
![alt text](https://github.com/CharlesDavidEly/monte-carlo-basic/blob/main/MonteCarloEqn.jpg?raw=true)


# Parameters

In addition to the most basic and fundamental parameters for this method (mean and variance), this Monte Carlo simulation implementation allows for the following inputs:

1) Skew
2) Kurtosis
3) Correlation

It also gives the option for all parameters to change over time, linearly from A to B or however else this is to be defined. This allows for the very useful assessment of nuanced market views, (e.g. that a stock's returns variance will increase over the next year, or that two stocks' returns correlation will decrease).

Though this naturally slows down the simulation process in simple cases, say if mean returns or return correlations remain constant, this is intended to be a generic implementation that gives the user significant optionality.

Where performance time is critical, an implementation tailored specifically for the task at hand with the precise amount of complexity necessary could be written. Moreover, a low-level language much better suited for such a task, such as C++, would likely be in order.

# Simulation Units

This simulates underlying price movements in days, rather than in time periods shorter or longer than a day.
