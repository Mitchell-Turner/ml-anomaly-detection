# Invoice Anomaly Detection

This Python script performs invoice anomaly detection using the Isolation Forest algorithm from the scikit-learn library. It loads invoice data from a CSV file, performs feature engineering, fits an Isolation Forest model, flags anomalies, computes per-feature z-scores for explanation, and exports the flagged anomalies along with their explanations to an Excel file.

## Features

- **Automated Data Processing**: Loads invoice data from a CSV file
- **Feature Engineering**: Creates engineered features for anomaly detection
- **Anomaly Detection**: Identifies potential anomalies in invoice data using Isolation Forest
- **Anomaly Explanation**: Computes per-feature z-scores to explain the flagged anomalies
- **Excel Output**: Generates a formatted Excel report with flagged anomalies and explanations

## Requirements

- Python 3.x
- scikit-learn
- pandas
- numpy
- openpyxl

To install the required libraries, run:

```
pip install scikit-learn pandas numpy openpyxl
```

## Usage

To run the script, use the following command:

```
python invoice_anomaly_detection.py --input_csv master_invoices.csv \
                                    --output_excel anomalies.xlsx \
                                    --contamination 0.002 \
                                    --features "AP Amount" "Supplier" "Invoice Date" \
                                    --z_threshold 3.0
```

### Parameters

- `--input_csv` (str): Path to the input CSV file containing invoice data. Default is 'master_invoices.csv'.
- `--output_excel` (str): Path to the output Excel file for anomalies and explanations. Default is 'invoice_anomalies_with_reasons.xlsx'.
- `--contamination` (float): Proportion of data points to be flagged as anomalies. Default is 0.002.
- `--features` (list): List of feature column names to use for anomaly detection. Default is ['AP Amount', 'Supplier', 'Invoice Date'].
- `--z_threshold` (float, optional): Threshold for filtering anomalies based on z-score. Default is None.

## Functionality

The script performs the following steps:

1. Loads the invoice CSV file
2. Parses the 'Invoice Date' column if present in the specified features
3. Performs feature engineering
4. Builds a feature matrix for the model
5. Handles missing values
6. Fits an Isolation Forest model
7. Scores and flags anomalies
8. Computes per-feature z-scores for explanation
9. Determines the top driver feature and its z-value for each flagged anomaly
10. Filters the anomalies based on the specified z-score threshold (if provided)
11. Exports the flagged anomalies along with their explanations to an Excel file
12. Logs the summary of the anomaly detection process

## Output

The script generates an Excel file with the flagged anomalies and their explanations. It also logs the summary of the anomaly detection process, including the number of invoices scanned and anomalies flagged.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- The anomaly detection algorithm used in this script is based on the Isolation Forest implementation from the scikit-learn library.
