# K6 Performance Testing Lab

This repository contains the performance testing scripts and results for the **ITDS362 Software Quality Assurance and Testing** course. All tests are executed using [Grafana K6](https://k6.io/) against the public demo site [QuickPizza](https://quickpizza.grafana.com/).

## Repository Structure

The project is divided into two main parts: K6 Basics (Part 0) and Load Test Types (Part A).

### Part 0: K6 Basics
Contains scripts demonstrating core K6 functionalities:
* `01-first-test.js`: Basic GET request and check.
* `04-pizza-api.js`: POST request with JSON payload, headers, and Authorization token.
* `05-no-token.js`: Validating expected failure responses (401 Unauthorized).
* `06-thresholds.js`: Implementing pass/fail thresholds based on performance requirements.
* `07-requirement.js`: Translating business requirements into K6 threshold rules.
* `08-bug-hunt.js`: Debugging API behavior under load (discovering edge cases).
* `explore.js`: Utility script to fetch and log API enums (toppings and tools).

### Part A: Load Test Types
Contains a realistic user journey and various load profiles:
* `journey.js`: The common module defining the 3-step user journey (Home, Quotes, Recommendation) with think times (`sleep`).
* `a1-smoke.js`: Smoke test (1 VU, 30s) to verify script correctness.
* `a2-average.js`: Average-load test (up to 3 VUs) to measure baseline performance.
* `a3-stress.js`: Stress test (up to 5 VUs) to test system behavior near the maximum allowed limit.
* `a4-spike.js`: Spike test (jump to 5 VUs and drop) to verify system recovery.
* `a5-soak.js`: Soak test (2 VUs, 10m) to check for stability over an extended period.

### Reports and Results
* `reports/`: Contains HTML dashboard exports for tests A2 to A5.
* `RESULTS.md`: Contains the lab answers, metrics summaries, and reflection questions (Part B).

## Prerequisites
To run these scripts locally, you must have [K6 installed](https://grafana.com/docs/k6/latest/set-up/install-k6/):

**Windows (winget):**
```powershell
winget install k6 --source winget
```

## How to Run
Execute any test script using the `k6 run` command from the root of this repository:
```bash
k6 run 01-first-test.js
```

To run a test and generate a web dashboard report:
```bash
k6 run --out web-dashboard=export=reports/a2-average.html a2-average.js
```

## Testing Rules & Limitations
As requested by Grafana for the QuickPizza public site:
- **Maximum Load:** Never exceed 5 Virtual Users (VUs).
- **Maximum Duration:** Keep tests under 3 minutes (except for the 10-minute soak test using only 2 VUs).
- **No Breakpoint Tests:** No tests designed to break the public server are included or permitted.
