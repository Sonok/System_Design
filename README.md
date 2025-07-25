# MOCK Quantitative Signal Design and Backtesting Challenge

Thank you for your interest in the technical interview process. This case study is intended to evaluate your ability to process high-frequency market data, extract meaningful signals, and rigorously test your ideas using a systematic framework.

You will be working with limit order book (LOB) and trade data to develop a short-term trading strategy. Your submission should reflect a clear understanding of market microstructure, solid programming skills, and attention to detail.

---

## Objective

Using the provided market data, you are expected to:

1. Efficiently parse and preprocess raw LOB and trade data
2. Engineer a set of well-justified features that capture short-term market dynamics
3. Design a signal generation model based on those features
4. Implement a backtesting framework to evaluate your strategy
5. Produce a concise technical report explaining your approach and results

This is an open-ended problem. There are no right answers—only better assumptions, cleaner code, and more defensible reasoning.

---

## Dataset

You will be provided with two files:

- `lob_data.csv`: Top-10 depth of book snapshots at millisecond resolution
- `trades.csv`: Executed trades with timestamps, price, and volume

Each contains the following fields:

### lob_data.csv
- `timestamp` (int, in milliseconds)
- `bid_price_1` to `bid_price_10`, `bid_size_1` to `bid_size_10`
- `ask_price_1` to `ask_price_10`, `ask_size_1` to `ask_size_10`

### trades.csv
- `timestamp` (int, in milliseconds)
- `price` (float)
- `size` (int)

Data may be unordered, noisy, or incomplete. Your preprocessing should account for this.

---

## Technical Requirements

### 1. Data Handling

- Efficiently load and process the data (expect ~1 million rows per file)
- Align trade and book data on a consistent clock (e.g., fixed-width intervals)
- Handle missing or malformed data without silently failing
- Memory and time efficiency will be assessed

### 2. Feature Engineering

You must engineer a minimum of **five features** that reflect market state or dynamics. Examples may include, but are not limited to:

- Order Book Imbalance (OBI)
- Price momentum
- Rolling volatility (e.g., standard deviation over past N intervals)
- Relative depth or spread changes
- Trade flow imbalance

You are expected to justify your choice of features quantitatively or theoretically.

### 3. Signal Construction

Develop a signal (binary or ternary) that takes on values such as:

- +1: Enter long
- -1: Enter short
- 0: Hold/flat

Signal generation may be rule-based or model-driven. If using a machine learning approach, explain your labeling methodology and cross-validation setup. Do not use libraries that abstract away model logic (e.g., AutoML, pipelines).

### 4. Backtesting Framework

You must implement your own backtesting system from scratch. It should:

- Simulate intraday trading over at least three distinct trading sessions
- Track trade execution, inventory, and slippage
- Include basic risk controls (e.g., max position size, stop-loss)
- Output key metrics:
  - Total and per-trade PnL
  - Sharpe Ratio
  - Maximum drawdown
  - Trade frequency and win rate
- Optional: incorporate latency, queue dynamics, or price impact models

### 5. Analysis and Reporting

Prepare a technical report (2–3 pages maximum) that includes:

- A summary of your methodology
- Description and justification of features
- Explanation of signal logic
- Summary of backtest results
- Discussion of assumptions and limitations
- Clear proposals for how the strategy might be extended or improved

Reports that lack depth or are overly verbose will be penalized.

---

## Deliverables

Your submission should include:

- A Git repository or zipped folder containing all code
- A `README.md` file explaining:
  - How to run your pipeline
  - Python version and dependencies
  - Directory structure
- A `report.pdf` or `report.md` file
- At least three charts:
  - Signal vs. mid-price or returns
  - Cumulative PnL
  - Feature correlation or feature importance (if applicable)
- Optional:
  - Unit tests for key modules
  - Config files or CLI support
  - Modular components for feature generation and backtesting

Submissions that are incomplete, unstructured, or overly reliant on libraries like Backtrader, QuantConnect, or Zipline will not be considered.

---


## Evaluation Criteria

| Dimension         | Criteria                                                                 |
|-------------------|--------------------------------------------------------------------------|
| Code Quality      | Modular, well-documented, logically organized                            |
| Feature Design    | Originality, relevance to market behavior, and clear justification       |
| Signal Logic      | Coherence, robustness, and transparency of decision process              |
| Backtesting       | Correctness, realism, and interpretability of metrics                    |
| Analytical Rigor  | Depth of insights, avoidance of overfitting, and recognition of limits   |
| Communication     | Clarity and structure of the report, reproducibility of results          |

---

## Constraints and Assumptions

- You may not use external financial libraries for signal generation or backtesting.
- You may use any public Python libraries (e.g., `pandas`, `numpy`, `scikit-learn`, `matplotlib`) for general computation and visualization.
- You may not use pre-trained models or external datasets.
- You are expected to build all core components (e.g., signal logic, backtester) yourself.

---

## Submission Instructions

Submit your work as a private GitHub repository or compressed archive to the designated contact or portal. Include your name and a brief summary in the repository's `README.md`.

Do not include any proprietary or sensitive data in your submission.

---

## Final Note

This challenge is intended to reflect the kinds of problems you will encounter in a real quantitative development or research role. You are encouraged to focus on correctness, defensible reasoning, and engineering discipline over complexity or excessive ambition.

There is no perfect solution—only thoughtful approximations under uncertainty.


Thank you for your time and effort.

— X Quantitative Research & Development Team
