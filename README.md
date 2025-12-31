# Portfolio Risk Report Generator
# Project Report

## Overview
This project is a simple portfolio risk report generator written in Python. 
Developed as a group project for HSG Introduction to Programming course. The program loads a CSV file containing historical monthly asset returns, asks the user to input portfolio weights (e.g. 0.3, 0.3, 0.4), and generates a portfolio risk report including metrics such as returns, volatility, drawdown and the Sharpe ratio. 

Files in This Repository:
- Portfolio_risk_report_generator.py Main Python script that performs the analysis. 
- sample_returns.csv CSV Sample dataset with monthly asset returns used for demonstration of the program. 

How to run:
- Make sure Python3 is installed 
- Keep the .csv and .py file in the same folder 
- Run the script: python Portfolio_risk_report_generator.py 
- Enter portfolio weight that sum up to 1 (comma separated, example: 0.4, 0.3, 0.3)


## 1. Goal
This program generates a basic risk report for a user-defined portfolio. It reads historical monthly returns from a CSV file, asks the user for asset weights, computes portfolio returns and reports key risk and return statistics.

## 2. How the program works
1. Read CSV file (`sample_returns.csv`) using `csv.DictReader`
2. Extract asset columns (not `Date`)
3. Prompt the user for portfolio weights and validate:
   - correct number of weights
   - sum of weights equals 1
   - weights are non-negative (long-only)
4. Compute portfolio monthly returns.
5. Compute risk metrics and print the report.

## 3. Metrics and formulas

Key variables:
- r_i,t = return of asset i in month t
- w_i = portfolio weight of asset i
- r_p,t = portfolio return in month t
- n = number of months

Portfolio return:
r_p,t = Σ_i (w_i * r_i,t)

Average monthly return:
r̄_p = (1/n) * Σ_t r_p,t

Volatility (sample standard deviation):
σ_p = sqrt(Σ_t (r_p,t - r̄_p)^2/(n - 1))

Monthly risk-free rate (from annual r_f,a):
r_f,m = (1 + r_f,a)^(1/12) - 1

Sharpe ratio (monthly):
Sharpe = (r̄_p - r_f,m) / σ_p

Wealth path (starting from 1):
W_0 = 1
W_t = W_(t-1) * (1 + r_p,t)

Total return:
Total return = W_n - 1

Drawdown:
Peak_t = max_(k<=t)(W_k)
DD_t = (W_t - Peak_t) / Peak_t

Maximum drawdown (reported as a positive):
MDD = min_t(DD_t)

## 4. Input data format
The CSV must include a "Date" column and one column per asset with numeric monthly returns as decimals (e.g., 0.02 = 2%).

## 5. Example
- Dataset: sample_returns.csv
- Example weights: 0.4,0.3,0.3
- The program prints:
  - average monthly return
  - volatility
  - Sharpe ratio
  - best/worst month
  - maximum drawdown
  - total return and final wealth


Assets found in CSV: Stock_A, Stock_B, Stock_C
Enter 3 weights separated by commas (example: 0.4,0.3,0.3), must sum to 1:
Weights: 0.4,0.3,0.3        

-------------------------
  PORTFOLIO RISK REPORT
-------------------------
CSV file used:  sample_returns.csv
Assets:  Stock_A, Stock_B, Stock_C
Weights:  40.00%, 30.00%, 30.00%

Average monthly return: 0.59%
Volatility (std dev): 1.67%
Sharpe Ratio (monthly, based on annual rf=1%): 0.3042

Best month: 2022-10 , 3.10%
Worst month: 2022-09 , -2.55%
Maximum drawdown: 2.55% (worst peak-to-trough decline)

Total return over period: 7.17%
Final wealth (starting from 1 unit): 1.0717
-------------------------


## 6. Assumptions and limitations
- Long-only weights (no short selling)
- Risk-free rate is fixed at 1% annually
- Data is assumed complete and properly formatted
- Metrics are monthly (no annualization)

## 7. Potential improvements
- Annualized metrics
- Support shorting
- Additional risk metrics
- Robust handling of missing values and input errors
- Visualizations of data

## Authors
- Didrik Bengtsson 
- Yiannis Tsigkas 
- Adam Bursic 
- Max Prohorovs

## Statement of Generative AI
We acknowledge the use of generative AI tools ChatGPT 5 and Copilot for general brainstorming and project ideation as well as improvements to the overall code quality.