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

## Notebooks and how to run

```
python -m venv .venv            # activate it
pip install -r requirements.txt
jupyter notebook
```

| Notebook | Method | Output |
|---|---|---|
| `Exact_Method.ipynb` | MILP with MAD risk, solved by Branch and Bound (HiGHS via `scipy.optimize.milp`) | `results/exact_results.csv` |
| `Heuristic_Method.ipynb` | Simulated Annealing over K-stock subsets; an inner LP gives the best weights of each subset | `results/heuristic_results.csv` |

Run `Exact_Method.ipynb` first; the heuristic notebook reads its results. Set `QUICK = True` in either notebook for a short test run. The full heuristic notebook takes about 45 minutes (12 instances x 10 SA seeds, tuning and ablation).

## Results so far (heuristic versus exact)

- All 120 SA solutions pass the independent feasibility check; every instance's exact optimum is found by at least one of the 10 seeds; mean gap 0 % to 0.51 % per instance.
- SA is slower than the MILP for N = 20, about even at N = 50, and faster at N = 100 (1.4 to 2.3 times) and N = 170 (4.5 times). Where the MILP hits its 60 s limit (K = 8, N = 170), SA reaches the same incumbent in about 14 s.
- A plain swap local search from the top-K start reaches the exact optimum on all 12 instances, so SA adds no quality beyond a local optimum on these instances (see section 10 of `Heuristic_Method.ipynb`).
