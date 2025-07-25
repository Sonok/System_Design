
# Fake Take-Home Assessment: Real-Time Dealer Dislocation Detection

## Overview

This take-home exercise is designed to evaluate your ability to build scalable, robust, and insightful systems for real-time market data analysis. You will work with FX quote data to identify and characterize pricing dislocations across multiple simulated liquidity providers. The project reflects realistic challenges encountered in low-latency trading infrastructure, with an emphasis on data quality, engineering design, and quantitative reasoning.

This assessment should take approximately 6–10 hours to complete. Please submit your code, documentation, and any relevant analysis within 48 hours of receiving this prompt.

---

## Objective

Design and implement a system that detects when a dealer’s quoted price for an FX pair deviates significantly from the market consensus. You will use historical tick data to simulate multiple dealers and analyze real-time dislocations.

---

## Dataset

Please download free EUR/USD tick-level FX data from:

**https://www.histdata.com/download-free-forex-data/**

Select:
- **Symbol**: EUR/USD
- **Timeframe**: Tick
- **Month**: January 2023 (or any recent available)
- File format: CSV

Each row represents a new quote with the following structure:

```
Timestamp, Bid, Ask
2023-01-02 00:00:01.123, 1.07001, 1.07021
...
```

---

## Tasks

### 1. Simulate Multiple Dealers

You will create synthetic quote streams for at least **5 distinct dealers** by introducing controlled variability to the raw data. For each dealer, apply:
- Latency (e.g., random delay between 50ms–200ms)
- Spread model (tight, wide, stale, noisy)
- Notional weight or quoting volume (optional)

Each dealer should exhibit a distinguishable quoting pattern. Ensure the combined output maintains realistic market behavior.

### 2. Implement a Real-Time Aggregator

Create a process that:
- Ingests incoming quotes chronologically
- Maintains a sliding time window of recent quotes (e.g., last 500ms)
- Computes a synthetic mid-price from other dealers (excluding the current one), using a weighted or unweighted average
- Tracks standard deviation of the mids in the window

### 3. Detect Dislocations

Define a dislocation event as follows:
- A dealer is considered "dislocated" if:
  
  ```
  |dealer_mid - synthetic_mid| > max(2 × std_dev, 0.00010)
  ```

- Mark the start and end of dislocation periods if:
  - The condition persists for N ≥ 3 consecutive quotes or
  - The duration exceeds 500 milliseconds

Track ongoing dislocations in real time and emit structured events.

### 4. Metrics and Diagnostics

For each dealer and trading session, compute:
- Total dislocation time (ms)
- Number of dislocation events
- Max dislocation magnitude
- Quote frequency
- Average spread
- Any notable correlations or edge cases

Provide diagnostics to differentiate between:
- Latency-based dislocations
- Intentional wide quoting
- Stale quote behavior

### 5. Optional Extension: System Design

Write a short design document explaining how your system could be deployed in production. Discuss:
- Real-time ingestion (e.g., Kafka, shared memory)
- State management
- Fault tolerance
- Monitoring and alerting
- Performance tradeoffs (latency vs throughput)

---

## Deliverables

1. **Codebase** with clear structure and documentation
2. **README.md** containing:
   - Build/run instructions
   - Design explanation
   - Summary of assumptions
   - Observations or takeaways
3. `dislocations.csv`: Output file with dislocation events in the format:
   ```
   start_ts, end_ts, dealer_id, max_dislocation, avg_spread_during
   ```
4. `metrics.csv`: Summary file with per-dealer statistics
5. Visualizations (optional but encouraged)

Please ensure your solution is self-contained and runnable with reasonable memory and time constraints (< 5 minutes on a typical laptop).

---

## Evaluation Criteria

| Category           | Description |
|--------------------|-------------|
| **Correctness**     | Dislocation detection logic is valid and robust |
| **Engineering**     | Code is clean, modular, documented, and testable |
| **Performance**     | Can process large tick datasets efficiently |
| **Insight**         | Distinguishes between genuine and noise-induced dislocations |
| **Communication**   | Results and rationale are clearly presented |

---

## Submission

Please submit a zip file or Git repository link with your completed project. Ensure all instructions to run your solution are included.

Thank you for your time and effort.

— X Quantitative Research & Development Team
