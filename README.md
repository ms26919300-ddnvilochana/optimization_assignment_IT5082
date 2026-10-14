IT5082 - Optimization Methods
Optimization Assignment
This is code repository for the IT5082 - Optimization Methods group Assignment by DDN VILOCHANA and P.P. KODIKARA.

## Dataset status

The Dataset is Finalized.

## Problem 

Cardinality-constrained portfolio selection (choose at most K stocks and their weights to minimise risk for a target return). Dataset: S&P 500 stock prices from Kaggle (https://www.kaggle.com/datasets/andrewmvd/sp-500-stocks).

## Why this dataset

- Real-world data: actual daily market prices of large US companies, not synthetic numbers, which the assignment brief prefers.
- Natural fit for subset selection: hundreds of stocks to choose from, so the number of possible portfolios grows combinatorially and an exact method and a heuristic can be compared meaningfully.
- Scalable: we can build test universes of different sizes (for example 20, 50, 100 and 200 stocks) from the same file to study runtime and solution quality as the problem grows.
- Used only to instantiate the model: daily prices give returns, from which we compute mean returns and the risk measure. No machine learning or model training is involved.
- Known limitation: it contains today's index members only (survivorship bias), which we note in the discussion.