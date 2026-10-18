# Real-Time IoT Data Collection and Stream Processing System

## 1. Project overview
This project implements a reproducible real-time-style IoT monitoring pipeline for temperature and humidity data. Records are generated one at a time, processed incrementally with Pandas and NumPy, checked for threshold/z-score anomalies, printed to the console, stored as CSV, and visualized.

## 2. Requirements
- Python 3.10+
- pandas
- numpy
- matplotlib

## 3. Installation
```bash
python -m venv .venv
source .venv/bin/activate        # macOS/Linux
# .venv\Scripts\activate       # Windows
pip install -r requirements.txt
```

## 4. Run
From the `src` directory:
```bash
cd src
python main.py --records 120 --delay 0.05 --output-dir ../results
```
For a fast demonstration, use `--delay 0`.

The program:
1. creates a reproducible timestamped input stream;
2. yields records one at a time;
3. cleans and transforms each record;
4. updates a 10-record rolling window;
5. calculates moving average, rolling standard deviation, window min/max and cumulative event count;
6. applies threshold and local z-score rules;
7. prints continuously updated results;
8. stores all processed rows;
9. creates a visualization.

## 5. Input schema
| Field | Type | Meaning |
|---|---|---|
| timestamp | ISO datetime | Time of sensor reading |
| sensor_id | string | Sensor identifier |
| temperature_c | float | Temperature in Celsius |
| humidity_pct | float | Relative humidity percentage |

Frequency: one record per simulated second.

## 6. Detection rules
- Temperature anomaly if T < 15°C or T > 30°C.
- Humidity anomaly if RH > 85%.
- Additional temperature anomaly if absolute local z-score >= 3 after enough observations.

## 7. Outputs
- `results/input_stream.csv`
- `results/processed_results.csv`
- `results/realtime_visualization.png`

## 8. Reproducibility
The generator uses seed `42` and deterministic anomaly injection. Running the same command reproduces the same stream and processed results.

## 9. Project structure
```text
Midterm_Real_Time_IoT_Project/
├── README.md
├── requirements.txt
├── report/
│   └── Technical_Report.docx
├── src/
│   ├── __init__.py
│   ├── generator.py
│   ├── processor.py
│   ├── visualization.py
│   └── main.py
├── data/
│   └── input_stream.csv
└── results/
    ├── processed_results.csv
    └── realtime_visualization.png
```
