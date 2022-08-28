# Monte Carlo Basic

This project is intended to showcase a basic Monte Carlo simulation implementation in Python. It enables one to simulate underlying price movements for multiple stocks, having a few basic additions beyond a plain vanilla implementation that allow for more realistic and useful results.

# Parameters

In addition to the most basic and fundamental parameters for this method (mean and variance), this Monte Carlo simulation implementation allows for the following inputs:

1) Skew
2) Kurtosis
3) Correlations

It also gives the option for all parameters to change over time, linearly from A to B or however else this is to be defined. Though this naturally slows down the simulation process in simple cases, say if mean returns or return correlations remain constant, this is intended to be a generic implentation that gives the user significant optionality.

Where performance time is critical, an implemenation tailored specifically for the task at hand with the precise amount of complexity necessary could be written. Moreover, a language much better suited for such a task would likely be in order, such as C++.

# Simulation Units

This simulates underlying price movements in days, rather than in time periods shorter or longer than a day.
